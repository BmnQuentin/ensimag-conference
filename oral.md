# Notes pour l'oral

Ce qu'on dit, dans l'ordre des slides. Les sources sont dans `sources.md`, classées par titre. Les `[à compléter]` sont à remplir par Quentin et Elise.

## 0. Le piège (10 min)

### Consigne (2 min)

"Vous êtes data scientist à la CNAF. Chaque mois, 13,8 millions de foyers reçoivent une prestation. Vous avez environ 700 contrôleurs pour les contrôles sur place (chiffre de presse, à recouper). Votre mission : choisir les dossiers à contrôler pour récupérer le plus possible d'argent versé à tort."

Ne pas prononcer les mots biais, discrimination, éthique.

### En binômes (4 min)

Ils choisissent 5 variables parmi les 10 affichées. On note au tableau les plus citées.

A observer : presque tout le monde refuse la nationalité, beaucoup acceptent le code postal.

### Révélation (4 min)

- Le score existe depuis le début des années 2010. Il note chaque foyer entre 0 et 1, chaque mois : plus de 13 millions de scores, portant sur 32 millions de personnes.
- Quelques dizaines de variables, retenues après un apprentissage sur plus de 1 000 informations par allocataire.
- La Quadrature du Net a obtenu le code source des versions 2010-2018. Ce qui fait monter le score : faibles revenus, chômage, RSA, handicap (AAH, surtout avec un emploi), parent isolé (des femmes dans 80 % des cas), quartier défavorisé.
- L'exemple à détailler, l'AAH (allocation aux adultes handicapés) : sans emploi, l'allocataire déclare ses ressources une fois par an et son allocation est stable. Avec un emploi en milieu ordinaire, il passe à une déclaration tous les trois mois ("AAH trimestrialisée") et l'allocation est recalculée à chaque fois. Plus de déclarations et des revenus qui bougent, donc plus d'erreurs, donc plus de trop-perçus dans les données passées, donc un score élevé. La personne handicapée qui travaille est davantage contrôlée parce que sa règle est plus compliquée, pas parce qu'elle triche. (Détail du régime trimestriel à recouper ; l'AAH aurait été retirée du modèle 2026 d'après la presse, non confirmé par la page de la CAF.)
- Le point clé : le modèle ne prédit pas la fraude mais le risque d'indu, c'est-à-dire de trop-perçu, qui est le plus souvent une erreur. Or on se trompe là où les règles sont compliquées : minima sociaux, déclarations trimestrielles, revenus qui bougent. Le score mesure la complexité des règles imposées aux plus précaires, pas leur malhonnêteté.
- La réponse de la CAF, à donner honnêtement : l'algorithme ne cible "pas forcément les personnes les plus pauvres, mais celles dont les revenus varient" (N. Grivel, directeur de la CNAF). Et le datamining ne représente que 6,5 % des contrôles sur place ou sur pièces selon la CAF.
- Nationalité contre code postal : vous avez refusé l'une et pris l'autre, alors que le code postal porte en partie la même information. C'est ce qu'on appelle un proxy.

Ton : "vous avez fait ce que ferait tout bon ingénieur, et c'est bien le problème". Pas "vous vous êtes fait avoir".

Si certains ne tombent pas dedans : leur demander pourquoi, ils font l'argumentaire à notre place.

### Si on nous demande "c'était quoi, la bonne réponse ?"

Réponse courte, pour ne pas éventer la suite : "Il n'y a pas de bonne liste de variables. La bonne réponse commence par se demander ce qu'on prédit vraiment et ce qu'on fait du score. On construit ça ensemble jusqu'à la fin." La réponse complète est en conclusion.

## I. Ça ne date pas d'hier (15 min)

Transition : "Ce mécanisme n'a pas attendu le machine learning." Sept exemples, du plus ancien au plus récent, à filtrer selon le temps.

Fil rouge à énoncer une fois : un système de décision est calibré sur des données du passé, donc il reproduit les discriminations du passé, avec en prime un vernis de neutralité.

### La grille de lecture : trois endroits où ça casse

