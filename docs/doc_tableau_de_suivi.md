# Documentation technique du Tableau de Suivi (TS)
## Telecom Etude - Trésorier·e 2025-2026

> Ce document explique l'architecture du TS, la logique de chaque onglet, les scripts Apps Script associés, et les points d'attention pour maintenir, modifier ou débugger le fichier.

## 1. Vue d'ensemble

Le Tableau de Suivi (TS) est un fichier Google Sheets hébergé sur le Google Drive de Telecom Etude. Il couvre l'intégralité de l'exercice fiscal (1er mai au 30 avril). **C'est le seul fichier que le trésorier maintient activement** : le VT n'y touche jamais.

Le TS remplit trois fonctions :

1. **Suivi opérationnel** : facturation clients, bulletins de versement, rétributions, achats.
2. **Déclaratif** : génération automatique des fichiers TVA et BRC mensuels, suivi des échéances.
3. **Pilotage financier** : budget prévisionnel/réalisé, suivi des disponibilités, cut-off comptable.

Un menu custom apparait dans Google Sheets à l'ouverture (via `onOpen`) :
- **Declaratif** : Générer BRC ou TVA pour un mois donné.
- **Suivi d'etude** : Générer les sheets de facturation.
- **Remise a zero** : Créer un nouveau TS vierge pour l'année suivante.

Pour accéder aux Apps Script, aller dans Extensions > Apps Script. 

## 2. Architecture des onglets

### Onglets de saisie (à remplir par le trésorier)

| Onglet | Rôle |
|---|---|
| `Budget` | Budget prévisionnel (Bas/Moyen/Haut) vs réalisé |
| `Suivi des études` | Une ligne par étude, de la signature CE au PVRF |
| `Factures ventes` | Une ligne par facture émise (client) |
| `Factures dachats` | Une ligne par facture reçue ou NDF |
| `BV & RM` | Une ligne par bulletin de versement émis |
| `Intervenants` / `Fournisseurs` / `Clients` | Référentiels tiers |
| `Déclaratifs mensuels` | Suivi des deadlines BRC et TVA mois par mois |
| `DADS - DAS2` | Agrégat annuel des BV pour la DADS et la DAS2 |

### Onglets de paramétrage

| Onglet | Rôle |
|---|---|
| `Paramétrage` | Identifiants des templates Drive, dossiers destination, données JE |
| `Taux cotisations` | Taux AM, AT, SMIC utilisés dans les calculs BV |

### Onglet de dashboard et KPIs

| Onglet | Rôle |
|---|---|
| `Dashboard` | Graphiques de suivi financier et des tâches à faire |
| `KPIs` | Indicateurs de performance clés (ex : délai moyen de paiement) |
| `Indicateurs qualité` | Suivi des indicateurs de qualité pour le pôle qualité |

### Onglets de référence (ne pas modifier)

| Onglet | Rôle |
|---|---|
| `Pays` | Table de référence pour les pays et nationalités |
| `Datas` / `Datas_VT_*` / `Datas_suivi_etudes` | Données sources pour les tableaux croisés dynamiques |
| `Introduction` / `Mode d'emploi` | Documentation interne du fichier |

### Onglets non utilisés à Telecom Etude

| Onglet | Raison |
|---|---|
| `Suivi Disponibilités` | Pas de nécessité de suivi des disponibilités spécifique, géré via le budget |
| `Cut-off` | Utilisation du tableau fourni par l'expert-comptable |
| `TVA_Etrange` | Utilisation de notre propre tableau de TVA |
| `TVA` / `TVA trimestriel` | Génération via script dans un autre tableau, donc celui n'est pas utilisé |
| `URSSAF` | Génération via script dans un autre tableau, donc celui n'est pas utilisé |


## 3. Onglet `Suivi des études`

### Structure des colonnes (ligne 1 = en-tête)

