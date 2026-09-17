# Mise en forme pour FLOCK

Transforme une matrice de génotypes en disposition FLOCK — un allèle par colonne, prête à rouler.

**→ [Ouvrir l'outil](https://nanoeditionsarcheus-web.github.io/flock-convert/)**

---

## Ce que ça fait

FLOCK attend les génotypes avec **un allèle par colonne** : `SPEC ID`, puis deux colonnes par locus. Or les matrices de travail ont souvent les allèles **collés** (`147167` dans une seule case). Passer de l'un à l'autre à la main — convertir en texte, insérer une colonne par locus, découper au milieu, ajouter les en-têtes — est long et propice aux erreurs de décalage.

Cet outil le fait d'un seul clic. On colle la matrice, on récupère la disposition FLOCK : allèles séparés, données manquantes à `0`, vrais noms de locus en en-tête. Le résultat se copie directement dans le classeur FLOCK ou s'enregistre en CSV.

## Les locus à plus de deux allèles

FLOCK travaille en **diploïde** : deux allèles par locus. Un locus qui en porte trois ou quatre — signature possible d'hybridation ou d'introgression — est donc **développé en ses versions à deux allèles**, chacune sur sa propre ligne.

Par exemple, un individu `1050` dont le locus LAV211 vaut `157161169` ressort en trois versions :

| Identifiant | LAV211 retenu |
|---|---|
| `1050_A` | 157 / 161 |
| `1050_B` | 157 / 169 |
| `1050_C` | 161 / 169 |

Une **légende** accompagne le résultat : pour chaque version développée, elle indique quels allèles ont été retenus, à quels locus — de quoi relire ensuite les sorties de FLOCK sans se perdre.

Deux modes sont offerts :

- **Toutes les combinaisons** (défaut) : énumération exhaustive. Idéal quand un individu n'a qu'un ou deux locus multi-allèles.
- **Tirage aléatoire** : un nombre fixe de versions tirées au hasard par individu. Utile si un individu cumule beaucoup de locus multi-allèles, où l'énumération complète deviendrait trop volumineuse.

## Format des données

Première ligne : l'en-tête — un libellé d'identifiant, puis le nom de chaque locus. Ensuite, une ligne par individu : l'identifiant, puis les génotypes, allèles collés à trois chiffres chacun.

```
NO ind	LAV237	LAV321	LAV336	LAV347	LAV211
1974	147167	168168	188192	169193	169177
1993	155171187	144168	184188	177201	149161
```

Le séparateur de colonnes — tabulation, point-virgule ou virgule — est détecté automatiquement ; un copier-coller depuis Excel fonctionne directement. Les données manquantes sont codées `0` par défaut, et ce code est modifiable. Chaque allèle doit être scoré sur trois chiffres (un allèle inférieur à 100 s'écrit avec un zéro devant, ex. `097`).

## Vos données restent chez vous

Tout le calcul se fait dans le navigateur. Aucune donnée n'est envoyée nulle part : la page est servie une fois, puis fonctionne seule. Le code est lisible en entier dans ce dépôt.

Pour un usage entièrement hors ligne, faites *Enregistrer la page sous* dans votre navigateur, ou téléchargez `index.html` : le fichier fonctionne tel quel, par simple double-clic, sur Mac comme sur PC. Aucune installation n'est requise.

## Origine

Outil conçu pour la démarche d'assignation d'espèce de **Nathalie Tessier** (cinq catostomidés du Québec). La méthode de développement des locus multi-allèles en versions diploïdes s'inspire d'une suggestion de **Pierre Duchesne**, auteur du logiciel FLOCK.

## Écriture

Cet outil a été écrit par **Claude** (Anthropic), dans le cadre d'un échange avec Éleine Leblanc, et vérifié sur des matrices de test réelles.