A annoncer avant les exemples (slide "Où ça casse ?"), puis à nommer explicitement à chaque exemple, avec les mêmes mots que sur les slides. Chaque exemple a un mécanisme principal ; la plupart en illustrent aussi un ou deux autres.

| Où | Mécanisme | En une phrase | Exemple principal | Aussi dans |
|---|---|---|---|---|
| Données | La reproduction du passé | le modèle apprend des décisions humaines, biais compris | St George's | Amazon, CAF |
| Données | Le dataset d'entraînement | ceux qui sont absents ou sous-représentés dans les données n'existent pas pour le modèle | Crash-tests, Amazon | Gender Shades |
| Données | Les survivants | on ne voit que ceux qui ont passé le filtre | avions de 1943 (caveats) | CAF |
| Modèle | Correlation <> causation | une variable "marche" pour prédire, on agit comme si elle décrivait la personne | A-levels | Amazon, CAF, redlining |
| Modèle | La loi de Goodhart | le modèle optimise très bien le critère qu'on lui donne, pas l'intention derrière | rats de Hanoï (caveats) | A-levels, CAF |
| Usage | La prophétie auto-réalisatrice | la décision fabrique les données qui la confirmeront | Redlining | CAF |
| Usage | La boîte noire | sans accès au code, rien de ce qui précède n'est détectable | APB | CAF avant 2023 |

Deux précisions utiles pour des matheux :

- Corrélation contre causalité : pour prédire, une corrélation suffit, et c'est pour ça que le modèle "marche". Le problème commence quand on décide : contrôler, refuser, noter quelqu'un, c'est traiter la corrélation comme une propriété de la personne. Prédire n'est pas décider.
- Aucun de ces mécanismes n'est une erreur de calcul. Et même en les corrigeant tous, il reste un choix de valeurs entre définitions de l'équité : c'est l'objet de l'atelier. Ne pas laisser croire qu'il "suffit de faire de la bonne stat".

### 1. Redlining, USA, années 1930 (origine / quartier)

Mécanisme : la prophétie auto-réalisatrice (usage). Aussi : correlation <> causation, le quartier servant de proxy de l'origine.

- 1935-1940 : l'agence fédérale HOLC fait cartographier 239 villes en 4 classes de risque de crédit, de A ("best") à D ("hazardous", en rouge). La composition raciale du quartier pèse lourd dans la note.
- La boucle : pas de prêt, donc pas d'investissement, donc le quartier se dégrade, donc la carte "avait raison". La prédiction fabrique ses propres données.
- Interdit en 1968 (Fair Housing Act), mais les effets restent dans les données. En 2016, la livraison Amazon Prime en un jour exclut des quartiers majoritairement noirs dans plusieurs villes, dont Roxbury à Boston, sans que l'origine soit une variable.
- Contrepoint cartographie radicale : W. Bunge et la Detroit Geographical Expedition (1968-71) font cartographier la ville par ses habitants. Qui choisit ce qu'on mesure choisit ce qu'on voit.

### 2. Mannequins de crash-test, années 1970 (sexe)

Mécanisme : le dataset d'entraînement (données).

- Les tests reposent historiquement sur un mannequin d'homme "moyen", mis au point dans les années 1970.
- Sur les accidents réels aux USA entre 1998 et 2008, une conductrice ceinturée a un odds de blessure grave supérieur de 47 % à celui d'un conducteur dans un accident comparable (IC 95 % : 28-70 %). Attention : c'est un rapport de cotes, pas "47 % de risque en plus".
- Parlant pour une filière modélisation / simulation : ici le "dataset", c'est le modèle physique lui-même.

### 3. St George's Hospital Medical School, Londres, 1979-1988 (sexe + origine)

Mécanisme : la reproduction du passé (données). C'est le cas le plus pur de biais humain intégré à l'algorithme.