| Colonne | Contenu | Notes |
|---|---|---|
| A | Numéro étude | Ex : `225001`, `224AA-03` |
| B | Etat actuel | Dropdown : En cours, Terminée, Rupture... |
| C | Prise en compte | Case à cocher |
| D | Entreprise | |
| E | Client | Nom du contact |
| F | Nom de l'étude | |
| G | Sheet de facturation | Lien Drive généré automatiquement |
| H | Générer sheet | Case à cocher - déclenche la génération via Apps Script |
| I | Date lancement pré-étude | |
| J | Date de signature | Date effective |
| K | Date de signature prévisionnelle | |
| L | Délai (sem) | |
| M | Date de signature PVRF | |
| N | Date de signature PVRF prévisionnelle | |
| O | Prix JEH | |
| P | Nombre JEH | |
| Q | Total prestation | = O * P |
| R | Pourcentage frais de dossier | En général 5% |
| S | Frais de dossier | = Q * R |
| T | Fini mandat N | Case à cocher |
| U-X | Ratios / JEH / Prestation mandat N | Calculs pour cut-off |
| Y-AA | JEH / Prestation / Frais mandat N+1 | Calculs pour cut-off |

### Génération du sheet de facturation

Lorsque la case **H (Générer sheet)** est cochée, le script `genererSheetFacturation()` (fichier `SheetFacturation.gs`) :
1. Vérifie que G est vide, F et A sont remplis, J (date de signature) est renseignée.
2. Copie le template Drive (constante `ID_TEMPLATE_SHEET_FACT` dans `constants.gs`) dans le dossier destination (`ID_DOSSIER_SHEETS_FACT`).
3. Nomme le fichier `{numEtude} {nomEtude}`.
4. Écrigt l'URL dans la colonne G et décoche H.

**Pour changer de template** : modifier `ID_TEMPLATE_SHEET_FACT` dans `constants.gs`.

## 4. Onglet `Factures ventes`

### Structure des colonnes (ligne 4 = en-tête, données à partir de la ligne 5)

| Colonne | Contenu | Notes |
|---|---|---|
| B | Jours de retard | Calculé automatiquement |
| C | N° facture | Ex : `FAC-518-223AE-07-3` |
| D | Tier | Nom du client |
| E | Type | Facture d'Acompte / Intermédiaire / Solde / Avoir |
| F | Référence étude | |
| G | Libellé | |
| H | TVA Client | Lien vers onglet `TVA_Etrange` si étranger |
| I | TVA | Numéro de TVA intracommunautaire du client |
| J | Pièce | Nom du fichier PDF joint |
| K | Date émission | |
| L | Date échéance | = K + 30 jours (60 pour partenaires) |
| M | Nb JEH | |
| N | HT JEH | |
| O | HT Dossier | |
| P | HT frais | |
| Q | HT acompte | Montant négatif si déduction d'acompte |
| R | Total HT | = SUM(N:Q) |
| S | Taux TVA | |
| T | TVA à collecter | = R * S |
| U | TTC | = R + T |
| V | Date paiement | Saisie manuelle à réception |
| W | Statut de paiement | Calculé : Réglé / En attente / En retard |
| X | Jours de retard | = V - L (si négatif = paiement en avance) |
| Y | Mois déclaratif de TVA | Ex : `Mai 2025` |
| Z | Budget | Ligne du poste budgétaire correspondant |
| AA | TVA déclaré | Case à cocher - cochée par le script TVA |
| AB | DES | Pour déclaration européenne si applicable |
| AC | VT | Case à cocher : bon à payer VT |
| AD | BQ | Case à cocher : enregistrement bancaire |
| AE | Annulée / avoir | Case à cocher |
| AF | BV émis | Case à cocher : BV correspondant généré |
| AG | Frais sous-traitance | |
| AH | Type de paiement | Client / Partenaire |
| AI | Commentaires | |
| AJ à AS | Processus de relance | Etapes 1 à 4 + dates |

### Point d'attention : la colonne AA (TVA déclaré)

