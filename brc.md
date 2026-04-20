# Déclaration du BRC (Bordereau Récapitulatif des Cotisations)

## Vue d'ensemble

Le BRC est la déclaration mensuelle des charges sociales dues à l'URSSAF au titre des rétributions versées aux intervenants via les BV. Il permet de déclarer et payer les cotisations calculées lors de l'émission des BV du mois précédent.

- **Fréquence** : mensuelle
- **Échéance** : avant le **15 du mois suivant** la période concernée (ex : BRC de mars à déposer avant le 15 avril)
- **Où** : sur le site URSSAF (urssaf.fr)
- **Paiement** : prélèvement automatique après validation de la déclaration

Si aucun BV n'a été émis sur le mois, **une déclaration à zéro** doit quand même être soumise.

**Interlocuteurs impliqués**

- Trésorier : génération via AppScript, vérification, déclaration sur le site URSSAF
- VT : double contrôle avec la comptabilité (comptes 6226 et 431)

**Outils utilisés**

- TS (Google Sheets) : onglet `BV & RM` (source des données) et onglet `Déclaratifs mensuels` (suivi)
- AppScript du TS : génération automatique du sheet BRC pré-rempli
- Drive Trésorerie > Déclaratifs > BRC + TR > Mandat 202X-202Y > AAAA-MM : archivage
- Site URSSAF : dépôt de la déclaration

> Logigramme : [logigramme_brc.md](logigrammes/logigramme_brc.md)

## Procédure pas à pas

### Etape 1 - Générer le sheet BRC via l'AppScript

Dans le TS, lancer l'AppScript dédié au BRC (menu Déclaratif > Générer BRC pour un mois)

> Il lit automatiquement l'onglet `BV & RM` et génère un sheet pré-rempli avec les données du mois : assiette de cotisations, effectifs, rétributions brutes.

Le sheet généré est automatiquement :
- Stocké dans Drive Trésorerie > Déclaratifs > BRC + TR
- Lié dans la colonne `Fichier BRC` de l'onglet `Déclaratifs mensuels` du TS

**Action à faire manuellement** : déplacer le fichier généré dans le bon sous-dossier Drive Trésorerie > Déclaratifs > BRC + TR > Mandat 202X-202Y > AAAA-MM.

### Etape 2 - Vérifier le sheet généré

Avant de reporter les chiffres sur le site URSSAF, contrôler le sheet :

- **La base URSSAF est-elle à jour** pour l'année en cours ?
- **Le taux AT (Accident du Travail)** est-il correct ? Il est consultable sur la lettre CARSAT ou sur le site URSSAF / net-entreprise.fr. Il change tous les 1er janvier
- **L'assiette de cotisations** = Base URSSAF × total des JEH du mois (croiser avec l'onglet `BV & RM`)
- **Les effectifs** sont-ils cohérents avec les BV émis sur le mois ?
- **Les salaires arrondis** correspondent-ils à la somme des assiettes de cotisations des BV du mois ?
- **Les lignes inutiles** sont-elles bien absentes ou à zéro ?

Double contrôle avec le VT : croiser les montants avec les comptes comptables **6226** (rétributions brutes) et **431** (dettes URSSAF).

### Etape 3 - Déclarer sur le site URSSAF

Se connecter sur urssaf.fr avec les identifiants de la structure (voir les accès trésorerie).

Retranscrire case par case les chiffres du sheet généré dans le formulaire en ligne :

- Remplir "Effectif au dernier jour de la période"
- Remplir "Effectif rémunéré pour la période"
- Laisser "Effectifs" à 0
-  Remplir "Salaires arrondis" avec la somme des assiettes de cotisations des BV du mois

> Les montants sont **toujours arrondis à l'unité** (jamais de centimes).

Valider la déclaration. Le paiement est déclenché automatiquement par prélèvement SEPA sur le compte BNP de Telecom Etude.

### Etape 4 - Archiver la déclaration BRC

- Télécharger le récapitulatif de la déclaration au format PDF depuis le site URSSAF
- Le déposer dans le Drive Trésorerie > Déclaratifs > BRC + TR > Mandat 202X-202Y > AAAA-MM
- Le nommer selon la nomenclature suivante :

```
BRC-AAAA-MM
```

> Demander au VT de déposer une copie du grand livre du compte 431 (dettes URSSAF) du mois concerné dans le même dossier. 

### Etape 5 - Mettre à jour le TS

Dans l'onglet `Déclaratifs mensuels`, compléter la colonne `Date déclaration BRC` pour le mois concerné.

## Les bases du calcul

### Assiette de cotisations

Le calcul des cotisations ne se base pas sur les rétributions brutes, mais sur une **assiette dérogatoire** propre aux Junior-Entreprises :

```
Assiette de cotisations = Base URSSAF × nombre de JEH de la période
```

La **Base URSSAF** correspond à 4 fois le SMIC horaire au 1er janvier de l'année en cours :
- 2025 : 4 × 11,88 € = **47,52 €**
- 2026 : 4 × 12,02 € = **48,08 €**

> La Base URSSAF est à vérifier chaque 1er janvier lors du changement de SMIC. Une mauvaise base fausse tous les calculs de l'année.

### Effectifs à déclarer

| Champ | Ce qu'il faut renseigner |
|---|---|
| Effectif au dernier jour de la période | 0 si aucun BV sur le mois, 1 sinon (quel que soit le nombre d'intervenants) |
| Effectif rétribué pour la période | Nombre d'intervenants **différents** ayant reçu au moins un BV sur le mois |
| Colonne "Effectifs" | Toujours **0** : nos intervenants ne sont pas des salariés |

### Lignes à supprimer ou ignorer

Certaines lignes apparaissent parfois dans le déclaratif URSSAF mais ne s'appliquent plus aux JE :

| Ligne | Raison |
|---|---|
| 900T - Versement Transport | Supprimé pour les JE depuis le 01/01/2016 |
| 236D - FNAL supplémentaire | Supprimé pour les JE depuis 2015 |
| 772D - Assurance chômage | Supprimé pour les JE depuis le 01/03/2023 (loi n°2022-1616) |
| 937D - AGS | Idem |
| 400D - CICE | Disparu en 2019 |
| 671P - Réduction Générale Base Plafonnée | Taux à 100 % pour les JE : à supprimer |

> Il faut veiller à **supprimer ces lignes** lors de la déclaration. 

## En cas d'erreur sur un BRC passé

Un BRC déjà soumis ne se corrige pas. La marche à suivre dépend de la nature de l'erreur (effectif ou montant) : voir la fiche dédiée [brc_rectification.md](brc_rectification.md).

## Points d'attention et pièges fréquents

- **Respecter l'échéance du 15 du mois.** Un retard de déclaration peut entraîner des pénalités URSSAF.
- **Vérifier la Base URSSAF chaque 1er janvier.** Elle change avec le SMIC. Si elle n'est pas mise à jour, tous les BV et BRC de l'année seront faux.
- **Même sans BV sur le mois, la déclaration est obligatoire** (déclaration à zéro).
- **Arrondir à l'unité**, jamais de centimes dans un BRC.
- **Un intervenant avec plusieurs BV sur le même mois ne compte que pour 1** dans l'effectif rétribué.
- **Ne pas toucher aux lignes 772D et 937D** (chômage/AGS) : elles ne s'appliquent pas aux JE.
- **Conserver le sheet BRC et les déclaratifs archivés** : ils servent de référence pour le TR en fin d'année civile.
- **En cas d'erreur sur un BRC déjà soumis** : suivre la procédure de rectification dédiée — [brc_rectification.md](brc_rectification.md).