- Un enseignant écrit un programme pour présélectionner les candidatures. En 1979, il reproduit les notes du jury avec 90-95 % de corrélation. En 1982, toute la présélection est faite par ordinateur.
- Il retire des points aux femmes et aux noms à consonance non européenne, comme le jury le faisait. Jusqu'à 60 candidats sur 2 000 écartés chaque année pour ce seul motif.
- Décembre 1986 : deux enseignants de l'école, A. Burke et J. Collier, alertent la Commission for Racial Equality, qui conclut en 1988 à une discrimination.
- La phrase à citer, du BMJ en 1988 : "the prejudice of a computer is no less than that of its designers".
- Probablement le premier cas documenté de "on reproduit les biais du dataset d'entraînement". Même point de départ que l'outil de tri de CV d'Amazon (exemple 5), quarante ans plus tôt.

### 4. APB, France, 2016 (opacité)

Mécanisme : la boîte noire (usage). Seul exemple où le problème n'est pas un biais mais l'impossibilité de le chercher.

- L'association Droits des lycéens demande le code source en mars 2016. Après avis favorable de la CADA, le ministère envoie en octobre une vingtaine de pages imprimées, limitées au tirage au sort des licences en tension.
- "Malicious compliance" : ce qui pose souci ici, c'est la boîte noire qui empêche l'auditabilité. Sans audit possible, aucun des biais précédents ne peut être détecté.

### 5. Amazon et le tri de CV, 2014-2018 (sexe)

Mécanisme : le dataset d'entraînement (données), les embauches passées étant surtout masculines. Aussi : correlation <> causation, par le mot "women's".

- A partir de 2014, Amazon développe un outil qui note les CV de 1 à 5 étoiles. Il est entraîné sur dix ans de candidatures reçues par l'entreprise, très majoritairement masculines pour les postes techniques.
- Le genre n'est pas une variable. Mais le modèle apprend à pénaliser les CV contenant le mot "women's" (par exemple "women's chess club captain") et les diplômées de deux universités féminines. C'est un proxy : le mot est corrélé aux embauches passées, il ne dit rien de la compétence.
- Les ingénieurs neutralisent ces termes, sans pouvoir garantir que le modèle n'en trouvera pas d'autres. Le projet est abandonné, l'affaire est révélée par Reuters en octobre 2018.
- A dire : retirer la variable sensible ne suffit pas, c'est exactement ce que la salle a fait avec la nationalité et le code postal dans le piège.

### 6. Notes des A-levels, Angleterre, 2020 (classe sociale)

Mécanisme : correlation <> causation (modèle). Passé en Angleterre en 2020, pendant Covid

L'objectif était d'éviter l'inflation des notes, donc de conserver la distribution nationale des années précédentes : le modèle y parvient très bien, au prix de l'injustice individuelle. Aussi : la reproduction du passé, par l'historique du lycée.

- Examens annulés pour cause de Covid, l'algorithme d'Ofqual ajuste les notes des professeurs selon l'historique de résultats de chaque lycée.
- 39,1 % des notes sont abaissées d'au moins un cran, les baisses les plus fortes touchant les milieux les plus défavorisés. Les très petits effectifs, plus fréquents dans le privé, échappent à l'ajustement.
- Un bon élève d'un "mauvais" lycée hérite des notes de ses prédécesseurs. Manifestations "Fuck the algorithm", retrait le 17 août, 4 jours après les résultats.
- Public concerné : des gens de l'âge des étudiants.

### 7. CAF, France, 2010-2026 (précarité, handicap, parents isolés) : la boucle se referme

Mécanisme : presque tous. C'est la synthèse (slides "En résumé" puis "Et la CAF ?").

- C'est le cas du piège, on y revient pour le relier aux autres. Elle cumule cinq mécanismes sur sept :
  - reproduction du passé : le score est appris sur les résultats des contrôles passés ;
  - correlation <> causation : la précarité va avec les erreurs, la cause est la complexité des règles ;
  - loi de Goodhart : l'indicateur suivi est l'argent récupéré, pas les erreurs dans les deux sens ;
  - prophétie auto-réalisatrice : voir ci-dessous ;
  - boîte noire : code inaccessible jusqu'à l'action de La Quadrature du Net en 2023, publié par la CAF en 2026.