Cette case est cochée **automatiquement** par le script `TVA.gs` lors de la génération du fichier TVA mensuel. Ne pas la cocher manuellement, sauf correction exceptionnelle. Une ligne dont la case est déjà cochée ne sera plus prise en compte dans les prochaines déclarations TVA.

## 5. Onglet `Factures dachats`

### Structure des colonnes (ligne 4 = en-tête, données à partir de la ligne 5)

| Colonne | Contenu | Notes |
|---|---|---|
| B | Nb jours | Délai de paiement effectif |
| C | N° pièce | Ex : `ACH-001-250401-FAC OVH` |
| D | Pièce | Nom du fichier PDF |
| E | Fournisseur | |
| F | Type | Facture fournisseur / NDF / Don / Impôt |
| G | Type d'achat | Service / Bien / Immobilisation |
| H | Libellé | |
| I | N° TVA Fournisseur | |
| J | TVA | TVA FR / TVA Intracom / TVA Extracom |
| K | Date pièce | |
| L | Mois déclaratif de TVA | Ex : `Mai 2025` |
| M | HT 1 | Premier taux |
| N | Taux TVA 1 | |
| O | TVA 1 à déduire | = M * N |
| P | HT 2 | Deuxième taux si applicable |
| Q | Taux TVA 2 | |
| R | TVA 2 à déduire | = P * Q |
| S | Total HT | = M + P |
| T | TVA à déduire | = O + R |
| U | TTC | = S + T |
| V | Budget | Poste budgétaire |
| W | Date de paiement | |
| X | Nb jours échéance | = W - K |
| Y | ACH | Case à cocher : pièce enregistrée |
| Z | BQ | Case à cocher : enregistrement bancaire |
| AA | DAS2 | Case à cocher : à déclarer en DAS2 |
| AB | TVA déclaré | Case à cocher - cochée automatiquement par le script |
| AC | Relance reçu | Case à cocher |
| AD | Commentaires | |

### Règle des types de pièces exclus de la TVA

Dans le script `TVA.gs`, la fonction `remplirRecapAchat` ignore les lignes dont la nature est `Don` ou `Impôt`. Ces types ne génèrent pas de TVA déductible.

## 6. Onglet `BV & RM`

### Structure des colonnes (ligne 6 = en-tête, données à partir de la ligne 8)

| Col | Contenu | Notes |
|---|---|---|
| B | N° BV | Ex : `BV-001-223045-2` |
| C | Référence Etude | |
| D | Date émission | |
| E | Date de paiement | |
| F | Numero de Virement ou cheque | |
| G | Mois décla URSSAF | Ex : `Janvier 2026` |
| H | Nb JEH | |
| I | Rétri. brute | = Nb JEH * Prix JEH |
| J | Taux | Référence au tableau `Taux cotisations` (A, B ou C) |
| K | Nom Prenom | Concaténation |
| L | NOM | |
| M | Prénom | |
| N | N° sécu | |
| O | Adresse fiscale | Adresse complète (rue + CP + ville) |
| P | Commune naissance | |
| Q | Date naissance | |
| R | RIB | IBAN complet |
| S | N° RM | |
| T | N° AVRM | Si avenant au RM |
| U | Mission | Domaine (ex : Informatique) |
| V | Taux AM | Taux cotisation Assurance Maladie |
| W | Taux AT | Taux Accident du Travail |
| X | BASE URSSAF | Plancher de calcul (fraction du SMIC) |
| Y | Assiette cotisation | = max(rétri brute, base URSSAF) |
| Z | Cotiz. (Junior) | Part cotisation JE |
| AA | Cotiz arrondi (Junior DADS) | Arrondi pour la DADS |
| AB | Cotiz. (étudiant) | Part cotisation étudiant |
| AC | Total cotiz. | = Z + AB |
| AD | Rétri. nette | = I - AC |
| AE | Rétribution brut /JEH | = I / H |
| AF | BV | Lien vers le BV généré (Google Sheets) |
| AG | BQ | Case à cocher : virement effectué |
| AH | Pièce | Lien vers le BV en PDF |
| AI | Générer BV | Case à cocher - déclenche la génération |

