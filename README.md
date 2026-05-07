# SRE Sales Guides — Argumentaires Joseph V2

Repo dédié aux fiches argumentaires commerciales par super-produit SRE,
maintenues par Joseph V2 chef de produit catalogue (cf.
[NicolasPycik/joseph](https://github.com/NicolasPycik/joseph) — `joseph/catalog/`).

## Structure

```
argumentaires/
  SP-001.md
  SP-002.md
  ...
  SP-XXX.md   ← un fichier par super-produit actif (~41 SP au 2026-05-07)
```

## Gabarit (8 sections — doctrine Bloc 10 Martine V4)

Chaque fiche suit le même squelette Markdown, parsable par
`src/martine_v4/tools/joseph_argumentaire.py:_parse_argumentaire_md`.

Gabarit :
- `# Nom complet du super-produit` (titre H1)
- `## Caractéristiques`
- `## Usages catalogues`
- `## Mode de pose`
- `## Accessoires de pose`
- `## Argumentaire client` avec 4 sous-sections H3 :
  - `### Esthétique` (vecteur design)
  - `### Durabilité` (vecteur longévité)
  - `### TCO` (vecteur coût total ownership)
  - `### Écologie` (vecteur environnement)
- `## Contre-indications`
- `## Alternatives`
- `## FAQ`
- Footer : `> Fiche version: X.Y.Z` + `> Source: ...`

## Workflow

1. Joseph V2 drafte via `POST /api/v1/catalog/draft_argumentaire_md`
2. Validation Telegram par 1 des 4 validators (nicolas/fabrice/francois/stefan)
3. Approve → `joseph/catalog/writer.py:write_argumentaire_md` :
   - Render MD via `tools.render_argumentaire_md`
   - Écrit `argumentaires/SP-XXX.md` localement
   - `git add + commit + push origin main`
4. Martine V4 consomme via `consulter_argumentaire(sp_id, vecteur)` qui parse le MD

## Lecteurs

- **Martine V4** : tool `consulter_argumentaire(sp_id, vecteur)` —
  `src/martine_v4/tools/joseph_argumentaire.py`. Parser tolérant au gabarit.
- **Site LBM V3** (V2) : potentiel rendu fiches produit côté client.
- **Sales-guide PDF generator** (V2) : compilation PDF par dépôt commercial.

## Versionning

- Chaque fiche a son propre `fiche_version` (SemVer dans le footer)
- Historique git complet — révisions traçables
- Joseph V2 incrémente la version à chaque révision validée

## Licence

Propriété SRE / Le Bois Malin. Usage interne uniquement.
