# Signature de l'État de Rapprochement Bancaire (ERB)

## Vue d'ensemble

L'État de Rapprochement Bancaire (ERB) est un document mensuel qui prouve que la comptabilité tenue dans Cegid Loop est en parfait accord avec le relevé bancaire BNP. C'est une pièce de contrôle interne fondamentale : si l'écart de rapprochement est à zéro, cela signifie qu'aucune opération n'a été oubliée ou mal saisie en comptabilité.

C'est le **VT qui produit l'ERB** depuis Loop à partir du relevé bancaire du mois. Le **trésorier vérifie et cosigne** en tant que contrôleur.

**Interlocuteurs impliqués**

- Vice trésorier⸱e (VT) : produit l'ERB dans Cegid Loop, joint le relevé bancaire et le grand livre
- Trésorier : dépose l'ERB sur YouSign, vérifie l'ERB et cosigne
- Président : vérifie l'ERB et cosigne

**Outils utilisés**

- Cegid Loop : génération de l'ERB et du grand livre
- Relevé bancaire BNP : pièce de référence pour le rapprochement
- YouSign : signature électronique de l'ERB
- TS (Google Sheets) : onglet `Déclaratifs mensuels`, suivi de la validation mensuelle

> Logigramme : [logigramme_erb.md](logigrammes/logigramme_erb.md)

## Procédure pas à pas

### Etape 1 - Réception de l'ERB sur YouSign

Le VT produit l'ERB dans Loop en début de mois suivant, y joint le relevé bancaire et le grand livre, puis le trésorier dépose le tout sur YouSign pour signature.

### Etape 2 - Vérification

Effectuer les cinq contrôles décrits **ci-dessous**. Si tout est correct, passer à la signature. Si une anomalie est détectée, ne pas signer et contacter le VT.

### Etape 3 - Signature via YouSign

Signer l'ERB via YouSign. Le président cosigne de son côté.

### Etape 4 - Mise à jour du TS

Une fois l'ERB signé par le trésorier **ET** le président, compléter la colonne `Date signature ERB` dans l'onglet `Déclaratifs mensuels` du TS pour le mois concerné.

## Structure du document

L'ERB transmis par le VT se compose de trois parties :

**1. L'ERB proprement dit** (généré par Loop)

Il présente quatre lignes et un solde de contrôle :

| Ligne | Contenu |
|---|---|
| Relevé bancaire | Solde final du relevé BNP du mois |
| Solde en banque à rapprocher | Doit être identique au relevé bancaire |
| Solde en comptabilité | Solde du compte 51240000 dans Loop |
| Solde en comptabilité à rapprocher | Doit être identique au solde comptable |
| **Écart de rapprochement** | **Doit impérativement être 0,00** |

**2. Le relevé bancaire BNP** du mois concerné

Il liste toutes les opérations du mois : virements reçus, paiements par carte, virements émis, prélèvements.

**3. Le grand livre général du compte 51240000** (généré par Loop)

Il liste toutes les écritures comptables saisies en banque pour le même mois, avec pour chacune le libellé, le montant et le solde progressif.

## Procédure de vérification avant signature

### 1. Vérifier l'écart de rapprochement

C'est le premier et le plus important des contrôles. **L'écart de rapprochement doit être 0,00.** S'il ne l'est pas, il ne faut pas signer et demander au VT de corriger.

### 2. Vérifier la cohérence des soldes

- Le solde "Relevé bancaire" sur l'ERB doit correspondre exactement au **solde final du relevé BNP** du mois.
- Le solde en comptabilité doit être le même : les deux colonnes de l'ERB doivent afficher le même chiffre.

### 3. Croiser le relevé bancaire avec le grand livre

Passer en revue chaque opération du relevé BNP et vérifier qu'elle se retrouve bien dans le grand livre avec le bon montant et la bonne date. Quelques exemples de ce qu'on s'attend à voir :

- Un virement reçu `FAC-568-CRA25-251020` pour 249,60 € dans le relevé → la même référence et le même montant dans le grand livre
- Un prélèvement URSSAF de 90,00 € dans le relevé → une écriture `URSSAF Février 2026` de 90,00 € dans le grand livre
- Un paiement carte Mailchimp de 19,84 € dans le relevé → une écriture `ACH-143-260315-FAC Mailchimp` de 19,84 € dans le grand livre

Toute opération présente dans le relevé bancaire doit avoir son équivalent dans le grand livre, et vice versa.

### 4. Vérifier les libellés du grand livre

Les libellés des écritures dans le grand livre doivent respecter les nomenclatures en vigueur :
- Factures d'achat : `ACH-XXX-AAMMJJ-FAC Nom fournisseur`
- Factures de vente encaissées : référence `FAC-XXX-...`
- Déclarations : `URSSAF Mois Année`, `TVA Mois Année`

Un libellé vague ou absent est un signal d'alerte à remonter au VT.

### 5. Vérifier l'absence d'opérations anormales

Parcourir rapidement les opérations pour détecter tout mouvement inhabituel : montant très élevé, émetteur inconnu, libellé incompréhensible. En cas de doute, vérifier avec le VT avant de signer.

## Points d'attention et pièges fréquents

- **Ne jamais signer si l'écart n'est pas à zéro.** Un écart, même faible, signifie qu'une opération est manquante ou incorrecte en comptabilité. Ce n'est pas anodin.
- **L'ERB porte sur le mois N-1.** En avril, on signe l'ERB de mars. Ne pas confondre les périodes.
- **Bien vérifier les soldes de départ.** Le solde initial du grand livre pour le mois doit correspondre au solde final de l'ERB du mois précédent.
- **Le contrôle n'est pas une formalité.** En tant que cosignataire, le trésorier **engage sa responsabilité** sur la véracité du rapprochement. Prendre le temps de croiser les opérations.
