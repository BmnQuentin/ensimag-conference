---
title: Neutralité et algorithmes
theme: black
css: style.css
revealOptions:
  width: 1280
  height: 720
  transition: slide

---

# Pour commencer

Vous êtes data scientist à la CNAF : 
- 13.8 millions de foyers allocataires
- ~700 contrôleurs

<p class="fragment"><strong>Votre mission</strong> : déterminer quels dossiers contrôler pour récupérer le plus d'argent versé à tort</p>

---

## Choisissez 5 variables

| | |
|---|---|
| Niveau de revenus | Code postal |
| Variabilité des revenus | Nationalité |
| Situation familiale | Âge |
| Type d'allocation | Ancienneté du dossier |
| Changements de situation déclarés | Situation professionnelle |

---

# Neutralité et algorithmes

Élise & Quentin

---

## Ce modèle existe vraiment

Donne à chaque foyer un score recalculé chaque mois.

10 variables retenues parmi 1000 informations

Ce qui fait monter le score (versions 2010-2018) :

- faibles revenus, chômage, RSA <!-- .element: class="fragment" -->
- handicap (AAH), surtout avec un emploi <!-- .element: class="fragment" -->
- parent isolé <!-- .element: class="fragment" -->
- quartier défavorisé <!-- .element: class="fragment" -->

<small>Sources : La Quadrature du Net (2023), Le Monde (2023), Amnesty (2024)</small>

---

## Fraude ou erreur ?

Le modèle prédit les **trop-perçus**, pas la fraude

On se trompe là où les règles sont compliquées <!-- .element: class="fragment" -->

Le score mesure la complexité des règles, pas la malhonnêteté <!-- .element: class="fragment" -->

---

## Où ça casse ?

Des causes potentiellement multiples

| Dans les données | Dans le modèle | Dans l'usage |
|---|---|---|
| La reproduction du passé | Correlation <> causation | La prophétie auto-réalisatrice |
| Le dataset d'entrainement | La loi de Goodhart | La boîte noire |
| Les survivants | | |

Sept exemples, de 1935 à aujourd'hui

---

## 1935 : redlining

<!-- .slide: class="img-right" -->

![Carte de redlining (HOLC)](pictures/redlining.jpg)

La prophétie auto-réalisatrice <!-- .element: class="tag" -->

239 villes américaines notées de A à D

Pas de prêt -> pas d'investissement -> le quartier se dégrade -> la carte "avait raison" <!-- .element: class="fragment" -->

<small>Source : Mapping Inequality, Université de Richmond</small>

---

## Années 1970 : crash-tests

Le dataset d'entrainement <!-- .element: class="tag" -->

Mannequin de référence = l'homme "moyen"

Conductrices : risque de blessure grave +47% <!-- .element: class="fragment" -->

Biais dans l'échantillon statistique, avec lien sur le modèle physique. Se retrouve encore par exemple dans la pharmacologie. <!-- .element: class="fragment" -->

<small>Source : Bose et al., American Journal of Public Health, 2011</small>

---

## 1979 : St George's, Londres

La reproduction du passé <!-- .element: class="tag" -->

Programme designé pour imiter jury d'admission : jusqu'à 95 % de corrélation. Peut-on en déduire que c'étais satisfaisant ?

L'algo pénalise les femmes et les noms non européens, comme le jury <!-- .element: class="fragment" -->

Jusqu'à 60 candidats écartés par an <!-- .element: class="fragment" -->

> "The prejudice of a computer is no less than that of its designers" <!-- .element: class="fragment" -->

<small>Source : Lowry & Macpherson, BMJ, 1988</small>

---

## 2016 : APB

La boîte noire <!-- .element: class="tag" -->

Mars : association de lycéens demande le code source

<p class="fragment">Octobre : après des mois de bataille judiciaire, le code est envoyé imprimé par la poste, sur papier : cas de <em>malicious compliance</em></p>

Pas d'audit, pas de biais détectable <!-- .element: class="fragment" -->

<small>Sources : Next, L'Etudiant EducPros, 2016</small>

---

## 2018 : Amazon et les CV

Le dataset d'entrainement <!-- .element: class="tag" -->

Outil de tri entraîné sur 10 ans de CV reçus, surtout masculins

Le genre n'est pas une variable... <!-- .element: class="fragment" -->

...mais le mot "women" dans un CV fait baisser la note <!-- .element: class="fragment" -->

<small>Sources : Reuters, Numerama, 2018</small>

---

## 2020 : A-levels

<!-- .slide: class="img-right" -->

![Manifestation contre l'algorithme d'Ofqual, Londres, août 2020](pictures/fuck-algorithms.jpg)

