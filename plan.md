# Contexte 

Troisième année

"conférences technologiques" en 3ème année dans la filière modélisation mathématique, image, et simulation.

Il s'agit d'interventions d'entreprises ou autres organisations, centrées sur du contenu technique (les maths et l'info mis en oeuvre pour répondre à une problématique concrète).

Etudiants peu politisés

# Trame proposée

## 0. Accroche (5 min)

Question aux étudiants : "est-ce que ça vous est déjà arrivé de trouver les résultats d'un algorithme non pertinents voire injustes ?" 

Ils parlent de leurs exemples éventuels, puis on leur cite les 2 ci-dessus :

L'exemple Gender Shades (étude du MIT, 2018, Buolamwini & Gebru) : ils ont testé trois logiciels commerciaux de classification de genre : le taux d'erreur était de 0.8 % pour les hommes à peau claire, contre 34,7 % pour les femmes à peau foncée. Essentiellement un souci de sous-représentation dans le dataset d'entrainement initial. IBM a arrêté son programme de reconnaissance faciale en 2020, notamment suite au shitstorm de cette affaire

2e exemple : l'algorithme utilisé par Amazon pour sélectionner des CV, qui discriminait les femmes (à cause de la sur-représentation d'hommes dans les profils déjà embauchés par l'entreprise) : https://www.numerama.com/tech/426774-amazon-a-du-desactiver-une-ia-qui-discriminait-les-candidatures-de-femmes-a-lembauche.html


## I. Quelques exemples historiques et d'actu (15 min)

Ca ne date pas d'hier, quelques exemples historiques : 
- Redlining dans les années 1920 aux USA
- Quelques exemples sur le pourquoi de la cartographie radicale
- Autre (j'ai un biais assez carto donc à varier)

Revue de presse plus récente :
- APB : longue bataille pour accès à l'algo du code source. Après un an de procédure, le code est livré sur papier. "Malicious compliance" : ici ce qui pose souci c'est la question de boite noire venant empêcher l'auditabilité du code
- CAF : détection fraudes -> [Le monde](https://www.lemonde.fr/les-decodeurs/article/2023/12/04/profilage-et-discriminations-enquete-sur-les-derives-de-l-algorithme-des-caisses-d-allocations-familiales_6203796_4355770.html) ou [Quadrature du net](https://www.laquadrature.net/2022/12/23/notation-des-allocataires-febrile-la-caf-senferme-dans-lopacite/)
(on le garde si on en parle dans l'atelier ?)


## II. Témoignages & QR (30 min : ~15 min chacun)

Quentin :
- Majeure BTP : projet grue connectée et cycles de dumpers -> recherche efficacité, sécurité, etc. Mais effet rebond / paradoxe de Jevons à challenger, impact social, compréhension terrain, ...
- Startup traitement données géospatiales : idée de départ pour favoriser rénovation énergétique, in fine pricing assurance. Principe de non neutralité de la tech
- Organisme public : recherche de maximisation de l'impact. Pose tout de même question de comment on mesure un impact sans tomber dans paradoxe de goodhart, et fragilité de l'écosystème

Elise : 
- Travail dans une PME (domaine smart city) sur un projet d'optimisation du positionnement de bennes de tri sélectif dans une ville.
- Explication des différentes phases du projet : récolte des données, préparation, stratégie d'analyse, clustering, modèle prédictif, carte de chaleur pour identifier des lieux où déplacer des bennes, expérimentation, rapport
- Questionnements sur l'utilité par rapport aux limites du modèle (R² de 50% : TB pour un modèle sur des comportements, mauvais pour faire des propositions pertinentes) et à la meilleure connaissance des éboueurs sur le terrain
- On juge la qualité d'un modèle sur le critère qu'on a décidé d'optimiser, mais est-ce toujours le bon critère ?


## III. Atelier sur la gouvernance des algorithmes (1h)

On présente 3 algorithmes : celui de la CAF, Albert (aide aux agents publics) et la vidéo-surveillance algorithmique.

Division en 3 groupes, et réflexion sur : quels sont les acteurs liés à cet algorithme ? (conception, impacts...)
Pour chaque acteur, remplir une fiche acteur indiquant à quel point il est influent pour et impacté par le fonctionnement de l'algorithme.
Restitution tous ensemble, on positionne les fiches sur un double axe impacté +/-, influence +/-. On voit qu'il y a globalement des acteurs influents et peu impactés, et d'autres peu influents et très impactés.

Re-division en 3 groupes, choix d'un acteur pour lequel on réfléchit à : "Quelle(s) solution(s) envisager pour permettre à l’acteur de participer à la prise de décision sur le système algorithmique et d’accroître son influence dessus ?"
(+ restitution)


## IV. Débat mouvant (20 min)

(chacun se positionne à droite ou à gauche de la salle à chaque question selon son avis, puis certains expliquent leur positionnement)

- Est-ce que je suis personnellement responsable si le travail qu'on me demande a un fort risque de biais discriminatoires ?
- Les algorithmes utilisés dans des domaines critiques (santé, justice, finance) devraient-ils être open source pour permettre leur audit, même si cela signifie révéler des secrets industriels ?
- Avez-vous déjà été confronté à des demandes de votre employeur qui vous questionnaient d'un point de vue éthique ?
  
(ajouter des questions, en essayant de se rapprocher autant que possible des enjeux de leur filière ?)


## V. Ouverture optimiste (20 min)

L'objectif n'est pas de dégouter du métier bien entendu ; il s'agit juste d'essayer de détricoter l'idée de "science ou algo neutre". Chaque algo porte en soit des biais il est important d'en avoir conscience et être capable de les reconnaître et faire évoluer.

En pratique dans le métier : 
- Privilégier baseline simple pour tous leurs modèles : reproductibilité, sobriété, explicabilité, et incrémenter si le besoin est avéré
- Impliquer les parties prenantes au plus tôt. Notamment à une époque où coder devient plus simple, il est (de plus en plus) important d'avoir un rôle produit "éclairé" quand on est tech.

En organisation : 
- Des organisations citoyennes qui peuvent être une source d'empowerment, importance de ne pas "subir la data" -> Exemple projets data for good, exemple Eclaireur Public, Biolit, Pyronear, ou assos type quadrature du net, shift
- Prêter une attention à ce qui est fait, se faire porte parole de modèles optimistes open source par exemple

---

Marge (transitions/questions) : ~15-20 min