- Le score est calibré sur les résultats des contrôles passés. Plus de contrôles sur certains profils, donc plus d'indus trouvés chez eux, donc le modèle est "confirmé". Même boucle que le redlining, 90 ans plus tard.
- Précédent aux Pays-Bas (toeslagenaffaire) : le fisc utilise la nationalité comme facteur de risque de fraude aux allocations de garde d'enfants. Des dizaines de milliers de familles accusées à tort, démission du gouvernement en janvier 2021.

## II. Nos expériences (35 min)

Principe : raconter jusqu'au point de décision, s'arrêter, faire se positionner la salle, donner la parole à deux ou trois personnes, puis raconter la suite.

### Elise (~15 min)

- Travail dans une PME (domaine smart city) sur un projet d'optimisation du positionnement de bennes de tri sélectif dans une ville.
- Explication des différentes phases du projet : récolte des données, préparation, stratégie d'analyse, clustering, modèle prédictif, carte de chaleur pour identifier des lieux où déplacer des bennes, expérimentation, rapport
- Questionnements sur l'utilité par rapport aux limites du modèle (R² de 50% : TB pour un modèle sur des comportements, mauvais pour faire des propositions pertinentes) et à la meilleure connaissance des éboueurs sur le terrain
- On juge la qualité d'un modèle sur le critère qu'on a décidé d'optimiser, mais est-ce toujours le bon critère ?

### Quentin (~15 min)

1. Majeure BTP, cycles de dumpers : gains d'efficacité et de sécurité. "Si le chantier va plus vite et est optimisé, c'est forcément meilleur pour la planète non ?"
   - Effet rebond (paradoxe de Jevons), impact social, compréhension du terrain.
2. Startup de traitement de données géospatiales. L'outil est pensé pour favoriser la rénovation énergétique. Un client assureur veut s'en servir pour du pricing.
   - On retombe exactement dans des problèmes de "proxy" vieux comme le monde (a minima les années 30, cf le redlining).
3. Organisme public : maximiser l'impact. "on vous demande un indicateur d'impact unique pour piloter l'équipe"
   - Loi de Goodhart

## III. Atelier (1h)

A valider ensemble : la slide "Atelier" est encore à écrire, ce qui suit est une proposition.

### Temps 1 : l'équité impossible (25 min)

Données fictives, construites pour l'exercice. Deux groupes de 1 000 allocataires : A (revenus stables) et B (revenus instables). Le score les range en trois classes. Le score est calibré : dans une classe donnée, le taux d'indu est le même pour A et pour B.

| Classe de score | Taux d'indu | Groupe A | dont indus | Groupe B | dont indus |
|---|---|---|---|---|---|
| Faible | 10 % | 700 | 70 | 300 | 30 |
| Moyen | 40 % | 200 | 80 | 400 | 160 |
| Elevé | 80 % | 100 | 80 | 300 | 240 |
| Total | | 1 000 | 230 | 1 000 | 430 |

Budget : 400 contrôles. Trois équipes, une règle chacune (10 min de calcul) :

- Equipe 1, même seuil pour tous : à score égal, traitement égal.
- Equipe 2, parité : autant de contrôles dans A que dans B.
- Equipe 3, erreurs égales : un allocataire sans indu doit avoir la même probabilité d'être contrôlé, qu'il soit A ou B.

Corrigé :

| Règle | Contrôles A / B | Indus trouvés | Honnêtes contrôlés, A | Honnêtes contrôlés, B |
|---|---|---|---|---|
| 1. Même seuil | 100 / 300 | 320 | 20 sur 770, soit 2,6 % | 60 sur 570, soit 10,5 % |
| 2. Parité | 200 / 200 | 280 | 80 sur 770, soit 10,4 % | 40 sur 570, soit 7,0 % |
| 3. Erreurs égales | 170 / 230 | 292 | 62 sur 770, soit 8,1 % | 46 sur 570, soit 8,1 % |

Détail des règles 2 et 3 : en A, on contrôle les 100 "élevé" puis 100 "moyen" (règle 2) ou 70 "moyen" (règle 3) ; en B, 200 ou 230 "élevé".