Correlation <> causation <!-- .element: class="tag" -->

Covid : examens annulés et notes ajustées selon l'historique du lycée

Objectif du modèle : éviter l'inflation des notes

39,1 % des notes abaissées, très majoritairement dans les milieux défavorisés <!-- .element: class="fragment" -->

Héritage in-code des notes des prédécesseurs. <!-- .element: class="fragment" -->

<p class="fragment"><em>Fuck the algorithm</em> -> retrait en 4 jours</p>

<small>Sources : Ofqual, HEPI, 2020</small>

---

## En résumé

| | Mécanisme | Exemple |
|---|---|---|
| Données | La reproduction du passé | St George's |
| Données | Le dataset d'entrainement | Crash-tests, Amazon |
| Données | Les survivants | en fin de séance |
| Modèle | Correlation <> causation | A-levels |
| Modèle | La loi de Goodhart | en fin de séance |
| Usage | La prophétie auto-réalisatrice | Redlining |
| Usage | La boîte noire | APB |

---

## Et la CAF ?

Elle en cumule cinq sur sept

- reproduction du passé : apprise sur les contrôles passés <!-- .element: class="fragment" -->
- correlation <> causation : précarité et erreurs <!-- .element: class="fragment" -->
- loi de Goodhart : l'indicateur, c'est l'argent récupéré <!-- .element: class="fragment" -->
- prophétie auto-réalisatrice : plus de contrôles, plus d'indus trouvés <!-- .element: class="fragment" -->
- boîte noire : code inaccessible jusqu'en 2023 <!-- .element: class="fragment" -->

---

## Nos expériences

---

### Élise


---

### Quentin


---

## Atelier

À voir ensemble je suis pas super sûr

---

## Débat mouvant

D'accord : à gauche

Pas d'accord : à droite

---

### Affirmation 1

Je suis personnellement responsable si le travail qu'on me demande a un fort risque de biais discriminatoires.

---

### Affirmation 2

Les algorithmes utilisés dans des domaines critiques (santé, justice, finance) doivent être open source pour permettre leur audit.

---

### Affirmation 3

...

---

# Et pour finir

---

## Quelques caveats pour votre métier

- Les données **que vous n'avez pas** sont importantes <!-- .element: class="fragment" -->
- L'indicateur qu'on vous **demande d'optimiser** n'a plus d'intérêt <!-- .element: class="fragment" -->
- **Trop beau** pour être vrai ? Sans doute <!-- .element: class="fragment" -->

---

## 1943 : les avions qui reviennent

![Schéma du biais du survivant : impacts relevés sur les avions revenus](pictures/survivor-bias.webp)

<small>Abraham Wald, Statistical Research Group, 1943</small>

---

## 1902 : les rats de Hanoï

![Estampe vietnamienne représentant des rats](pictures/hanoi-rats.jpg)

> Quand une mesure devient une cible, elle cesse d'être une bonne mesure <!-- .element: class="fragment" -->

<small>Loi de Goodhart, 1975</small>

---

## Spurious correlations

![Exemple de corrélation fallacieuse (Tyler Vigen)](pictures/spurious-correlation.svg)

Avec assez de variables, on trouve toujours une corrélation <!-- .element: class="fragment" -->

<small>Tyler Vigen - Spurious correlations</small>

---

## Et par rapport à l'algo de la CNAF

Qu'est-ce que vous changeriez ?

---

## Et par rapport à l'algo de la CNAF

Qu'est-ce que vous changeriez ?

Pas de réponse générale hélas mais quelques pistes : 
- Requestionner le besoin <!-- .element: class="fragment" -->
- Traiter la cause <!-- .element: class="fragment" -->
- Encadrer le modèle de ciblage (si le besoin reste avéré) <!-- .element: class="fragment" -->

---

## Quelques questions à vous poser

1. Sur quelles données du passé est entraîné mon algo ? <!-- .element: class="fragment" -->
2. Qui est absent des données ? <!-- .element: class="fragment" -->
3. Quel critère j'optimise, et qui l'a choisi ? <!-- .element: class="fragment" -->
4. D'où vient la demande, est-ce que je permets aux parties prenantes de contester / auditer ? <!-- .element: class="fragment" -->
5. Est-ce que j'ai un regard statistique et citoyen, produit, et pas juste "belle techno" ? <!-- .element: class="fragment" -->

---

## Où et comment agir

Dans des assos : 
- Data for Good
- La Quadrature du Net
- The Shift Project

Mais surtout en faisant bien votre métier <!-- .element: class="fragment" -->
Et en doutant <!-- .element: class="fragment" -->

---

# Merci, des questions ?
