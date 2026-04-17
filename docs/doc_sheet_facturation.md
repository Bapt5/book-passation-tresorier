# Documentation du Sheet de Facturation

## 1. Vue d'ensemble

Le sheet de facturation est un fichier Google Sheets **créé automatiquement par le TS** pour chaque étude (voir section 3 du TS sur `Suivi des études`, colonne H). Il est nommé `{numEtude} {nomEtude}` et stocké dans le  Drive Trésorerie > Sheets de facturation des études.

Il contient deux onglets :
- **`Phases`** : données de l'étude (infos client, phases de prestation, intervenants).
- **`Facture`** : plan de facturation (acompte, factures intermédiaires, solde, synthèses financières).

Des boutons sont disponible dans l'onglet `Facture`  pour générer les factures en Google Docs.

## 2. Onglet `Phases`

### Bloc "Informations étude" (colonnes C et K, lignes 1 à 9)

Ces cellules sont lues par le script pour remplir les variables de la facture.

| Cellule | Contenu | Notes |
|---|---|---|
| C1 | `isCE` | Booléen : `TRUE` si Convention d'Etude, `FALSE` si Bon de Commande |
| C2 | Référence étude | Ex : `225001` |
| C3 | Nom de l'étude | Ex : `Refonte site web` |
| C4 | Référence avenant | Ex : `ACE-3-225001` ou `BCR-1-225AB-02` si avenant, vide sinon |
| G2 | Pourcentage frais de dossier | En pourcentage du total prestation (ex : `5%`) |
| G3 | Pourcentage frais de suivi | En pourcentage du total prestation (souvent `0%`) |
| G4 | Pourcentage acompte | En pourcentage du total HT (ex : `30%`) |
| H2, H3, H4 | Montants calculés automatiquement à partir des pourcentages (peuvent être modifiés manuellement si besoin) | |
| K2 | Entreprise | Raison sociale du client |
| K3 | Contact | Nom du contact chez le client |
| K4 | Poste | Intitulé de poste du contact |
| K5 | Adresse | Rue |
| K6 | Ville | CP + ville |
| K7 | SIREN | |
| K9 | Délais de paiement | En jours (ex : `30`) |

> **Règle contractuelle** : 30 jours pour les clients standards (60 si le client a négocié). C'est cette valeur qui calcule automatiquement la date d'échéance sur la facture générée.

### Bloc "Phases" (à partir de la ligne 10, colonnes B à G)

Une ligne par phase de l'étude. Le script lit la plage `B10:G` jusqu'à la première ligne vide.

| Colonne | Contenu |
|---|---|
| B | Numéro de phase |
| C | Intitulé de la phase |
| D | Prix JEH |
| E | Nombre de JEH |
| F | Prix total de la phase (= D * E) |
| G | Numéro de facture associée (`1`, `2`... ou `"finale"` pour le solde) |

La colonne G est centrale : elle détermine **quelle(s) phase(s) apparaissent sur quelle facture**.

- `1`, `2`, `3`... : la phase apparaît sur la facture intermédiaire numéro correspondante.
- `finale` : la phase apparaît sur la facture de solde.
- toutes les phases apparaissent sur la facture d'acompte.

## 3. Onglet `Facture`

### Cellules de configuration

| Cellule | Contenu |
|---|---|
| I | Date de signature des PVRI (utilisée pour les factures intermédiaires) |
| L12 | Date de signature du PVRF (utilisée pour la facture de solde) |

### Bloc "Factures intermédiaires" (lignes 5+, colonnes E à I)

Une ligne par facture intermédiaire prévue.

| Colonne | Contenu |
|---|---|
| E | Numéro de la facture intermédiaire (`1`, `2`...) |
| F | Prestation HT |
| G | Frais de dossier HT |
| H | Frais divers HT |
| I | Date de signature du PVRI correspondant |

La ligne 4 contient les en-têtes de F, G, H : ces libellés sont utilisés directement dans le tableau de synthèse de la facture générée.

### Bloc "Synthèse solde" (colonnes K et L, lignes 4 à 10)

Utilisé pour le tableau de synthèse de la facture de solde. Le script lit la plage `K4:L10`.

| Colonne K | Colonne L |
|---|---|
| Libellé de la ligne sur la facture | Montant |

Contient typiquement : total prestation, frais de dossier, déduction acompte, déduction factures intermédiaires, net à payer.

## 4. Script de génération (`Code.gs`)

### Architecture générale

Le script expose trois fonctions principales, accessibles via un menu dans le sheet de facturation :

