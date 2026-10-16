# Notes pour l'oral

## 1. La CAF (10 min)

### Pour commencer / Choisissez 5 variables (5 min)

Vous êtes data scientist à la CNAF (Caisse nationale des allocations familiales). Chaque mois, 13,8 millions de foyers reçoivent une prestation. Vous avez environ 700 contrôleurs pour les contrôles sur place (chiffre de presse, à recouper). Votre mission : choisir les dossiers à contrôler pour récupérer le plus possible d'argent versé à tort.

### Ce modèle existe vraiment

- Le score existe depuis le début des années 2010. Il note chaque foyer entre 0 et 1, chaque mois : plus de 13 millions de scores, portant sur 32 millions de personnes.
- Quelques dizaines de variables, retenues après un apprentissage sur plus de 1 000 informations par allocataire.
- Code fermé au début
- La Quadrature du Net a obtenu le code source des versions 2010-2018. Ce qui fait monter le score : faibles revenus, chômage, RSA, handicap (AAH, surtout avec un emploi), parent isolé (des femmes dans 80 % des cas), quartier défavorisé.
- L'exemple de l'AAH (allocation aux adultes handicapés) : sans emploi, l'allocataire déclare ses ressources une fois par an et son allocation est stable. Avec un emploi en milieu ordinaire, il passe à une déclaration tous les trois mois ("AAH trimestrialisée") et l'allocation est recalculée à chaque fois. Plus de déclarations et des revenus qui bougent, donc plus d'erreurs, donc plus de trop-perçus dans les données passées, donc un score élevé. La personne handicapée qui travaille est davantage contrôlée parce que sa règle est plus compliquée.

### Fraude ou erreur ?

- Le point clé : le modèle ne prédit pas la fraude mais le risque d'indu, c'est-à-dire de trop-perçu, qui est le plus souvent une erreur. Or on se trompe là où les règles sont compliquées : minima sociaux, déclarations trimestrielles, revenus qui bougent. Le score mesure la complexité des règles imposées aux plus précaires, pas leur malhonnêteté.
- Pourquoi "il mesure surtout l'exposition à des règles complexes" :
  - Ordres de grandeur : selon la Cour des comptes, 8 % des prestations versées en 2024 sont entachées d'erreurs, soit 6,3 milliards d'euros. La fraude détectée la même année : 449 millions.
  - Ces erreurs vont dans les deux sens : la Cour compte aussi des sommes dues jamais versées. Une fraude ne joue que dans un sens, une règle trop compliquée produit des erreurs dans les deux.
  - Elles sont concentrées là où les règles sont compliquées. D'après le directeur de la CNAF devant les parlementaires, 96 % des erreurs relevées par la Cour portent sur le RSA et les aides au logement, et 83 % viennent des déclarations : pour moitié inexactes dès le départ, pour moitié devenues inexactes à cause du décalage entre déclaration et calcul de la prestation. Ce décalage est de la pure mécanique de règle. Un quart des montants de la prime d'activité, elle aussi déclarée tous les trois mois, est entaché d'erreurs.
  - Le même allocataire change de score en changeant de régime de déclaration : c'est l'exemple de l'AAH ci-dessous.
  - L'Etat a reconnu le problème : le Défenseur des droits dénonçait en 2017 des sanctions contre des allocataires "de bonne foi mais mal informés", la loi du 10 août 2018 crée un droit à l'erreur, et la "solidarité à la source" préremplit les déclarations depuis 2025 pour réduire les erreurs.
  - Le score mêle aussi de la fraude. En 2019, les fraudes détectées se répartissaient en omissions et fausses déclarations (69 %), fausses déclarations d'isolement (18 %) et faux ou escroqueries (12,5 %) ; le critère "parent isolé" est donc en partie lié à la vie de couple dissimulée. Une même omission de ressources peut être une erreur ou une fraude, seule l'intention les distingue, et les données ne l'enregistrent jamais.

