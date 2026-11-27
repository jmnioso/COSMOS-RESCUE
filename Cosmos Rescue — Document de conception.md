# Cosmos Rescue — Document de conception

Nov 27, 2026 · @Jm

## Pitch

Cosmos Rescue est un jeu d'arcade de sauvetage en 3D isométrique : on pilote un vaisseau de secours au-dessus d'une Lune en dérive pour treuiller des colons et récupérer 5 cellules d'énergie, en évitant une tempête ionique.

- **Inspirations** : la série Cosmos 1999 pour l'ambiance et Cyclone (Vortex Software, ZX Spectrum, 1985) pour le gameplay.
- **Plateforme** : navigateur HTML5, jouable sur iPhone, iPad et ordinateur.
- **Durée d'une partie** : 5 à 15 minutes selon la difficulté.
- **Ton** : tendu mais lisible, rétro-futuriste années 70.
- **Usage** : projet personnel. Le vaisseau actuel reprend l'Aigle de la série, un design protégé : un vaisseau original sera nécessaire avant toute diffusion publique.

## Univers et histoire

Une tempête ionique balaie la face cachée de la Lune et menace les avant-postes isolés autour de la base Séléné.

- **Le joueur** pilote le seul vaisseau de secours disponible.
- **La base Séléné** manque d'énergie : sans ses 5 cellules, elle ne tiendra pas.
- **Les colons** sont bloqués dehors, autour de 12 avant-postes, et font de grands signes à l'approche du vaisseau.
- **La tempête** se déplace, accélère avec le temps et emporte les colons qu'elle traverse.

## Commandes

Les directions suivent l'écran : pousser vers la droite déplace le vaisseau vers la droite de l'écran.

| Action | Tactile (iPhone, iPad) | Clavier |
| --- | --- | --- |
| Diriger | Pouce gauche (joystick virtuel) | Flèches |
| Monter | Bouton HAUT | A |
| Descendre | Bouton BAS | Q |
| Treuil | Bouton TREUIL maintenu | Espace maintenu |
| Pause | Bouton pause (à ajouter) | Échap (à ajouter) |

Le mode paysage est recommandé sur téléphone.

## Règles et déroulement d'une mission

La mission est gagnée quand les 5 cellules d'énergie sont installées à la base. Elle est perdue quand le dernier vaisseau est détruit.

1. Le vaisseau décolle de la plateforme de la base Séléné.
2. Le joueur explore la carte : le radar montre la base, la tempête et les avant-postes où il reste des colons. Les cellules n'apparaissent pas sur le radar, il faut les trouver.
3. Pour récupérer un colon ou une cellule, il place l'ombre du vaisseau dessus, descend sous l'altitude de treuillage et maintient le treuil.
4. Il revient se poser sur la plateforme pour décharger, refaire le plein et réparer.
5. Il repart jusqu'à ce que les 5 cellules soient installées.

**Perte d'un vaisseau** : les colons à bord sont perdus, les cellules retombent au sol à l'endroit du crash, et un nouveau vaisseau attend sur la plateforme.

**Colons au sol** : la tempête emporte ceux qu'elle traverse. Ils sont comptés comme perdus.

## Le vaisseau

Le vaisseau a de l'inertie, une réserve de carburant limitée et une coque qui encaisse les impacts. Les valeurs ci-dessous sont celles du mode Pilote (normal).

| Caractéristique | Valeur |
| --- | --- |
| Altitude maximale | 120 m |
| Altitude de treuillage | 45 m ou moins |
| Portée du treuil au sol | 36 unités autour de l'ombre |
| Capacité du module | 6 colons, cellules illimitées |
| Carburant | 100 %, environ 60 s de vol actif |
| Coque | 100 %, une météorite retire 38 % |
| Vitesse d'atterrissage maximale | 100 unités/s, au-delà crash |

- **Rotation** : le vaisseau tourne progressivement et passe par les 16 vues du sprite, sans saut d'angle.
- **Panne sèche** : sans carburant, il descend seul. Il s'écrase s'il ne se pose pas sur la plateforme.
- **Treuil** : le câble descend à 60 m/s, remonte à 75 m/s. Il faut le maintenir jusqu'à l'accrochage.
- **Indicateurs** : l'ombre au sol montre où tombe le treuil. Le cercle sous le vaisseau devient vert sous 45 m.

## Base Séléné et ascenseur d'atterrissage

La plateforme orange est un ascenseur : elle descend sous terre avec le vaisseau pour le décharger, puis le remonte prêt à repartir.

**Feux de la plateforme**

- **En attente** : les feux du contour tournent en chenillard orange pour guider l'approche.
- **Vaisseau posé** : tous les feux clignotent ensemble, puis passent au rouge fixe pendant la descente.
- **Remontée** : chenillard vert, puis vert fixe quand le vaisseau est prêt au décollage.

**Séquence**

