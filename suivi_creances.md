# Suivi des créances et procédure de relance

## Vue d'ensemble

Une créance est une somme due à Telecom Etude par un tiers (client d'étude ou partenaire) suite à l'émission d'une facture. Le trésorier est seul responsable du suivi des créances : c'est lui qui pilote les relances, pas le chef de projet. Ne pas attendre qu'on lui signale un retard.

Le délai de référence est **J = date d'échéance de la facture** (pas la date d'émission).

**Interlocuteurs impliqués**

- Trésorier : surveille les créances, déclenche et coordonne les relances
- Chef de projet (CdP) : effectue la relance douce à l'échéance pour les créances clients
- Responsable partenariat : effectue les deux premières relances pour les créances partenaires
- Président : cosigne les lettres amiables recommandées à partir de J+30 (clients) ou J+60 (partenaires)
- CNJE : à contacter pour la mise en demeure

**Outils utilisés**

- TS (Google Sheets) : onglet `Factures ventes`, qui calcule automatiquement le nombre de jours depuis l'émission et depuis l'échéance

> Logigramme : [logigramme_suivi_creances.md](logigrammes/logigramme_suivi_creances.md)

## Suivi quotidien des créances

L'onglet `Factures ventes` du TS centralise toutes les factures émises. Pour chaque facture non encore encaissée, le TS calcule automatiquement le nombre de jours écoulés depuis l'émission et depuis l'échéance.

**Consulter régulièrement cet onglet** pour détecter les factures qui approchent ou dépassent leur date d'échéance et déclencher les relances dans les délais.

Lorsqu'un paiement est reçu : noter la date du virement dans le TS et **notifier le CdP ou le responsable partenariat** concerné.

## Procédure de relance clients (études)

| Etape | Délai | Qui | Moyen |
|---|---|---|---|
| Relance douce | J | CdP | Téléphone, mail, courrier |
| Relance répétée | J+15 | Trésorier | Téléphone, mail, courrier |
| Lettre amiable recommandée | J+30 | Trésorier + Président | Courrier recommandé avec AR à conserver |
| Mise en demeure | J+45 | Trésorier | Contacter la CNJE |

> Pour une facture destinée à l'État : ne pas décompter en jours. Attendre la fin de procédure sur Chorus Pro.

### Détail des étapes

**J - Relance douce (CdP)**

À l'échéance, le CdP prend contact avec le client pour lui rappeler le règlement attendu. Le trésorier surveille que cette relance a bien lieu et peut relancer le CdP si nécessaire.

**J+15 - Relance répétée (Trésorier)**

Le trésorier prend le relais directement auprès du client. Le ton reste cordial mais la relance est plus ferme. Mentionner le numéro de facture, le montant et la date d'échéance dépassée.

**J+30 - Lettre amiable recommandée (Trésorier + Président)**

Envoi d'un courrier recommandé avec accusé de réception, signé par le trésorier et le président. **Conserver l'accusé de réception** : il constitue une preuve en cas de contentieux ultérieur.

**J+45 - Mise en demeure (Trésorier)**

Contacter le pôle Conseil de la CNJE pour obtenir un accompagnement sur la procédure de mise en demeure. Ne pas improviser à cette étape.

## Procédure de relance partenaires (subventions)

| Etape | Délai | Qui | Moyen |
|---|---|---|---|
| Relance douce | J | Responsable partenariat | Téléphone, mail, courrier |
| Relance répétée | J+30 | Responsable partenariat | Téléphone, mail, courrier |
| Lettre amiable recommandée | J+60 | Trésorier + Président | Courrier recommandé avec AR à conserver |
| Mise en demeure | J+90 | Trésorier | Contacter la CNJE |

Les deux premières relances sont portées par le **responsable partenariat**, qui entretient la relation commerciale. Le trésorier entre en jeu à partir de J+60. La logique est la même qu'avec les clients : escalade progressive, lettre recommandée avec AR, puis CNJE.

## Points d'attention et pièges fréquents

- **C'est le trésorier qui pilote, pas le CdP.** Le CdP effectue la relance douce à J, mais c'est le trésorier qui surveille le calendrier et déclenche les étapes suivantes si nécessaire. Ne pas attendre un signal externe.
- **Conserver tous les accusés de réception** des lettres recommandées. Ils sont indispensables en cas de contentieux.
- **Ne pas dépasser J+45 sans contacter la CNJE** pour les clients. Au-delà, la procédure devient juridique et Telecom Etude ne doit pas l'engager seule.
- **Mentionner le bon délai de paiement selon le type de facture** : 30 jours pour les clients d'études, 60 jours pour les partenaires. Les délais de relance sont calculés par rapport à l'échéance réelle.
- **Présenter les créances en cours en CA** pour informer les membres. 