| Fonction | Usage |
|---|---|
| `genererFactureAcompte()` | Génère la facture d'acompte (une seule par étude, optionnelle) |
| `genererFactureIntermediaire()` | Génère une facture intermédiaire (autant que de phases intermédiaires) |
| `genererFactureSolde()` | Génère la facture de solde (une seule, en fin d'étude) |

Toutes trois partagent le même template Google Docs (ID `idTemplate` en haut du script).

### Flux d'exécution commun

1. Lecture des infos étude dans l'onglet `Phases` (`getInformationsEtude`).
2. Demande à l'utilisateur du numéro d'incrémentation globale de la facture (numéro séquentiel toutes études confondues, à lire dans le TS `Factures ventes`).
3. Demande de l'ID du dossier Drive de destination.
4. Copie du template Google Docs dans le dossier cible, nommé avec la référence facture.
5. Remplacement des variables dans le corps du document (`remplacerVariables`).
6. Remplissage du tableau des phases (`remplirTableauPhases`).
7. Remplissage du tableau de synthèse (`remplirTableauSynthese`).
8. Sauvegarde et fermeture du document.

### Référence de la facture générée

La référence suit le format : `FAC-{incrementFacture}-{referenceEtude}-{incrementFactureEtude}`

Exemples :
- `FAC-518-223AE-07-3` : 518e facture tous clients, étude 223AE-07, 3e facture de cette étude.
- `FAC-519-223AE-06-6` : 519e facture tous clients, étude 223AE-06, 6e facture de cette étude.

Le numéro `incrementFactureEtude` est calculé ainsi :

| Type | Calcul |
|---|---|
| Acompte | Toujours `1` |
| Intermédiaire | `numFacture` si pas d'acompte, `numFacture + 1` si acompte existe |
| Solde | `(dernière FI + 1)` si pas d'acompte, `(dernière FI + 2)` si acompte existe |

### Variables remplacées dans le template Google Docs

| Variable dans le template | Valeur injectée |
|---|---|
| `{{ref facture}}` | Référence complète de la facture |
| `{{Date}}` | Date du jour |
| `{{Date échéance}}` | Date du jour + délai de paiement |
| `{{Type facture}}` | `d'acompte` / `intermédiaire` / `de solde` |
| `{{Type de contrat}}` | `Convention d'étude` ou `Bon de commande` |
| `{{ref contrat}}` | `CE-{refEtude}` ou `BC-{refEtude}` |
| `{{Avenant}}` | Texte de l'avenant si applicable (voir ci-dessous) |
| `{{Date signature PVR}}` | `Date de signature du PVR : {date}` ou vide |
| `{{Etude n°}}` | Référence étude |
| `{{Dénomination étude}}` | Nom de l'étude |
| `{{Entreprise}}` | Raison sociale |
| `{{Contact}}` | Nom du contact |
| `{{Poste}}` | Intitulé de poste |
| `{{Adresse}}` | Rue |
| `{{Ville}}` | CP + ville |
| `{{SIREN}}` | SIREN client |

> **Important** : si une variable est absente ou mal orthographiée dans le template, elle n'est pas remplacée et reste visible telle quelle dans le PDF final. Toujours vérifier le document généré avant envoi.

### Gestion des avenants

La cellule C4 de l'onglet `Phases` peut contenir une référence d'avenant.

**Pour une Convention d'Etude (CE)** : le script reconstruit automatiquement la liste complète des avenants. Si C4 vaut `ACE-3-225001`, le texte généré sera `(modifiée par ACE-1-225001, ACE-2-225001, ACE-3-225001)`. Le script extrait le numéro final (ici `3`) et génère la liste de `ACE-1-...` à `ACE-N-...`.

**Pour un Bon de Commande (BC)** : le texte généré est simplement `(rectifié par {valeur de C4})`.

**Si aucun avenant** (C4 vide) : la variable `{{Avenant}}` est remplacée par une chaîne vide.

### Tableau des phases dans la facture

La fonction `remplirTableauPhases` recherche dans le document Google Docs un tableau dont la cellule en haut à gauche contient exactement le texte `Phase`. Elle insère ensuite les lignes de données correspondant au numéro de facture demandé.

Chaque ligne insérée contient : numéro de phase, intitulé, prix JEH, nb JEH, prix total.

La dernière ligne du tableau (déjà présente dans le template) est mise à jour avec les totaux : total JEH et total prestation.

### Tableau de synthèse dans la facture

La fonction `remplirTableauSynthese` recherche un tableau dont la cellule en haut à gauche contient exactement `Synthèse`. Elle y insère les lignes dont le montant est non nul.

**Source des données selon le type :**
- Acompte : plage `Facture!B4:C9`
- Intermédiaire : colonnes F, G, H de la ligne correspondante dans l'onglet `Facture` (libellés pris en ligne 4)
- Solde : plage `Facture!K4:L10`

## 5. Mode opératoire

### Générer une facture d'acompte

1. Ouvrir le sheet de facturation de l'étude.
2. Vérifier que C4 (`referenceAvenant`) est rempli si un avenant a été signé.
3. Vérifier que C7 (`montant acompte`) est renseigné dans l'onglet `Facture`.
4. Dans l'onglet `Phases`, vérifier que les phases sont toutes renseignées (colonnes B à F).
5. Utiliser le menu > **Générer facture d'acompte**.
6. Saisir le numéro d'incrémentation globale (visible dans le TS `Factures ventes` : c'est le numéro de la prochaine facture à créer).
7. Saisir l'ID du dossier Drive de destination (dossier de l'étude dans Drive).
8. Vérifier le document généré avant envoi.

