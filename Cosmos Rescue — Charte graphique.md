# Cosmos Rescue — Charte graphique

Nov 27, 2026 · @Jm

## Intention visuelle

Un rendu 3D semi-réaliste, rétro-futuriste années 70, en vue isométrique : des machines utilitaires et usées sur un régolithe gris, réchauffées par des lumières ambre et une tempête violette.

- **Références** : la série Cosmos 1999 pour les volumes et les matériaux, Cyclone pour la lisibilité de la vue isométrique.
- **Lisibilité avant tout** : sur un écran de téléphone, chaque élément interactif (colon, cellule, plateforme) doit se repérer en une seconde.
- **Contraste de couleurs** : décor gris et neutre, éléments interactifs en couleurs vives (orange, cyan), danger en violet et rouge.

## Palette de couleurs

| Rôle | Couleur | Code |
| --- | --- | --- |
| Régolithe (sol) | Gris lunaire | #8A8D95 |
| Ombres du décor | Gris anthracite | #3A3C43 |
| Espace | Noir bleuté | #04050B |
| Coque, dômes | Blanc cassé | #E8ECF4 |
| Secours, plateforme, accent | Orange | #FF8A1F |
| Bandes du vaisseau | Rouge | #D62828 |
| Cellules d'énergie, réacteurs | Cyan | #5FF3FF |
| Fenêtres, feux de base | Ambre | #FFC35A |
| Tempête ionique | Violet | #B07BFF |
| Danger, alerte | Rouge vif | #FF4A3A |
| Validé, prêt | Vert | #5DFF9A |

## Typographie

- **Titres, alertes, logo** : Orbitron (Google Fonts), graisses 600 et 900.
- **Interface et textes** : Exo 2 (Google Fonts), graisses 400 à 700, chiffres à chasse fixe pour le tableau de bord.
- **Tailles** : titre 40 à 68 px, alertes 15 px, interface 13 à 14 px, jamais moins de 12 px.
- **Lisibilité** : texte blanc avec une ombre noire portée sur le décor de jeu.

## Caméra, échelle et éclairage

Toutes les images partagent la même caméra, la même lumière et la même échelle. C'est ce qui évite les problèmes de proportions.

- **Caméra** : isométrique orthographique, 30° d'élévation, rapport 2:1, sans perspective. Seules exceptions, les textures du sol et le disque de l'ascenseur, vus exactement de dessus.
- **Lumière** : studio douce venant du haut à gauche. Faces gauches éclairées, faces droites dans l'ombre.
- **Fond** : transparent, sans ombre portée au sol (le jeu dessine les ombres).
- **Repère d'échelle** : un colon mesure 1 tuile de haut, soit 32 unités.

| Élément | Taille au sol | Hauteur |
| --- | --- | --- |
| Colon | 0,5 tuile | 1 tuile |
| Cellule d'énergie | 0,5 tuile | 0,6 tuile |
| Vaisseau | 3,5 tuiles de long | 1,2 tuile |
| Avant-poste | 2,5 tuiles | 1,5 tuile |
| Pic rocheux | 0,6 à 1 tuile | 1,5 à 4 tuiles |
| Plateforme d'atterrissage | 5 tuiles de diamètre | 0,3 tuile |
| Base complète | environ 14 × 9 tuiles | 1,5 à 3 tuiles |

Astuce : pendant la génération, place un colon à côté de l'élément comme repère, puis efface-le.

## Bloc de style commun

Ce bloc se colle à la fin de chaque prompt de la charte. Les prompts sont en anglais, plus efficace avec les générateurs d'images.

```
Consistent game art style: semi-realistic 3D render, retro 1970s hard sci-fi, worn utilitarian materials, true isometric orthographic camera at 30° elevation (2:1), no perspective distortion, soft studio light from top-left, transparent background, no ground shadow, no text, game asset.
```