Restitution (10 min), ce qu'il faut faire sortir :

- Règle 1 : la plus "rentable", mais un allocataire B sans indu est contrôlé 4 fois plus souvent qu'un A sans indu.
- Règles 2 et 3 : un A classé "moyen" est contrôlé alors qu'un B classé "élevé" ne l'est pas. A score égal, traitement inégal.
- Aucune règle ne satisfait les trois critères. Ce n'est pas un défaut de ce tableau : c'est un théorème dès que les taux de base diffèrent (Kleinberg, Mullainathan et Raghavan ; Chouldechova, 2016). Il a été formulé à la suite de la controverse COMPAS (voir les exemples en réserve).
- Et le tableau suppose que le score est juste, alors qu'il est appris sur des contrôles passés déjà ciblés.

Conclusion du temps 1 : "équitable" n'est pas un réglage technique. Quelqu'un doit choisir. Qui ?

### Temps 2 : comité de pilotage (35 min)

Mise en situation (5 min) : la CNAF réunit un comité pour décider du sort de son score. Trois issues possibles : on déploie tel quel, on modifie, on arrête.

Cinq rôles, une fiche chacun (à écrire) :

- Direction de la CNAF : objectifs de recouvrement fixés par l'Etat, image publique
- Data scientist : a construit le modèle, connaît ses limites
- Association d'allocataires : vit les contrôles
- Contrôleur ou contrôleuse : reçoit la liste des dossiers, va au domicile
- Défenseur des droits : garant de la non-discrimination

Déroulé : 5 min de préparation par rôle, 15 min de comité, 10 min de débrief.

Débrief : placer les cinq acteurs sur deux axes, influence sur l'algorithme et impact subi. Qui a parlé le plus ? Qui a décidé ? Les plus impactés sont rarement les plus influents. Puis la question de l'ancienne trame : comment donner du poids à ceux qui n'en ont pas ?

Ce qui s'est passé en vrai, à raconter après le débrief :

- 2022-2023 : La Quadrature du Net obtient le code des anciennes versions, Le Monde et Lighthouse Reports enquêtent.
- Octobre 2024 : 15 associations, dont Amnesty, saisissent le Conseil d'Etat. Issue non vérifiée à ce jour, à recouper avant la conférence.
- Janvier 2026 : la CAF met en service un nouveau modèle (DMDE 2026), publie son code source, et annonce avoir retiré nationalité, genre, adresse et données de comportement. Les associations saluent la publication mais maintiennent leur recours, d'après la presse.

## IV. Débat mouvant (20 min)

Chacun se positionne à gauche (d'accord) ou à droite (pas d'accord) de la salle, puis certains expliquent leur positionnement.

- Affirmation 1 : "Je suis personnellement responsable si le travail qu'on me demande a un fort risque de biais discriminatoires."
- Affirmation 2 : "Les algorithmes utilisés dans des domaines critiques (santé, justice, finance) doivent être open source pour permettre leur audit."
- Affirmation 3 : `[à compléter]`

## V. Et pour finir : caveats pour votre métier (10 min)

Transition après le débat : "Trois réflexes qui valent bien au-delà des algorithmes publics, quel que soit votre futur poste." Ce sont les versions générales de trois mécanismes vus en partie I.

### 1. Les données que vous n'avez pas : le biais du survivant (1943)

C'est "les survivants" de la grille. Beaucoup la connaissent déjà : poser la question et laisser la salle répondre.

- Pendant la guerre, l'armée américaine relève les impacts sur les bombardiers rentrés de mission et veut blinder les zones les plus touchées.
- Le statisticien Abraham Wald (Statistical Research Group, université Columbia) fait remarquer que l'échantillon ne contient que les avions revenus. Il faut blinder là où ils n'ont pas d'impacts, les moteurs notamment : ceux qui ont été touchés là ne sont pas rentrés.
- Honnêteté : le schéma de l'avion criblé de points rouges qu'on voit partout est une illustration moderne sur des données hypothétiques, pas un document de Wald. Son mémoire de 1943 est réel, l'anecdote a été embellie depuis.
- A retenir : dans un jeu de données, ceux qui manquent ne manquent pas au hasard. Les femmes dans les crash-tests. A la CAF : on ne connaît les trop-perçus que des dossiers qu'on a contrôlés, et ceux qui ne demandent pas leurs droits n'apparaissent nulle part.

