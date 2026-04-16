# Emission des bulletins de versement (BV)

## Vue d'ensemble

Le bulletin de versement est le document qui formalise la rétribution d'un intervenant (étudiant réalisant une étude). Il est l'équivalent d'une fiche de paie dans le cadre du statut JE. Son émission conditionne le versement de la rétribution nette à l'intervenant et le calcul des charges sociales dues à l'URSSAF.

Le BV est émis **après encaissement du paiement client**, pas à l'émission de la facture de solde. C'est la réception du virement client qui déclenche la procédure.

> Document RGPD : le BV ne doit être transmis qu'à l'intervenant concerné, pas au chef de projet ni à d'autres membres.

**Interlocuteurs impliqués**

- Trésorier : vérifie le dossier, contacte l'intervenant, émet le BV, réalise le virement
- Intervenant : fournit son IBAN, remplit le questionnaire de satisfaction
- Vice trésorier⸱e (VT) : contrôle, comptabilisation et archivage
- Président : réalise le virement si le trésorier est lui-même intervenant (voir cas particulier)

**Outils utilisés**

- TS (Google Sheets) : onglet `BV & RM`, modèle de BV auto-complété depuis le TS
- Interface bancaire : virement de la rétribution nette
- Template Google Docs de BV : s'auto-complète depuis le TS
- Questionnaire de satisfaction intervenant : Google Form

## Nomenclature

```
BV-XXX-22YYYY-N
```

- `XXX` : numérotation incrémentée depuis le **1er janvier** (repart à 001 chaque année civile, contrairement aux factures et NDF qui repartent au 1er mai)
- `22YYYY` : numéro d'étude
- `N` : N-ième BV de l'étude

**Exemple :** `BV-007-250012-1` pour le premier BV de l'étude 250012, septième BV émis depuis le 1er janvier.

## Conditions d'émission

Les trois conditions suivantes doivent être réunies simultanément avant d'émettre un BV :

1. **Signature du PVRF** : le procès-verbal de réception finale est signé par toutes les parties
2. **Dossier intervenant complet et valide** (voir détail ci-dessous)
3. **Encaissement du paiement client** : le virement du client est bien reçu sur le compte TE

> Pour les factures intermédiaires (PVRI), il est possible de rétribuer les JEH correspondant aux phases validées et payées. Les conditions sont identiques : PVRI signé + dossier complet + paiement reçu.

## Dossier intervenant : pièces à vérifier

Avant d'émettre le BV, vérifier la présence et la validité de chaque document dans le dossier de l'intervenant :