Pour les vues de dessus (sol, disque de l'ascenseur), remplace la partie caméra par :

```
perfectly top-down orthographic view, camera straight down at 90°, flat even lighting
```

## Prompts vaisseau

Le vaisseau a besoin de 16 vues, en 4 planches : 2 planches de 8 vues décalées de 22,5°, réacteurs éteints puis allumés. Joins l'image actuelle du vaisseau comme référence.

**V1 — Planche A, réacteurs éteints**

```
Sprite sheet of the spaceship from the reference image, identical design, colors and proportions in every frame. 8 views rotating clockwise around the vertical axis in exact 45° steps, starting with the nose pointing toward the viewer (0°, 45°, 90°, 135°, 180°, 225°, 270°, 315°). Grid of 4 columns x 2 rows, each cell 512x512 px, ship centered and same scale in every cell, landing pads on the same invisible ground line.
```

**V2 — Planche B, réacteurs éteints (vues intermédiaires)**

```
Same sprite sheet layout, same ship, rotated in exact 45° steps starting at 22.5° (22.5°, 67.5°, 112.5°, 157.5°, 202.5°, 247.5°, 292.5°, 337.5°).
```

**V3 et V4 — Réacteurs allumés**

Reprends V1, puis V2, en ajoutant :

```
...with bright blue-white glow coming out of the engine nozzles, identical ship and angles.
```

**V5 — Vaisseau original (pour une version diffusable)**

```
Original retro-futuristic lunar rescue shuttle, hexagonal white cargo module with orange rescue chevrons, wide flat wedge-shaped cockpit with dark tinted canopy, two cylindrical engine nacelles under the hull, tripod landing gear with round pads, small dish antenna on top, panel lines, weathered paint.
```

Si les 16 vues ne s'enchaînent pas bien, mieux vaut un modèle 3D (Meshy) rendu automatiquement sous 16 angles dans Blender.

## Prompts base et ascenseur

La base est livrée en calques séparés pour que la plateforme puisse pivoter et descendre. Le code anime les feux du contour (chenillard, clignotement) : le disque doit donc exister en deux états, feux éteints et feux allumés. Joins l'image actuelle de la base comme référence.

**B1 — Base avec puits vide**

```
Same lunar base as the reference image, same isometric angle, scale and lighting, but the circular landing platform is replaced by an open circular elevator shaft: a deep dark round hole with a thick metal rim, yellow and black warning stripes, small amber lights inside the shaft walls. No platform, no orange cross.
```

**B2 — Disque de l'ascenseur, feux éteints (vu de dessus)**

```
Circular landing elevator platform for a lunar base, dark metal disc with a large orange cross made of tiles, ring of 24 evenly spaced round light sockets around the rim, lights switched off (dark glass), panel seams, slight wear. Perfect circle filling a 1024x1024 square canvas, transparent outside the circle.
```

**B3 — Disque de l'ascenseur, feux allumés (vu de dessus)**

```
Exactly the same disc as the previous image, same framing, but the 24 rim lights are switched on, glowing warm amber with a soft halo.
```

**B4 — Paroi du puits (pour la descente)**

```
Interior wall of a circular elevator shaft seen from isometric view, dark metal ribs, vertical rails, amber guide lights, fading to black at the bottom, same rim as the base reference.
```

**B5 — Hangar souterrain (panneau de déchargement)**

```
Underground lunar hangar cutaway, elevator platform lowered with the rescue shuttle from the reference image on it, astronaut crew unloading colonists and glowing energy cells, fuel hoses connected, warm amber lights, wide 16:9 frame.
```

## Prompts décors

**D1 — Sol lunaire (texture répétable, vue de dessus)**

```
Seamless tileable lunar regolith ground texture, grey fine dust with small pebbles and tiny craters, no footprints, 1024x1024.
```

**D2 — Cratères**

```
Set of 6 lunar craters of different sizes on a 3x2 grid, shallow bowls with raised rims, shadow inside on the top-left side, lit rim on the bottom-right, soft fade at the edges to blend into grey regolith.
```

**D3 — Pics rocheux**

```
Set of 6 tall lunar rock spires of different heights and shapes on a 3x2 grid, jagged grey basalt, sharp silhouettes, all standing on the same ground line.
```

**D4 — Avant-postes (faire 3 variantes)**

```
Small lunar outpost module in the same style as the reference base: compact pressurized habitat with a dome, solar panel wing, antenna with red light, airlock door with amber light. Variant: [laboratory / fuel tank / greenhouse].
```

**D5 — Bord du monde**

```
Lunar cliff edge tiles, layered grey rock strata dropping into black space, matching grey regolith on top, 4 tiles for each side of a diamond-shaped map.
```

## Prompts personnages et objets

**P1 — Colons (planche d'animation)**

```
Sprite sheet of a small astronaut colonist in a white and orange spacesuit with dark visor, 4 isometric directions, rows of animations: idle, waving both arms for help, running, hanging from a winch cable, 4 frames each, same scale in every frame, feet on the same ground line.
```

**P2 — Cellule d'énergie**

```
Glowing energy cell canister, cylindrical, cyan light core visible through vertical slots, metal handle on top for a winch hook, 4-frame pulsing glow animation in a row.
```

**P3 — Crochet du treuil**

```
Small industrial winch hook with a short segment of steel cable, orange safety paint, single sprite.
```

## Prompts effets

**E1 — Météorite en chute**

```
Sprite sheet of a burning meteorite falling, rocky core with orange-white fiery trail, 4 frames in a row.
```

**E2 — Impact de météorite**

```
8-frame impact sequence in a row: dust burst, rock debris and expanding shockwave ring on grey lunar soil, ending with a small fresh crater.
```

**E3 — Explosion du vaisseau**

```
8-frame explosion sprite sheet in a row, fiery orange-white blast with grey lunar dust cloud and flying metal debris, no smoke trails (vacuum).
```

**E4 — Poussière des réacteurs**

```
6-frame puff of grey lunar dust kicked up by engine thrust, expanding and fading, in a row.
```

**E5 — Tempête ionique (texture d'appoint)**

```
Swirling ionic storm vortex, violet and cyan electric spiral clouds, glowing dark core, lightning arcs, 8-frame loop in a row.
```

La tempête reste dessinée par le code : cette texture sert seulement à l'enrichir.

## Prompts interface

Pour l'interface, remplace le bloc de style commun par « flat UI, transparent background, no text », sauf pour le logo.

**I1 — Icônes**

```
Set of flat game UI icons, retro sci-fi style, orange #FF8A1F and cyan #5FF3FF on transparent background, consistent 2 px stroke, 128x128 each on a grid: fuel, hull integrity, colonist, energy cell, altitude, winch, lives (small shuttle silhouette), pause, sound on, sound off.
```

**I2 — Logo**

```
Game title logo "COSMOS RESCUE", bold retro-futuristic 1970s space typography, brushed chrome letters with orange outline, subtle violet glow, transparent background.
```

**I3 — Cadre du radar**

```
Circular radar frame for a game HUD, dark translucent glass, thin metal bezel with small tick marks, orange accent, empty center, transparent background.
```

**I4 — Badges de difficulté**

```
Set of 4 small mission patch badges for difficulty levels, embroidered space-agency style, labels RECRUE, PILOTE, VETERAN, CAUCHEMAR, from green to red, transparent background.
```

## Production et nommage des fichiers

Chaque image est livrée en PNG à fond transparent, nommée selon le code de son prompt, pour que je l'intègre sans ambiguïté.

| Code | Fichier | Contenu |
| --- | --- | --- |
| V1 à V4 | vaisseau\_A\_off.png, vaisseau\_B\_off.png, vaisseau\_A\_on.png, vaisseau\_B\_on.png | 4 planches de 8 vues |
| B1 | base\_puits.png | Base sans plateforme |
| B2, B3 | disque\_off.png, disque\_on.png | Disque de l'ascenseur vu de dessus |
| B4, B5 | puits\_paroi.png, hangar.png | Puits et hangar souterrain |
| D1 à D5 | sol.png, crateres.png, pics.png, avantposte\_1.png à avantposte\_3.png, falaise.png | Décors |
| P1 à P3 | colon.png, cellule.png, crochet.png | Personnages et objets |
| E1 à E5 | meteorite.png, impact.png, explosion.png, poussiere.png, tempete.png | Effets |
| I1 à I4 | icones.png, logo.png, radar.png, badges.png | Interface |

**Vérifications avant envoi**

- [ ] Même angle de caméra que les autres images
- [ ] Lumière venant du haut à gauche
- [ ] Fond vraiment transparent, sans damier peint
- [ ] Échelle conforme au tableau des tailles
- [ ] Dans une planche, cases régulières et élément centré