### 2. L'indicateur qu'on vous demande d'optimiser : la loi de Goodhart

C'est "la loi de Goodhart" de la grille.

- L'histoire connue, les cobras de Delhi : l'administration britannique offre une prime par cobra mort, des habitants se mettent à en élever, la prime est supprimée, les cobras sont relâchés. C'est "l'effet cobra", nom popularisé par l'économiste Horst Siebert en 2001.
- Oui, c'est très probablement une légende : on ne lui connaît pas de source historique solide. A dire tel quel, c'est une bonne leçon de méthode.
- La version documentée est française : Hanoï, 1902. L'administration coloniale paie une prime par queue de rat rapportée. On voit apparaître des rats sans queue, relâchés pour se reproduire, et des élevages de rats. L'épisode est documenté par l'historien Michael Vann.
- La loi elle-même vient d'ailleurs : Charles Goodhart, économiste à la Banque d'Angleterre, 1975, à propos des objectifs de masse monétaire. Dès qu'on pilote sur un indicateur, sa relation avec ce qu'on voulait mesurer se défait. La formule "quand une mesure devient une cible, elle cesse d'être une bonne mesure" est de l'anthropologue Marilyn Strathern (1997). Les cobras et les rats illustrent des incitations perverses, ils ne sont pas à l'origine de la loi.
- Lien avec la séance : le témoignage de Quentin sur la mesure d'impact, les A-levels, et tout modèle de machine learning, qui optimise la métrique qu'on lui donne et pas l'intention derrière.

### 3. La corrélation qui tombe trop bien : spurious correlations

C'est "correlation <> causation" de la grille.

- Le site de Tyler Vigen, tylervigen.com/spurious-correlations, aligne des séries sans aucun rapport et très fortement corrélées. Exemple de la slide : la popularité du prénom Margarita et les vols de voitures dans l'Indiana (r = 0,96). Autre classique : les films avec Nicolas Cage et les noyades en piscine.
- Ouvrir le site en direct et en montrer deux ou trois.
- A retenir : avec assez de variables, on trouve toujours une corrélation. C'est ce que fait un modèle à qui on donne 1 000 informations par allocataire.

## VI. Et pour finir : conclusion (15 min)

### Retour sur le piège (5 min)

Réafficher leur liste de variables du début. "Qu'est-ce que vous changeriez ? Les variables, la cible, ou la question posée ?"

Laisser répondre, puis donner les trois niveaux, du plus radical au plus pragmatique. Il n'y a pas de bonne liste de variables : la bonne réponse consiste à contester l'énoncé avant de le résoudre.

1. Changer la cible. L'énoncé disait "récupérer l'argent versé à tort", et ce sont surtout des erreurs. Pourquoi contrôler plutôt que prévenir ? Le même score pourrait déclencher un appel ou un accompagnement avant l'erreur. Il pourrait aussi chercher les erreurs dans l'autre sens : l'argent non versé. Ordres de grandeur :
   - Fraude détectée par les CAF en 2024 : 449 millions d'euros (49 030 fraudes). Sommes versées à tort détectées, erreurs comprises : 1,68 milliard.
   - Non-recours au RSA : 34 % des foyers éligibles ne le demandent pas chaque trimestre, soit environ 750 millions d'euros par trimestre, de l'ordre de 3 milliards par an (DREES, données 2018). Sur ce seul minimum social, l'argent non versé pèse plusieurs fois la fraude détectée sur toutes les prestations.
   - Un contrôle peut jouer dans les deux sens : à la CAF des Yvelines en 2023, 82 % des montants régularisés étaient des indus, 18 % des rappels en faveur des allocataires. Chiffre local, pas de total national des rappels trouvé.
   - Précaution : non-recours et rappels ne sont pas la même chose. Le non-recours concerne des gens qui ne demandent rien, les rappels des allocataires sous-payés. Et la fraude détectée n'est pas la fraude réelle.
