# land_100 - Guide rapide

## 1) Structure du projet

```text
.
|-- index.html
|-- landings.json
`-- 100/
    |-- 01-meowsocks/
    |   `-- index.html
    `-- 02-.../
        `-- index.html
```

## 2) Ajouter une nouvelle landing

1. Cree un dossier dans `100/` avec le format `NN-slug`.
2. Mets ton code dans `100/NN-slug/index.html`.
3. Ajoute une entree dans `landings.json`.

Exemple:

```json
{
  "id": 2,
  "name": "Neon Grid Hero",
  "desc": "Hero futuriste avec grille et glow",
  "category": "html-css",
  "level": 2,
  "folder": "02-neon-grid-hero",
  "thumbnail": "",
  "url": "",
  "tags": ["hero", "neon", "css"],
  "tech": ["HTML", "CSS"],
  "author": "Marwichmisi",
  "date": "2026-03-22",
  "url": ""
}
```

### URL directe (landing externe)

Si la landing n'est pas dans `100/`, mets l'URL finale dans `url`.

```json
"url": "https://ton-site.com/landing-x"
```

Si tu utilises `url`, le hub ouvre ce lien directement.

## 3) Categories autorisees

- `html-css`
- `animations`
- `js-interactions`
- `3d-webgl`
- `video`
- `shaders`

## 4) Niveaux

- `1` = debutant
- `2` = debutant+
- `3` = intermediaire
- `4` = avance
- `5` = insane

## 5) GitHub Pages (configuration)

1. Ouvre le repo: `https://github.com/Marwichmisi/land_100`
2. Va dans `Settings` -> `Pages`
3. `Source`: **Deploy from a branch**
4. `Branch`: **main** et dossier **/(root)**
5. Clique `Save`
6. Attends 1-2 minutes
7. URL du site: `https://marwichmisi.github.io/land_100/`

## 6) Deploy d'une mise a jour

```bash
git add .
git commit -m "add landing xx"
git push
```
