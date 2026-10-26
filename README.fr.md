# Alpha & Omega

*[English version](README.md)*

Un jeu de stratégie au tour par tour pour deux joueurs, avec des loups-garous, qui se joue dans le
terminal. Je l'ai écrit en Python pendant ma première année d'informatique à l'Université de Namur (2022).
Deux meutes s'affrontent sur une grille : chacune a un **alpha**, un **oméga** et des loups-garous ordinaires,
et le premier joueur qui perd son alpha perd la partie.

![Une partie IA contre IA sur maps/classic.ano, une image par tour, jusqu'à la mort d'un alpha](docs/alpha-omega.gif)

*IA contre IA sur `maps/classic.ano`, une image par tour. Le rouge et le vert sont les deux meutes :
`α` l'alpha, `Ω` l'oméga, `⦿` un loup-garou, `X` un loup sans énergie ; le nombre sous chaque pièce est son
énergie. Les deux barres du bas montrent la santé de chaque alpha.*

C'était un projet de groupe à quatre étudiants ; j'ai écrit l'essentiel du code (1 584 des 1 590 lignes
ajoutées au moteur et à l'IA dans l'historique d'origine).

## Les règles en bref

- À chaque tour, chaque joueur donne ses ordres à ses loups : se déplacer, manger, attaquer ou pacifier.
- Les loups gagnent et perdent de l'**énergie** : manger la nourriture de la carte (baies, pommes, souris,
  lapins, cerfs) la recharge, les combats la consomment.
- Un loup près de son alpha gagne un bonus de +30, près des autres membres de la meute +10 : les formations comptent.
- L'**oméga** peut dépenser 40 points d'énergie pour *pacifier* les loups ennemis autour de lui pendant un tour.
- Si aucun loup n'est blessé pendant 200 tours, la meute qui a le plus d'énergie au total gagne.

Les ordres se tapent sur une ligne, `x-y:<ordre>x-y` :

```text
3-2:@4-2 1-1:*1-2 3-3:<4-4 2-2:pacify
 move     attack   eat      pacify (omega)
```

## Jouer

```bash
python -m pip install blessed
python engine_gr_19.py                              # IA contre IA sur maps/classic.ano
python engine_gr_19.py maps/vertical.ano human AI   # vous contre l'IA
```

Types de joueur : `human`, `AI`, `remote` (parties entre deux programmes par le réseau, utilisées pour le
tournoi du cours, via `distancemodule.py` fourni par le cours).

## Code

| Fichier | Rôle |
|---|---|
| `engine_gr_19.py` | règles, lecture des cartes, boucle des tours, plateau dessiné dans le terminal avec `blessed` (nourriture en emoji, barres de santé) |
| `ai_engine_gr_19.py` | l'IA : elle envoie la meute sur l'alpha adverse et son propre alpha vers la meilleure nourriture proche quand son énergie passe sous 80 |
| `ai_dumb_gr_19.py` | une IA au hasard, pour tester la vraie |
| `maps/*.ano` | taille du plateau, positions de départ, nourriture |

Le code est resté tel qu'il a été rendu (commentaires en français, nommage imposé par le cours), à part un
point d'entrée en ligne de commande ajouté en 2026 pour pouvoir le lancer sans le serveur du tournoi.
