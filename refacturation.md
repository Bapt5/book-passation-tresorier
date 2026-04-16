# Refacturation

## Vue d'ensemble

La refacturation désigne les cas où Telecom Etude avance un paiement pour le compte d'un tiers (membres, client d'une étude) puis lui répercute ce coût via une facture. C'est une facture de vente hors étude : elle ne s'appuie pas sur une CE ou un PVR, mais sur un justificatif de la dépense avancée.

La TVA est le taux de la dépense avancé, se référer au justificatif. En général, il s'agit de dépenses avec TVA à 20 % (places de congrès, frais d'étude hors CE, etc.).

> Attention : un étudiant ou un particulier ne peut pas déduire cette TVA.

**C'est le trésorier qui détecte lui-même le besoin de refacturer**, en constatant une dépense engagée par Telecom Etude pour le compte d'un tiers. Il n'y a pas de déclencheur externe formalisé.

> La refacturation peut être prévu dans le budget. Par exemple, pour les places de congrès. Dans ce cas, la refacturation peut être partielle. 

**Interlocuteurs impliqués**

- Trésorier : détecte le besoin, émet la facture et met à jour le TS
- Vice trésorier⸱e (VT) : contrôle, comptabilisation et archivage
- Tiers facturé : destinataire de la facture (membre, client d'étude, autre JE...)

**Outils utilisés**

- TS (Google Sheets) : onglet `Factures ventes`
- Template Google Docs refacturation : Drive Trésorerie > Template GDocs > Template refacturation

## Cas typiques

**Places de congrès CNJE**
Telecom Etude avance le paiement des inscriptions au congrès pour ses membres. Elle refacture ensuite chaque membre (ou un groupe) du montant correspondant.

**Frais d'étude hors CE**
Certains frais engagés pour la réalisation d'une étude ne sont pas prévus dans le budget de la CE. Selon les conditions générales d'étude : *"Tous les frais non prévus dans le budget et engagés pour la réalisation des prestations sont à la charge du Client. Ils seront refacturés au réel sous réserve de validation préalable par le Client et présentation des justificatifs."* Ces frais sont refacturés au client de l'étude, séparément des factures d'étude habituelles.

## Nomenclature

```
FAC-XXX-NOM_PERSONNE_OU_ENTREPRISE
```
Pour une refacturation à un individu ou une entreprise identifiée.

- `XXX` : numérotation globale incrémentée depuis toujours (partagée avec toutes les autres factures)
- `NOM_PERSONNE_OU_ENTREPRISE` : nom court du destinataire

**Exemples :**
- `FAC-574-Martin` pour une refacturation individuelle à un membre dont le nom de famille est Martin

## Procédure pas à pas

### Etape 1 - Identifier le besoin de refacturer

Le trésorier constate qu'une dépense a été engagée par Telecom Etude pour le compte d'un tiers. Avant d'émettre la facture, vérifier :

- Que la dépense est bien justifiée et traçable (facture fournisseur, reçu, relevé bancaire)
- Dans le cas de frais d'étude hors CE : que la **validation préalable du client** a bien été obtenue et que les justificatifs sont disponibles
- L'identité exacte du destinataire et ses coordonnées de facturation

### Etape 2 - Editer la facture

1. Ouvrir le template Google Docs **refacturation** depuis Drive Trésorerie > Template GDocs
2. Dupliquer le template et le renommer selon la nomenclature
3. Compléter les informations :
   - Raison sociale / nom et adresse du destinataire
   - SIRET si le destinataire est une entreprise (à vérifier sur [annuaire-entreprises.data.gouv.fr](https://annuaire-entreprises.data.gouv.fr))
   - Numéro de facture
   - Date d'émission et date d'échéance
   - Objet de la refacturation : décrire précisément la dépense avancée et la référence du justificatif
   - Montant HT, TVA (selon le taux de la dépense avancée) et montant TTC

4. Vérifier les mentions légales obligatoires :
   - En-tête : raison sociale de Telecom Etude, SIRET, code APE, numéro de TVA intracommunautaire
   - Mention "TVA sur les encaissements"
   - Modalités de paiement (virement bancaire)
   - Conditions d'escompte pour paiement anticipé

5. Joindre les justificatifs de la dépense avancée à l'envoi (facture fournisseur, reçu...) si pertinent pour le destinataire

6. Exporter la facture au format PDF

La facture n'est pas signée.

### Etape 4 - Envoi au destinataire

Le trésorier envoie directement la facture au destinataire depuis `tresorier@telecom-etude.fr`.

### Etape 5 - Mise à jour du TS

Après émission, mettre à jour l'onglet `Factures ventes` du TS :

- Le numéro de facture
- Le destinataire (à ajouter dans l'onglet `Clients` si nouveau)
- Le type : `Refac Client` ou `Refac Etudiant`
- Le lien vers la facture dans le Drive
- La date d'émission et la date d'échéance
- Le montant HT
- La TVA à collecter **si le taux est différent de 20 %**

Suivre le paiement depuis cet onglet. Lorsque le virement est reçu, noter la date.

### Etape 6 - Contrôle par le VT

Comme pour toute facture de vente, le VT contrôle, comptabilise et archive la facture. La déposer dans le Drive Trésorerie > Ventes (Factures) > Mandat 202X-202Y. 

Le VT la range ensuite dans le dossier du mois d'émission.

## Points d'attention et pièges fréquents

- **La TVA est toujours à appliquer au taux de la dépense avancée**, même si c'est différent de 20 %. Simplement, si le destinataire est un particulier, il ne pourra pas déduire cette TVA.
- **Pour les frais d'étude hors CE** : ne jamais refacturer sans validation préalable écrite du client et sans justificatifs. La base légale est dans les conditions générales d'étude.
- **Toujours conserver les justificatifs** de la dépense avancée : en cas de contrôle ou de contestation, ils font foi.
- **Ne pas oublier de facturer** : certaines dépenses avancées peuvent passer sous le radar si le trésorier ne fait pas le lien avec la dépense sortante. Surveiller le budget pour détecter les dépenses avancées et éviter les oublis de refacturation.