2. Traiter la cause plutôt que la prédire. Si les erreurs viennent de la complexité des déclarations, la solution la plus efficace n'est pas un modèle mais des règles plus simples. Depuis le 1er mars 2025, les déclarations trimestrielles du RSA et de la prime d'activité sont préremplies ("solidarité à la source"), pour plus de 6 millions de personnes. Le meilleur modèle est parfois pas de modèle.
3. Si on garde un modèle de ciblage, l'encadrer :
   - garder une part de contrôles tirés au hasard, pour avoir des données non biaisées et casser la boucle "plus de contrôles, donc plus d'indus trouvés" ;
   - mesurer avant déploiement qui est contrôlé, par groupe, et pas seulement combien d'indus on trouve ;
   - préférer les variables qui décrivent le dossier (nombre de déclarations, changements récents) à celles qui décrivent la personne (statut, quartier, situation familiale) ;
   - publier le code et prévoir une voie de contestation ;
   - associer allocataires et contrôleurs à la conception.

Le niveau 3 ne fait pas disparaître le problème : même encadré, le modèle oblige à choisir entre plusieurs définitions de l'équité, c'est ce qu'a montré l'atelier.

### Quelques questions à vous poser (3 min)

1. Sur quelles données du passé est entraîné mon algo ?
2. Qui est absent des données ?
3. Quel critère j'optimise, et qui l'a choisi ?
4. D'où vient la demande, est-ce que je permets aux parties prenantes de contester / auditer ?
5. Est-ce que j'ai un regard statistique et citoyen, produit, et pas juste "belle techno" ?

Deux réflexes de métier :

- Commencer par une baseline simple : reproductible, sobre, explicable. On complexifie si le besoin est avéré.
- Impliquer les parties prenantes au plus tôt. A une époque où coder devient plus simple, c'est le regard produit qui fait la différence.

### L'optimisme par les faits (5 min, à l'oral, sur la slide "Où et comment agir")

L'objectif n'est pas de dégoûter du métier, mais de détricoter l'idée d'algorithme neutre. Dans chaque exemple, quelqu'un de technique a levé le drapeau :

- St George's : deux enseignants de l'école.
- Gender Shades : une doctorante, Joy Buolamwini, mesure 0,8 % d'erreur sur les hommes à peau claire contre 34,7 % sur les femmes à peau foncée. IBM annonce en 2020 l'arrêt de sa reconnaissance faciale généraliste.
- A-levels : retrait de l'algorithme 4 jours après les résultats.
- CAF : code publié et variables retirées en 2026.

Où agir : Data for Good, Eclaireur Public, Biolit, Pyronear, La Quadrature du Net, le Shift. Importance de ne pas "subir la data".

## Exemples en réserve

A sortir selon les questions de la salle.

- Santé, USA, 2019 (origine) : un algorithme hospitalier prédit les dépenses comme proxy des besoins de soin. Comme on dépense moins pour les patients noirs à état de santé égal, il les juge en meilleure santé. Corriger le proxy ferait passer leur part dans le programme d'accompagnement de 17,7 % à 46,5 %. Echo direct au "est-ce le bon critère ?" d'Elise.
- COMPAS, USA, 2016 (origine, justice) : score de risque de récidive utilisé par des juges. Enquête ProPublica : parmi les personnes qui n'ont pas récidivé, 45 % des Noirs avaient été classés à haut risque contre 23 % des Blancs. L'origine n'est pas une variable d'entrée, mais les arrestations passées, le quartier ou l'emploi en sont des proxys. C'est le cas réel derrière le temps 1 de l'atelier.
- Gender Shades, 2018 (sexe + couleur de peau) : trois logiciels commerciaux de classification de genre, 0,8 % d'erreur sur les hommes à peau claire contre 34,7 % sur les femmes à peau foncée, par sous-représentation dans les données d'entraînement. Aussi cité en conclusion.