| Document | Points de contrôle |
|---|---|
| RM (Récapitulatif de Mission) | Signé par toutes les parties, cohérent avec le nombre de JEH et la rétribution |
| Avenants au RM | Tous présents et signés si des modifications ont eu lieu |
| CNI / Passeport / Titre de séjour | En cours de validité |
| Carte étudiante | En cours de validité |
| Carte vitale | Présente |
| BA (Bulletin d'adhésion) | Présent et signé |

Si un document est manquant ou expiré, contacter l'intervenant (ou le Secrétaire Général) pour le régulariser avant d'aller plus loin.

## Procédure pas à pas

### Etape 1 - Détecter l'encaissement client

Lors de la consultation quotidienne ou hebdomadaire du compte bancaire, constater qu'un virement client a été reçu. Identifier l'étude concernée en croisant avec l'onglet `Factures ventes` du TS.

### Etape 2 - Vérifier le dossier intervenant

Ouvrir le dossier de l'intervenant dans le Drive et vérifier la présence et la validité de toutes les pièces listées ci-dessus. Si tout est en ordre, passer à l'étape suivante. Sinon, contacter l'intervenant pour compléter le dossier.

### Etape 3 - Contacter l'intervenant

Envoyer un mail à l'intervenant pour lui demander :

- Son **IBAN** (si pas encore renseigné dans le dossier)
- De remplir le **questionnaire de satisfaction intervenant** (QS) : fourni par le VPO.

Il n'existe pas de processus automatisé pour cette demande : c'est un mail simple depuis `tresorier@telecom-etude.fr`.

### Etape 4 - Compléter le TS

Dans l'onglet `BV & RM` du TS, compléter les informations du BV à émettre.
- Numéro de BV (nomenclature)
- Référence de l'étude
- Date de l'émission du BV
- Nombre de JEH (à vérifier avec le RM et le PVRI/PVRF)
- Montant brut de la rétribution (à vérifier avec le RM)
- Nom et prénom de l'intervenant : à ajouter dans l'onglet `Intervenants` si nouveau en complétant toutes les informations nécessaires
   - nom
   - prénom
   - numéro de sécurité sociale
   - adresse fiscale
   - commune de naissance
   - date de naissance
   - IBAN
   - pays de naissance
   - nationalité
- Numéro RM (nomenclature)
- Référence du dernier avenant au RM si applicable (nomenclature)
- Mission : nom de la mission tel qu'indiqué sur le RM
- **Vérifier le taux AT** (lettre CARSAT) et **la base URSSAF** (4 * SMIC horaire brut au 1e janvier de l'année) : normalement correctement dans l'onglet `Paramétrage`

### Etape 5 - Identifier la procédure de surveillance des signataires

Le BV lui-même n'est pas signé. En revanche, le **virement** suit la procédure de surveillance des signataires si le trésorier est intervenant :

| Situation | Qui réalise le virement |
|---|---|
| Intervenant classique | Le trésorier |
| Le trésorier est intervenant | Le **président** réalise le virement. Le **VT** émet le BV à la place du trésorier. |
| Le président est intervenant | Le trésorier réalise le virement normalement |

### Etape 6 - Virer la rétribution nette

Effectuer le virement du montant **net** à l'IBAN de l'intervenant depuis l'interface bancaire. Conserver la référence du virement : elle doit figurer dans le BV.

> Payer d'abord, envoyer le BV ensuite.

### Etape 7 - Finir de compléter le TS

Après le virement, compléter les informations restantes dans le TS :
- Date du virement
- Référence du virement

### Etape 8 - Editer le BV

Le modèle de BV est un **Google Sheet** qui s'auto-complète depuis le TS si les informations de l'intervenant ont bien été renseignées.

> Le modèle de BV est dans le Drive Trésorerie > Template GDocs > BV_type_Janvier 2026. 

> La CNJE fournit un nouveau modèle de BV chaque année, avec les taux de cotisations à jour. Ne pas réutiliser un ancien modèle.

> Bien mettre à jour le lien du modèle de BV dans l'onglet `Paramétrage` > `ID BV Template` du TS à chaque nouvelle version.

Pour générer le BV :
1. Dans l'onglet `BV & RM` du TS, cocher la case `Générer BV` de la ligne du BV concerné
2. Cliquer sur le bouton `Générer BV`
3. Un nouveau fichier Google Sheet de BV est créé dans le dossier (celui défini dans l'onglet `Paramétrage` > `Dossier destination`)
4. Ouvrir le BV généré, vérifier que toutes les informations sont correctement reportées et que les calculs sont justes
5. Cacher la colonne `Part Junior` > `TAUX`
6. Exporter le BV au format PDF pour l'envoi à l'intervenant

### Etape 7 - Envoyer le BV et le tuto BNC

Envoyer à l'intervenant **uniquement** (document RGPD) :

- Le BV en PDF
- Le tutoriel de déclaration en BNC fourni par la CNJE (à récupérer sur Kiwi Légal)

### Etape 8 - Transmission au VT

Le VT contrôle, comptabilise et archive le BV. Le déposer dans le Drive Trésorerie > BV > Mandat 202X-202Y.

Le VT le range ensuite dans le dossier du mois d'émission.

## Points d'attention et pièges fréquents

- **Ne jamais émettre un BV avant l'encaissement client.** Même si le PVRF est signé depuis longtemps, le BV attend le virement. C'est une règle absolue pour garantir la trésorerie de l'association.
- **Vérifier le dossier complet avant de contacter l'intervenant.** Inutile de demander l'IBAN si la carte étudiante est expirée : autant identifier tous les blocages d'un coup.
- **Le BV est un document RGPD.** Ne jamais le transmettre à quelqu'un d'autre que l'intervenant, même au chef de projet.
- **La numérotation XXX repart au 1er janvier**, pas au 1er mai comme les factures. Ne pas mélanger les deux conventions.
- **Les charges sociales ne sont pas virées à l'intervenant** : elles sont calculées dans le TS et payées à l'URSSAF via la déclaration BRC mensuelle. La rétribution versée à l'intervenant est le montant **net**.
- **Si le trésorier est intervenant** : ne pas gérer son propre BV. Passer la main au VT pour l'émission et au président pour le virement.