### Générer une facture intermédiaire

1. Vérifier que la colonne G de l'onglet `Phases` est bien renseignée pour les phases concernées par cette facture intermédiaire (valeur = numéro de la FI : `1`, `2`...).
2. Vérifier que la ligne correspondante dans l'onglet `Facture` (colonne E = numéro de FI) est renseignée, notamment la date PVRI en colonne I.
3. Menu > **Générer facture intermédiaire**.
4. Saisir le numéro d'incrémentation globale.
5. Saisir le numéro de la facture intermédiaire (correspond à la valeur en colonne E de l'onglet `Facture`).
6. Saisir l'ID du dossier Drive de destination.

### Générer la facture de solde

1. Vérifier que la date de signature du PVRF est renseignée en cellule `Facture!L12`.
2. Vérifier que la plage `Facture!K4:L10` est remplie (synthèse finale avec déductions).
3. Vérifier que toutes les phases de la colonne G valant `"finale"` sont bien renseignées.
4. Menu > **Générer facture de solde**.
5. Saisir le numéro d'incrémentation globale.
6. Saisir l'ID du dossier Drive de destination.

> Le script détecte automatiquement le numéro de la facture de solde en cherchant le maximum des valeurs numériques dans la colonne G de l'onglet `Phases` et en ajoutant 1.

## 6. Points d'attention et comportements à connaître

### Le template Google Docs est partagé entre toutes les études

L'ID `idTemplate` est hardcodé en haut du script. Si le template est modifié, toutes les futures factures en bénéficient immédiatement. Si une modification casse les marqueurs `{{...}}` ou les noms de tableaux (`Phase`, `Synthèse`), toutes les générations futures échoueront.

> Ne jamais renommer les tableaux dans le template, ne jamais modifier l'orthographe des variables `{{...}}`.

### Le numéro d'incrémentation globale n'est pas automatique

C'est le seul champ entré manuellement à chaque génération. Il correspond au numéro séquentiel de la facture dans le TS (`Factures ventes`, colonne C). Avant de générer, consulter la dernière ligne du TS pour connaître le prochain numéro disponible.

### Vérification du dossier Drive

Si l'ID de dossier est incorrect ou inaccessible, le script affiche une erreur et s'arrête sans créer de fichier. En cas d'erreur, vérifier :
- que l'ID est bien celui du dossier (et non d'un fichier),
- que le compte Google du trésorier a les droits d'écriture sur ce dossier.

### Avenants : format attendu en C4

La logique de reconstruction de la liste des avenants CE attend le format `ACE-{N}-{refEtude}` avec un seul chiffre entre les deux premiers tirets. Si le format est différent (ex : `ACE-1B-225001`), le script tombe dans le fallback et affiche simplement `(modifiée par {valeur brute de C4})`.

## 7. Modifier ou étendre le script

### Changer le template Google Docs

Modifier la constante `idTemplate` en haut de `Code.gs`. Tester ensuite avec une étude de test pour vérifier que toutes les variables sont bien remplacées.

### Ajouter une variable dans la facture

1. Ajouter le marqueur `{{MaVariable}}` dans le template Google Docs.
2. Ajouter la clé/valeur correspondante dans l'objet `variables` de la fonction `remplacerVariables`.
3. Si la donnée vient de l'onglet `Phases`, l'ajouter dans `getInformationsEtude` et dans la cellule correspondante du sheet.