- Point important : nationalité contre code postal : vous avez refusé l'une et pris l'autre, alors que le code postal porte en partie la même information. C'est ce qu'on appelle un proxy.

Le travail d'ingénieur ne peut pas se limiter à chercher à optimiser un algo on voit qu'il faut réfléchir avec la complexité métier.

## 2. Ça ne date pas d'hier (15 min)

### Qu'est-ce qui pose problème et pourquoi ?

Ce mécanisme n'a pas attendu le machine learning. Neuf exemples, du plus ancien au plus récent.

Un système de décision est calibré sur des données du passé, donc il reproduit les discriminations du passé, avec en prime un vernis de neutralité.

### 1935 : redlining (origine / quartier)

Mécanisme de prophétie auto-réalisatrice. 

Aussi : correlation <> causation, le quartier servant de proxy de l'origine.

- Objectif attribution de prêts immobiliers abordables qui a accéléré le déclin des centre villes
- 1935-1940 : l'agence fédérale HOLC fait cartographier 239 villes en 4 classes de risque de crédit, de A ("best") à D ("hazardous", en rouge). La composition raciale du quartier pèse lourd dans la note.
- La boucle : pas de prêt, donc pas d'investissement, donc le quartier se dégrade, donc la carte "avait raison". La prédiction fabrique ses propres données.
- Entre 1945 et 1959, les Afro-Américains ont reçu moins de 2 % de tous les prêts immobiliers assurés par le gouvernement fédéral
- Interdit en 1968 (Fair Housing Act) donc après une trentaine d'années, mais les effets restent dans les données. Par exemple en 2016, la livraison Amazon Prime en un jour exclut des quartiers majoritairement noirs dans plusieurs villes, dont Roxbury à Boston, sans que l'origine soit une variable. Idem des problèmes de santé publique et qualité de l'air subsitent encore ce jour.

### Années 1970 : crash-tests (sexe)

Mécanisme : le dataset d'entraînement.

- Les tests reposent historiquement sur un mannequin d'homme "moyen", mis au point dans les années 1970.
- Sur les accidents réels aux USA entre 1998 et 2008, une conductrice ceinturée a un risque de blessure grave supérieur de 47 % à celui d'un conducteur dans un accident comparable
- Aujourd'hui encore les tests prévoient un mannequin plus typé "masculin" (taille, poids, morphologie, et même conception globale de la voiture)
- Ici ce qui fait office de "dataset", c'est le modèle physique utilisé au départ lui même lui-même. Données d'entrée parcellaires qui font que inadapté à une partie de la population.

A noter que cela se retrouve en pharma, exemple : le somnifère zolpidem :en janvier 2013, l’agence américaine du médicament (FDA) a divisé par deux la dose recommandée pour les femmes, de 10 mg à 5 mg. Elles éliminent la molécule plus lentement, ce qui laissait un effet résiduel le lendemain matin, notamment au volant. C’était 20 ans après sa mise sur le marché.

### 1979 : St George's, Londres (sexe + origine)

Mécanisme : la reproduction du passé. C'est le cas le plus pur de biais humain intégré à l'algorithme.

- Un enseignant écrit un programme pour présélectionner les candidatures et rendre le processus d'admission moins pénible pour l'administration. En 1979, il reproduit les notes du jury avec 90-95 % de corrélation. En 1982, toute la présélection est faite par ordinateur.
- Il retire des points aux femmes et aux noms à consonance non européenne, comme le jury le faisait. Jusqu'à 60 candidats sur 2 000 écartés chaque année pour ce seul motif.
- Décembre 1986 : deux enseignants de l'école, A. Burke et J. Collier, alertent la Commission for Racial Equality, qui conclut en 1988 à une discrimination.
- La phrase à citer, du British Medical Journal en 1988 : "the prejudice of a computer is no less than that of its designers".
- Probablement le premier cas documenté de "on reproduit les biais du dataset d'entraînement". Même point de départ que l'outil de tri de CV d'Amazon (exemple 5), 40 ans plus tôt.

### 2016 : APB (opacité)

