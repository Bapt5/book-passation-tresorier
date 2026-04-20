# Logigramme — Rectification d'un BRC

> Fiche associée : [brc_rectification.md](../brc_rectification.md)

```mermaid
flowchart TD
    classDef step fill:#c0392b,color:#fff,stroke:none
    classDef dec fill:#e67e22,color:#fff,stroke:none
    classDef se fill:#7b241c,color:#fff,stroke:none
    classDef ok fill:#27ae60,color:#fff,stroke:none
    classDef ref fill:#e8967a,color:#333,stroke:#c0502b

    START([Erreur détectée sur un BRC soumis]):::se

    DEC_TYPE{"Nature de l'erreur ?"}:::dec

    NOTHING["Aucune action requise\nL'effectif du TR annuel prime\nsur celui des BRC mensuels"]:::ok

    subgraph MONTANT["🗓 Erreur sur les montants"]
        direction TB
        M1["Documenter l'erreur immédiatement\nNature, montant concerné,\nmois du BRC erroné"]:::step
        M2["Signaler au VT\npour suivi comptable"]:::step
        M3["Ne pas corriger le BRC soumis\nNe pas soumettre un BRC rectificatif"]:::step
        M4["Régulariser lors du TR annuel\n📅 Avant le 31 janvier de l'année N+1"]:::step
        M1 --> M2 --> M3 --> M4
    end

    TR[["📎 Procédure TR et TR rectificatif\n→ Kiwi Légal CNJE"]]:::ref
    FIN([Erreur régularisée au TR]):::se

    START --> DEC_TYPE
    DEC_TYPE -->|Effectif| NOTHING
    DEC_TYPE -->|Montant / taux / assiette| MONTANT
    MONTANT --> TR --> FIN
    NOTHING --> FIN
```

## ⚠️ Points sensibles

- Ne pas tenter de corriger un BRC déjà soumis — il n'existe pas de BRC rectificatif, toute régularisation passe par le TR
- Documenter l'erreur immédiatement — plus le délai est long entre la détection et le TR, plus il est difficile de justifier l'écart auprès de l'URSSAF
- L'effectif du TR prime sur celui des BRC mensuels — une erreur d'effectif sur un BRC n'a pas besoin d'être régularisée

## ❓ Précisions

- Pour les procédures TR et TR rectificatif, consulter le [tutoriel CNJE sur Kiwi Légal](https://legal.junior-entreprises.com/knowledge-base/tableau-recapitulatif-tr/)