### Génération automatique des BV

Lorsque la colonne **AI (Générer BV)** est coché, le script `generate_bv()` (fichier `BV.gs`) :
1. Charge les données de la ligne.
2. Récupère depuis `Paramétrage` (plage `B28:F28`) l'ID du template BV et le dossier destination.
3. Copie le template, nomme le fichier avec le N° BV.
4. Remplace les cellules-balises dans l'onglet `Fiche BV` du fichier copié.
5. Écrit l'URL dans la colonne AF et décoche AI.

### Cellules-balises du template BV

Le template BV contient des cellules fixes à des adresses précises (définies comme constantes en haut de `BV.gs`) :

| Constante | Cellule | Donnée |
|---|---|---|
| `BV_N_CELL` | B2 | Numéro BV |
| `BV_DATE_TODAY_CELL` | E2 | Date d'émission |
| `BV_INTERVENANT_NOM_CELL` | H5 | Nom |
| `BV_INTERVENANT_PRENOM_CELL` | H6 | Prénom |
| `BV_INTERVENANT_ADRESSE_CELL` | H7 | Rue |
| `BV_INTERVENANT_CP_CELL` | H8 | CP + ville (extrait automatiquement de l'adresse) |
| `BV_INTERVENANT_SS_CELL` | H9 | N° sécu |
| `BV_INTERVENANT_RM_CELL` | H10 | N° RM (+ mention AVRM si avenant) |
| `BV_INTERVENANT_MISSION_CELL` | H11 | Mission |
| `BV_RET_BRUT_CELL` | E14 | Rétribution brute |
| `BV_JEH_CELL` | E15 | Nb JEH |
| `BV_BASE_URSSAF_CELL` | E17 | Base URSSAF |
| `BV_TAUX_SS_CELL` | H23 | Taux AM |
| `BV_TAUX_AT_CELL` | F24 | Taux AT |
| `BV_PAIEMENT_CELL` | H39 | N° virement + date paiement |

> **Si le template BV change de structure**, il faut impérativement mettre à jour ces constantes dans `BV.gs`. Ne pas modifier l'adresse des cellules dans le template sans mettre à jour le script.

### Cas particulier : le trésorier est lui-même intervenant

Le trésorier ne peut pas générer son propre BV. Dans ce cas, c'est le VT qui remplit la ligne dans le TS et génère le BV, puis le Président qui exécute le virement.

## 7. Onglet `Déclaratifs mensuels`

Cet onglet sert de tableau de bord des échéances déclaratives. Il est alimenté **automatiquement** par les scripts TVA et BRC via la fonction `insererChipFichier()`.

| Colonne | Contenu |
|---|---|
| A | Mois (ex : `mai 2025`) |
| B | Date réception relevé bancaire |
| C | Date signature état de rapprochement bancaire |
| D | Deadline BRC (= 15 du mois suivant) |
| E | En retard BRC (formule booléenne) |
| F | Date effective déclaration BRC |
| G | Lien fichier BRC généré |
| H | Deadline TVA (= 24 du mois suivant) |
| I | En retard TVA |
| J | Date effective déclaration TVA |
| K | Lien fichier TVA généré |

Le lien dans G et K est inséré automatiquement lors de la génération du fichier correspondant. La correspondance mois/ligne repose sur la correspondance exacte de la valeur de la colonne A avec le paramètre saisi dans la boîte de dialogue du script (ex : `Mai 2025`). 

## 8. Scripts Apps Script

### Architecture des fichiers

| Fichier | Fonction principale |
|---|---|
| `constants.gs` | IDs Drive centralisés (templates et dossiers) |
| `main.gs` | Crée les menus à l'ouverture (`onOpen`) |
| `BV.gs` | Génération des bulletins de versement |
| `TVA.gs` | Génération des fichiers TVA mensuels |
| `BRC.gs` | Génération des fichiers BRC mensuels |
| `SheetFacturation.gs` | Génération des sheets de facturation par étude |
| `insererChipFichier.gs` | Insertion du lien fichier dans `Déclaratifs mensuels` |
| `RemiseAZero.gs` | Création d'un TS vierge pour l'année suivante |
| `Code.gs` | Fonction `archive()` utilisée pour archiver un onglet |

### IDs Drive dans `constants.gs`

Tous les IDs Drive sont centralisés dans `constants.gs`. C'est le seul fichier à modifier si un template ou un dossier est déplacé ou recréé :

| Constante | Usage |
|---|---|
| `ID_TEMPLATE_TVA` | Template fichier TVA |
| `ID_DOSSIER_TVA` | Dossier destination des fichiers TVA |
| `ID_TEMPLATE_BRC` | Template fichier BRC |
| `ID_DOSSIER_BRC` | Dossier destination des fichiers BRC |
| `ID_TEMPLATE_SHEET_FACT` | Template sheet de facturation |
| `ID_DOSSIER_SHEETS_FACT` | Dossier destination des sheets de facturation |

Les scripts `TVA.gs`, `BRC.gs` et `SheetFacturation.gs` référencent ces constantes.

> **Exception** : les IDs BV (template et dossier destination) restent externalisés dans l'onglet `Paramétrage` (plage `B28:F28`), intentionnellement, pour pouvoir les modifier sans ouvrir l'éditeur de script.

### La fonction `detecterLignesCA3` (TVA.gs)

C'est la fonction la plus complexe du TS. Elle détermine les cases à remplir dans le formulaire CA3 (déclaration TVA) en fonction de :
- `type` : `ACHAT` ou `VENTE`
- `lieuTVAClient` : `TVA FR`, `TVA Intracom`, `TVA Extracom`
- `natureOperation` : `Service`, `Bien`, `Immobilisation`, `Facture d'Avoir`, etc.
- `date` : pour distinguer les mois (ligne 20 vs ligne 21 de la CA3)

La référence légale utilisée est disponible sur KiwiX CNJE (lien dans le commentaire du code). En cas de changement de réglementation TVA, c'est cette fonction qu'il faut mettre à jour.

**Cas particuliers gérés :**
- Les `Subvention NC`, `Cotisation`, `Pro Forma` : ignorés (pas de TVA).
- Les `Don` et `Impôt` dans les achats : ignorés.
- TVA taux 0 sur une vente : alerte utilisateur + ligne ignorée.

## 9. Remise à zéro du TS

La fonction `remiseAZero()` (fichier `RemiseAZero.gs`) crée une copie du TS actuel et vide les données saisies, en conservant formules, mise en forme et validations.

### Feuilles protégées (non vidées)

Les onglets suivants ne sont jamais touchés par la remise à zéro :
`Introduction`, `Mode d'emploi`, `Pays`, `Dashboard`, `Paramétrage`, `Taux cotisations`, `KPIs`, `TVA_Etrange`, `Indicateurs qualité`, `Cut-off`, `TVA`, `URSSAF`, `Datas`, `Datas_VT_Tiers`, `Datas_VT_Etudes_Clients`, `Datas_suivi_etudes`.

### Ce qui est préservé dans les autres onglets

- Les lignes et colonnes gelées (en-têtes).
- Toutes les formules.
- La mise en forme et les bordures.
- Les règles de validation de données (dropdowns, cases à cocher).
- Les filtres actifs sont réinitialisés (critères supprimés, filtre conservé).

### Ce qui est effacé

- Toutes les valeurs saisies dans la zone de données.
- Les cases à cocher remises à `FALSE`.

> **Point d'attention** : les onglets `Budget` et `Suivi Disponibilités` ont un traitement spécial car leurs colonnes gelées contiennent aussi des données à conserver. La remise à zéro vide uniquement les colonnes au-delà des colonnes gelées pour ces deux onglets.

## 10. Points d'attention et bugs connus

### Parsing de l'adresse fiscale dans BV.gs

La fonction `createBV` tente de séparer la rue du code postal via la regex `(.*)([0-9]{5,}.*)`. Si l'adresse ne contient pas de code postal à 5 chiffres (ex : adresse étrangère), la variable `bv_intervenant_cp` reste `undefined`. Le script ne plante pas mais le champ CP du BV sera vide. Il faut alors remplir manuellement dans le BV généré.

### Correspondance mois dans `insererChipFichier`

La recherche de la ligne correspondant au mois dans `Déclaratifs mensuels` se fait par comparaison de chaînes (`toLowerCase`). Si la valeur en colonne A est `mai 2025` et que le script reçoit `Mai 2025`, ça fonctionne. Si la valeur contient des espaces en trop ou une orthographe différente, la ligne ne sera pas trouvée et une alerte s'affiche.

### Colonne S masquée dans `Factures ventes`

La colonne S (TVA) de l'onglet `Factures ventes` est dans un groupe replié. Le script `remplirRecapVentes` l'expand temporairement le temps de lire les données, puis la replie. Si le script est interrompu entre les deux, la colonne reste dépliée. Ce n'est pas bloquant mais peut surprendre.

### Lien vers le BV généré (colonne AF vs Pièce colonne AH)

La colonne AF (`BV`) contient le lien vers le Google Sheets du BV. La colonne AH (`Pièce`) est prévue pour le lien vers le PDF exporté du BV. L'export en PDF et l'écriture dans AH ne sont **pas automatisés** : c'est une étape manuelle après génération.

## 11. Modifier ou étendre le TS

### Ajouter une colonne dans un onglet de saisie

1. Insérer la colonne à l'endroit souhaité.
2. Si l'onglet a un script associé (`BV & RM`, `Factures ventes`, `Factures dachats`), vérifier que les constantes d'index de colonnes sont mises à jour (dans `BV.gs` : `BV_COL_*`; dans `TVA.gs` : les index numériques de `getRange`).
3. Vérifier que la remise à zéro ne casse pas les formules de la nouvelle colonne (tester avec `remiseAZero`).

### Modifier les taux de cotisation

L'onglet `Taux cotisations` contient un ou plusieurs tableaux (Taux A, B, C). La colonne H de `BV & RM` permet de choisir quel taux appliquer par ligne. En début d'année civile (janvier), si le SMIC ou le taux AT change, il faut l'ajouter dans une nouvelle colonne du tableau `Taux cotisations`. 

### Changer l'exercice fiscal

Dans l'onglet `Paramétrage`, les dates de l'exercice fiscal sont en ligne 3 (colonnes D et E). Les modifier met à jour automatiquement tous les calculs qui en dépendent. Penser également à mettre à jour les libellés des mois dans `Déclaratifs mensuels`.

### Ajouter un nouveau type de document dans la TVA

Si un nouveau type de pièce doit être intégré à la CA3, ajouter le cas correspondant dans `detecterLignesCA3` dans `TVA.gs`, en consultant la documentation KiwiX CNJE sur les lignes CA3.

## 12. Checklist de reprise en main

A faire en début de mandat, après avoir reçu le TS de la passation :

- [ ] Vérifier les dates de l'exercice fiscal dans `Paramétrage`.
- [ ] Vérifier les IDs Drive dans `Paramétrage` (plage B28:F28) : template BV et dossier destination.
- [ ] Vérifier les IDs Drive dans `constants.gs` : templates TVA, BRC, sheet de facturation et dossiers destination associés.
- [ ] Ouvrir le menu "Remise a zero" et créer le TS vierge pour l'exercice en cours (le TS de passation devient l'archive).
- [ ] Vérifier que les mois sont bien présents et orthographiés correctement dans `Déclaratifs mensuels`.
- [ ] Vérifier les taux de cotisation dans `Taux cotisations` (mise à jour SMIC si nécessaire).
- [ ] Tester la génération d'un BV de test et vérifier le résultat dans Drive.