Mécanisme : la boîte noire. Seul exemple où le problème n'est pas un biais mais l'impossibilité de le chercher.

- L'association Droits des lycéens demande le code source en mars 2016. Après avis favorable de la CADA, le ministère envoie en octobre une vingtaine de pages imprimées, limitées au tirage au sort des licences en tension.
- "Malicious compliance" : ce qui pose souci ici, c'est la boîte noire qui empêche l'auditabilité. Sans audit possible, aucun des biais précédents ne peut être détecté.
- Des règles discutables et opaques sont trovuées, et un manque de base légale.
   - En octobre 2016 le code reçu est partiel. Le document d'une vingtaine de pages ne porte que sur le classement aléatoire des formations non sélectives. Les devs jugent qu'il ne permettait pas de comprendre l'algorithme.
   - Le tirage au sort dans les licences en tension (STAPS, PACES, etc.) n'avait aucune base légale. Une circulaire l'a rendu officiel en avril 2017. Le Conseil d'État ne l'a pas suspendue, mais n'a pas jugé le fond.
   - La CNIL a mis le ministère en demeure (décision du 30 août 2017, rendue publique le 28 septembre). Le motif : manque de transparence et prise de décision automatisée sans information des candidats.
   - La Cour des comptes a épinglé APB dans un rapport du 19 octobre 2017. Elle critique une procédure peu compréhensible et sans cadre juridique. La ministre a alors annoncé l'ouverture du code et des données, puis APB a été remplacé par Parcoursup en 2018.


### 2018 : Amazon et les CV (sexe) - Elise

Mécanisme : le dataset d'entraînement, les embauches passées étant surtout masculines. 

- A partir de 2014, Amazon développe un outil qui note les CV de 1 à 5 étoiles. Il est entraîné sur dix ans de candidatures reçues par l'entreprise, très majoritairement masculines pour les postes techniques.
- Le genre n'est pas une variable. Mais le modèle apprend à pénaliser les CV contenant le mot "women's" (par exemple "women's chess club captain") et les diplômées de deux universités féminines.
- C'est un proxy : le mot est corrélé aux embauches passées, il ne dit rien de la compétence.
- Les ingénieurs neutralisent ces termes, sans pouvoir garantir que le modèle n'en trouvera pas d'autres. Le projet est abandonné, l'affaire est révélée par Reuters en octobre 2018.
- Retirer la variable sensible ne suffit pas, c'est exactement ce que la salle a fait avec la nationalité et le code postal dans le piège.

### 2020 : A-levels (classe sociale) - Elise

Mécanisme : correlation <> causation (modèle). 

- En Angleterre en 2020, les examens sont annulés pour cause de Covid, l'algorithme d'Ofqual ajuste les notes des professeurs selon l'historique de résultats de chaque lycée (objectif rester sur la même courbe de ditribution que les années précédentes)
- 40% environ des notes sont abaissées d'au moins un cran, les baisses les plus fortes touchant les milieux les plus défavorisés. Les très petits effectifs, plus fréquents dans le privé, échappent à l'ajustement.
- Un bon élève d'un "mauvais" lycée hérite des notes de ses prédécesseurs. Manifestations "Fuck the algorithm", retrait le 17 août, 4 jours après les résultats.

### 2024 : des modèles de langage trient les CV (origine, sexe)

ATS : Applicant Tracking System

Mécanisme : souci dans le dataset d'entraînement. C'est comme Amazon en 2018, mais avec des modèles généralistes que n'importe quelle entreprise peut brancher sur son logiciel de recrutement (ATS).

- Kyra Wilson et Aylin Caliskan (Université de Washington) prennent plus de 500 CV et 500 offres d'emploi réels, sur neuf métiers. Seul le prénom change : 120 prénoms associés à des hommes, des femmes, des personnes noires ou blanches. Plus de 3 millions de comparaisons.
- Les prénoms associés aux personnes blanches sont préférés dans 85 % des cas, les prénoms féminins dans 11 % seulement. Les hommes noirs sont désavantagés dans jusqu'à 100 % des cas.
- Précision honnête : les modèles testés sont des modèles d'embedding pas des chatbots à proprement parler
- Personne n'a entraîné ces modèles à recruter. Ils ont appris sur tout le web, avec ses associations entre prénoms, métiers et compétences, et les ressortent dans un usage pour lequel ils n'ont pas été conçus.

