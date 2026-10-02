# Conférence Ensimag

Slides [reveal.js](https://revealjs.com/) générées à partir de `slides.md` avec [reveal-md](https://github.com/webpro/reveal-md). Style dans `style.css`.

## Installation

Il faut [Node.js](https://nodejs.org/). Rien d'autre à installer : `npx` télécharge reveal-md au premier lancement.

## Lancer les slides

```bash
npx reveal-md slides.md -w
```

Les slides s'ouvrent dans le navigateur et se rechargent à chaque modification de `slides.md`.

## Générer le HTML

```bash
npx reveal-md slides.md --static dist
```

Le site statique est écrit dans `dist/`.