1. **Atterrissage** : le vaisseau se pose à vitesse réduite. Les commandes se verrouillent.
2. **Alignement** : le disque orange pivote pour s'aligner sur l'orientation du vaisseau (environ 0,5 s).
3. **Descente** : le disque s'enfonce avec le vaisseau dans un puits sombre (2 à 3 s).
4. **Sous terre** : un panneau montre le déchargement des colons un par un, puis des cellules, le plein et les réparations. Le vaisseau est à l'abri de la tempête et des météorites, mais le chronomètre continue.
5. **Remontée** : le disque remonte (2 s), un signal annonce « prêt au décollage », et les commandes sont rendues.

**Collisions** : les bâtiments de la base sont solides sous 42 m. La tempête est repoussée à distance de la base.

## Dangers

| Danger | Effet | Comment l'éviter |
| --- | --- | --- |
| Tempête ionique | Fait dériver le vaisseau et réduit les commandes dans un rayon de 460 unités. Le centre détruit le vaisseau et emporte les colons. | Surveiller le radar, contourner large. |
| Météorites | Pluies périodiques d'environ 9 s, annoncées par une alarme. Un cercle rouge au sol marque chaque impact. Un impact retire 38 % de coque. | Rester en mouvement, sortir des cercles rouges. |
| Pics rocheux | Crash si le vaisseau les touche sous leur hauteur (35 à 118 m). | Monter ou contourner. |
| Bâtiments | Crash contre les dômes des avant-postes et la base sous leur hauteur. | Descendre à côté des dômes, pas dessus. |
| Atterrissage brutal | Crash si le vaisseau touche le sol trop vite. | Ralentir avant de descendre. |
| Panne sèche | Le vaisseau descend seul et s'écrase hors de la plateforme. | Rentrer quand le carburant passe sous 25 %. |
| Bord du monde | Le vaisseau rebondit sur la limite. | Aucun risque de crash. |

## Niveaux de difficulté

Quatre niveaux, choisis sur l'écran titre. Pilote correspond au réglage actuel du prototype. Ces valeurs sont un point de départ à ajuster en jouant.

| Réglage | Recrue | Pilote | Vétéran | Cauchemar |
| --- | --- | --- | --- | --- |
| Vaisseaux | 5 | 3 | 3 | 1 |
| Cellules à trouver | 3 | 5 | 5 | 7 |
| Avant-postes | 8 | 12 | 12 | 14 |
| Vitesse de la tempête | 70 % | 100 % | 125 % | 150 % |
| Force de la tempête | 60 % | 100 % | 120 % | 140 % |
| Pluies de météorites | Aucune | Toutes les 26 à 42 s | Toutes les 18 à 30 s | Toutes les 12 à 20 s |
| Consommation de carburant | 70 % | 100 % | 120 % | 140 % |
| Altitude de treuillage | 60 m | 45 m | 40 m | 35 m |
| Cellules sur le radar | Oui | Non | Non | Non |
| Multiplicateur de score | ×0,5 | ×1 | ×1,5 | ×2 |

Un record est enregistré séparément pour chaque niveau.

## Score

Le score récompense les sauvetages, puis la rapidité et les vaisseaux conservés en cas de victoire. Le total est multiplié selon la difficulté.

| Action | Points |
| --- | --- |
| Colon déposé à la base | 100 |
| Cellule installée | 500 |
| Bonus de temps (victoire) | 5 par seconde sous 10 minutes |
| Vaisseau restant (victoire) | 300 |

## Interface et audio

**À l'écran**

- **Tableau de bord** (en haut à gauche) : carburant, coque, altitude (en vert dans la zone de treuillage), colons à bord, cellules, colons sauvés, vaisseaux restants, temps.
- **Radar** (en haut à droite) : base, tempête, avant-postes avec colons, orienté comme la vue isométrique.
- **Flèche BASE** au bord de l'écran quand la base est hors champ, orange vif quand il faut rentrer.
- **Messages** au centre : alertes, conseils, événements.
- **Écrans** : titre avec choix de difficulté, panneau de déchargement sous terre, victoire, échec, avec le score et le record.

**Son**

- Bourdonnement moteur qui suit la poussée et l'altitude.
- Bips pour le treuil, l'embarquement et le déchargement.
- Alarme pour les météorites et la panne sèche.
- Explosions pour les impacts et les crashs.
- À ajouter : bruit de l'ascenseur et musique d'ambiance rétro.

## Feuille de route technique

La prochaine version repart d'une base pensée pour l'isométrique, avec une grille d'échelle commune à tous les éléments.

- [ ] Grille de référence : 1 tuile = 32 unités, un colon mesure environ 1 tuile de haut
- [ ] Vaisseau en 16 vues, rotation progressive vers l'angle visé
- [ ] Base découpée en calques : bâtiments, puits, disque de l'ascenseur
- [ ] Disque vu de dessus, tourné et projeté en isométrique par le code, feux du contour animés par le code
- [ ] Séquence d'ascenseur et panneau de déchargement
- [ ] Écran titre avec les 4 niveaux et un record par niveau
- [ ] Remplacement des dômes, pics, colons, cellules et effets par les sprites de la charte graphique
- [ ] Bouton pause
- [ ] Vaisseau original avant toute diffusion publique