### 2024-2026 : l'IA générative, aux dernières nouvelles tout va bien

- Racisme caché, *Nature*, septembre 2024 (Hofmann, Kalluri, Jurafsky, King, "AI generates covertly racist decisions about people based on dialect".
  - Méthode : on donne au modèle un tweet en anglais afro-américain (AAE) ou sa traduction en anglais standard, environ 2 000 paires, et on lui demande de décrire l'auteur. La race n'est jamais mentionnée.
  - 12 modèles testés
  - Stéréotypes : pour l'AAE, les modèles sortent "ignorant", "lazy", "stupid", "dirty", "rude", "aggressive". C'est plus négatif que tous les stéréotypes humains mesurés dans les enquêtes, et le plus proche de ceux de 1933 (étude de Katz et Braly à Princeton). Interrogés directement sur les Afro-Américains, les mêmes modèles répondent "musical", "religious", "loyal".
  - Emploi : l'AAE est associé à cuisinier, soldat, vigile, chanteur ; l'anglais standard à psychologue, professeur, économiste.
  - Justice (procès fictif, seul le dialecte change) : écart de 5%. Condamnation dans 68,7 % des cas contre 62,1 % ; peine de mort pour un meurtre au premier degré dans 27,7 % des cas contre 22,8 %.
  - Ni la taille ni l'alignement ne corrigent le biais : les modèles plus gros ont des stéréotypes cachés plus forts, et l'entraînement par retour humain (GPT-3 contre GPT-3.5) rend les stéréotypes affichés plus positifs sans changer significativement les stéréotypes cachés. Les auteurs en concluent que l'alignement apprend aux modèles à masquer le racisme en surface.
- Salaire, THWS (Würzburg-Schweinfurt), juillet 2025. Cinq chatbots grand public, des profils identiques sauf le genre, et la question "quel salaire demander ?". L'exemple qui a circulé : 400 000 dollars conseillés à un homme, 280 000 à une femme, pour un poste médical à Denver.
- Santé, LSE, août 2025. Des outils d'IA utilisés par plus de la moitié des collectivités anglaises résument les dossiers d'aide sociale. Sur 617 dossiers réels où seul le genre change (29 616 paires de résumés), le modèle Gemma de Google emploie plus souvent "handicapé", "incapable" ou "complexe" pour les hommes, et omet ou atténue des besoins équivalents chez les femmes.
- Assistants, Université de Limerick, en octobre 2026. 189 participants travaillent en réalité virtuelle avec deux avatars, Johan et Johanna, qui utilisent le même modèle (GPT-4). Payés en argent réel, ils donnent environ 10 % de moins à Johanna, tout en affirmant en entretien qu'ils ne feraient aucune différence. Ici ce n'est pas l'IA qui discrimine, ce sont ses utilisateurs.
- Point important : ces modèles n'ont été entraînés ni à recruter, ni à conseiller des salaires, ni à résumer des dossiers sociaux. Ils ont appris sur le web et ressortent ses associations dans des usages pour lesquels ils n'ont pas été conçus.

### En résumé (5min)

### Et la CAF ? (précarité, handicap, parents isolés) : la boucle se referme

Mécanisme : presque tous.


- reproduction du passé : le score est appris sur les résultats des contrôles passés ;
- correlation <> causation : la précarité va avec les erreurs, la cause est la complexité des règles ;
- loi de Goodhart : l'indicateur suivi est l'argent récupéré, pas les erreurs dans les deux sens ;
- prophétie auto-réalisatrice : voir ci-dessous ;
- boîte noire : code inaccessible jusqu'à l'action de La Quadrature du Net en 2023, publié par la CAF en 2026.
- Le score est calibré sur les résultats des contrôles passés. Plus de contrôles sur certains profils, donc plus d'indus trouvés chez eux, donc le modèle est "confirmé". Même boucle que le redlining, 90 ans plus tard.

## 3. Comment cela se retrouve dans nos expériences (10 min)

### Élise (~5 min)

- Travail dans une PME (domaine smart city) sur un projet d'optimisation du positionnement de bennes de tri sélectif dans une ville.
- Explication des différentes phases du projet : récolte des données, préparation, stratégie d'analyse, clustering, modèle prédictif, carte de chaleur pour identifier des lieux où déplacer des bennes, expérimentation, rapport
- Questionnements sur l'utilité par rapport aux limites du modèle (R² de 50% : TB pour un modèle sur des comportements, mauvais pour faire des propositions pertinentes) et à la meilleure connaissance des éboueurs sur le terrain
- On juge la qualité d'un modèle sur le critère qu'on a décidé d'optimiser, mais est-ce toujours le bon critère ?

### Quentin (~5 min)

1. Majeure BTP, cycles de dumpers : gains d'efficacité et de sécurité. "Si le chantier va plus vite et est optimisé, c'est forcément meilleur pour la planète non ?"
   - Effet rebond (paradoxe de Jevons), impact social, compréhension du terrain.
2. Startup de traitement de données géospatiales. L'outil est pensé pour favoriser la rénovation énergétique. Un client assureur veut s'en servir pour du pricing.
   - On retombe exactement dans des problèmes de "proxy" vieux comme le monde (a minima les années 30, cf le redlining).
3. Organisme public : maximiser l'impact. "on vous demande un indicateur d'impact unique pour piloter l'équipe"
   - Loi de Goodhart

## 4. Atelier (1h)

A voir ensemble 

## 5. Débat mouvant si on a le temps (20 min)

Chacun se positionne à gauche (d'accord) ou à droite (pas d'accord) de la salle, puis certains expliquent leur positionnement.

- Affirmation 1 : "Je suis personnellement responsable si le travail qu'on me demande a un fort risque de biais discriminatoires."
- Affirmation 2 : "Les algorithmes utilisés dans des domaines critiques (santé, justice, finance) doivent être open source pour permettre leur audit."
- Affirmation 3 : `[à compléter]`

## 6. Et pour finir, quelques réflexes (10 min)

Transition après le débat : "Quatre réflexes qui valent bien au-delà des algorithmes publics, quel que soit votre futur poste." Ce sont les versions générales de trois mécanismes vus en partie I.

### 1943 : les avions qui reviennent

C'est "les survivants" de la grille. Beaucoup la connaissent déjà : poser la question et laisser la salle répondre.

- Pendant la guerre, l'armée américaine relève les impacts sur les bombardiers rentrés de mission et veut blinder les zones les plus touchées.
- Le statisticien Abraham Wald (Statistical Research Group, université Columbia) fait remarquer que l'échantillon ne contient que les avions revenus. Il faut blinder là où ils n'ont pas d'impacts, les moteurs notamment : ceux qui ont été touchés là ne sont pas rentrés.
- Honnêteté : le schéma de l'avion criblé de points rouges qu'on voit partout est une illustration moderne sur des données hypothétiques, pas un document de Wald. Son mémoire de 1943 est réel, l'anecdote a été embellie depuis.
- A retenir : dans un jeu de données, ceux qui manquent ne manquent pas au hasard. Les femmes dans les crash-tests. A la CAF : on ne connaît les trop-perçus que des dossiers qu'on a contrôlés, et ceux qui ne demandent pas leurs droits n'apparaissent nulle part.

### 1902 : les rats de Hanoï

C'est "la loi de Goodhart" de la grille.

- L'histoire connue, les cobras de Delhi : l'administration britannique offre une prime par cobra mort, des habitants se mettent à en élever, la prime est supprimée, les cobras sont relâchés. C'est "l'effet cobra", nom popularisé par l'économiste Horst Siebert en 2001.
- Oui, c'est très probablement une légende : on ne lui connaît pas de source historique solide. A dire tel quel, c'est une bonne leçon de méthode.
- La version documentée est française : Hanoï, 1902. L'administration coloniale paie une prime par queue de rat rapportée. On voit apparaître des rats sans queue, relâchés pour se reproduire, et des élevages de rats. L'épisode est documenté par l'historien Michael Vann.
- La loi elle-même vient d'ailleurs : Charles Goodhart, économiste à la Banque d'Angleterre, 1975, à propos des objectifs de masse monétaire. Dès qu'on pilote sur un indicateur, sa relation avec ce qu'on voulait mesurer se défait. La formule "quand une mesure devient une cible, elle cesse d'être une bonne mesure" est de l'anthropologue Marilyn Strathern (1997). Les cobras et les rats illustrent des incitations perverses, ils ne sont pas à l'origine de la loi.
- Lien avec la séance : le témoignage de Quentin sur la mesure d'impact, les A-levels, et tout modèle de machine learning, qui optimise la métrique qu'on lui donne et pas l'intention derrière.

### 201x : Internet

C'est "correlation <> causation" de la grille.

- Le site de Tyler Vigen, tylervigen.com/spurious-correlations, aligne des séries sans aucun rapport et très fortement corrélées. Exemple de la slide : la popularité du prénom Margarita et les vols de voitures dans l'Indiana (r = 0,96). Autre classique : les films avec Nicolas Cage et les noyades en piscine.
- Ouvrir le site en direct et en montrer deux ou trois.
- La citation de la slide, "si on torture les données assez longtemps, elles finissent par avouer", est attribuée à l'économiste Ronald Coase (prix Nobel 1991). Il l'aurait dite dans les années 1960 sans jamais la publier ; la première trace écrite est une conférence du statisticien I. J. Good en 1971, qui la lui attribue.
- A retenir : avec assez de variables, on trouve toujours une corrélation. C'est ce que fait un modèle à qui on donne 1 000 informations par allocataire.

### 1973 : les admissions de Berkeley

C'est encore "correlation <> causation" de la grille, sous sa forme la plus piégeuse : une variable cachée (la composition des groupes) inverse la conclusion.

- Berkeley, automne 1973 : 12 763 candidatures en master. 44 % des hommes sont admis, contre 35 % des femmes. L'université craint un procès pour discrimination et demande une étude à des statisticiens.
- Filière par filière, l'écart disparaît, voire s'inverse : dans les six plus grandes, les femmes ont un taux d'admission égal ou supérieur dans quatre cas. Sur les 85 filières, 4 sont significativement défavorables aux femmes et 6 aux hommes. L'analyse groupée trouve même un léger biais en faveur des femmes.
- Explication : les femmes candidatent surtout aux filières les plus sélectives (lettres par exemple), les hommes à des filières qui admettent beaucoup (ingénierie). Le chiffre global mélange des filières qui n'ont rien à voir.
- Ce qu'il ne faut pas en conclure : "il n'y avait pas de discrimination". La question se déplace. Pourquoi les femmes visaient-elles des filières plus encombrées et moins financées ? Les auteurs eux-mêmes renvoyaient à des orientations façonnées en amont, par l'éducation et la socialisation (paraphrase, à vérifier dans l'article).
- Lien avec la séance : aucun de nos neuf exemples n'est à proprement parler un paradoxe de Simpson. Le plus proche est le tableau de l'atelier : dans chaque classe de score, le taux d'indu est le même pour A et B, mais les taux globaux diffèrent (23 % contre 43 %), uniquement à cause de la répartition dans les classes. Les A-levels en sont un cousin : la distribution nationale est juste, les notes individuelles ne le sont pas.
- A retenir : avant de conclure sur un chiffre agrégé, se demander par quoi il faudrait le découper.

## 7. Conclusion (10 min)

### Et par rapport à l'algo de la CNAF

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

### Quelques questions à vous poser

1. Sur quelles données du passé mon algo est-il entraîné, et qui en est absent ? (reproduction du passé, survivants)
2. Quel critère j'optimise, et qui l'a choisi ? (Goodhart)
3. Ce résultat n'est-il pas trop beau pour être vrai ? (spurious correlations)
4. Le chiffre global tient-il quand je le découpe ? (Simpson)
5. D'où vient la demande, et les parties prenantes peuvent-elles contester ou auditer ? (boîte noire)
6. Est-ce que j'ai un regard statistique et citoyen, produit, et pas juste "belle techno" ?

Et dans vos stages c'était comment ?

Deux réflexes de métier :

- Commencer par une baseline simple : reproductible, sobre, explicable. On complexifie si le besoin est avéré.
- Impliquer les parties prenantes au plus tôt. A une époque où coder devient plus simple, c'est le regard produit qui fait la différence.

### Où et comment agir, l'exemple DataForGood (10 min)

L'objectif n'est pas de dégoûter du métier, mais de détricoter l'idée d'algorithme neutre. 

Dans chaque exemple qui a été donné, quelqu'un, de technique ou pas, a lancé l'alerte (et dans tous les cas la tech a été impliquée)

Où agir : quelques exemples

### Merci, des questions ?

---

# Autres

## MISC

- Corrélation contre causalité : pour prédire, une corrélation suffit, et c'est pour ça que le modèle "marche". Le problème commence quand on décide : contrôler, refuser, noter quelqu'un, c'est traiter la corrélation comme une propriété de la personne. Prédire n'est pas décider.
- Aucun de ces mécanismes n'est une erreur de calcul. Et même en les corrigeant tous, il reste un choix de valeurs entre définitions de l'équité : c'est l'objet de l'atelier. Ne pas laisser croire qu'il "suffit de faire de la bonne stat".

Autres exemples
- Santé, USA, 2019 (origine) : un algorithme hospitalier prédit les dépenses comme proxy des besoins de soin. Comme on dépense moins pour les patients noirs à état de santé égal, il les juge en meilleure santé. Corriger le proxy ferait passer leur part dans le programme d'accompagnement de 17,7 % à 46,5 %. Echo direct au "est-ce le bon critère ?" d'Elise.
- COMPAS, USA, 2016 (origine, justice) : score de risque de récidive utilisé par des juges. Enquête ProPublica : parmi les personnes qui n'ont pas récidivé, 45 % des Noirs avaient été classés à haut risque contre 23 % des Blancs. L'origine n'est pas une variable d'entrée, mais les arrestations passées, le quartier ou l'emploi en sont des proxys. C'est le cas réel derrière le temps 1 de l'atelier.
- Gender Shades, 2018 (sexe + couleur de peau) : trois logiciels commerciaux de classification de genre, 0,8 % d'erreur sur les hommes à peau claire contre 34,7 % sur les femmes à peau foncée, par sous-représentation dans les données d'entraînement. Aussi cité en conclusion.

## Retour en 1935 : la cartographie radicale (3 min)

Slide avant "Où et comment agir". On revient à la première carte de la séance pour montrer que les mêmes outils peuvent servir à l'inverse.

- 1968-1971 : à Detroit, le géographe William Bunge et la Detroit Geographical Expedition font cartographier la ville par ses habitants, dans les quartiers noirs. Ils produisent des cartes que personne d'autre ne faisait, comme celle des enfants noirs renversés par les automobilistes qui traversent leur quartier pour rejoindre les banlieues aisées. Livre : *Fitzgerald: Geography of a Revolution* (1971).
- 2016 : l'Université de Richmond numérise et publie les cartes de redlining (Mapping Inequality). Les mêmes cartes servent aujourd'hui à mesurer les effets du redlining sur la santé, les températures urbaines ou le patrimoine.
- A retenir : qui choisit ce qu'on mesure choisit ce qu'on voit. Transition vers "Où et comment agir".