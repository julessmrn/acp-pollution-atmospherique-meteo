# Pollution atmosphérique et météorologie : analyse en composantes principales

Analyse multivariée des liens entre polluants atmosphériques (NO, NO₂, O₃, PM10) et conditions météorologiques à partir de mesures horaires, avec R.

Projet réalisé en binôme avec Antton Goyhetche, dans le cadre du Master Ingénierie des Risques Économiques et Financiers – Economic Risk and Data Sciences (Université de Bordeaux).

## Objectif

Identifier les grandes structures qui relient la pollution de l'air à la météo :
- quels polluants évoluent ensemble ;
- quelles conditions favorisent les épisodes d'ozone ;
- quel rôle jouent le vent et la pluie dans la dispersion des polluants.

## Données

Mesures horaires de 4 polluants et de 8 variables météorologiques (voir `data/README.md`). Le jeu de données a été fourni dans le cadre du cours et n'est pas inclus dans le dépôt.

## Méthodologie

1. **Analyse des corrélations** sur l'ensemble des mesures, puis sur les seules mesures de midi, pour neutraliser le cycle jour/nuit.
2. **Analyse bivariée de l'ozone :** relations avec le NO₂, l'heure, la température et l'humidité, lissées par LOESS.
3. **ACP sur données horaires** (FactoMineR), avec variables centrées-réduites :
   - jeu complet, puis sous-échantillons de midi et de 18 h ;
   - nuage des individus coloré par mois pour faire ressortir la saisonnalité ;
   - repérage d'un groupe d'observations extrêmes dans le plan factoriel et comparaison de leurs moyennes aux moyennes globales.
4. **ACP sur moyennes journalières** avec variables supplémentaires :
   - pollution active et météo projetée en supplémentaire ;
   - puis l'inverse, météo active et pollution en supplémentaire.
5. **Analyse personnelle :** effet du vent et des précipitations sur les polluants primaires (NOx, PM10) et secondaires (ozone), en contrôlant par la température et l'humidité.

## Principaux résultats

- **Le premier axe oppose les polluants du trafic à l'ozone.** NO, NO₂ et PM10 sont fortement corrélés entre eux, tandis que l'ozone s'y oppose, ce qui reflète la destruction de l'O₃ par les oxydes d'azote.
- **Le second axe est météorologique :** il sépare les situations chaudes et sèches des situations fraîches et humides.
- **Les épisodes d'ozone ont un profil très marqué.** Dans le groupe d'observations extrêmes repéré par l'ACP, l'ozone moyen atteint environ 102 contre 50 sur l'ensemble des données, avec une température moyenne de 35 °C contre 13 °C et une humidité de 35 % contre 82 %.
- **La saisonnalité est nette** sur les mesures de midi et plus diffuse à 18 h, quand la photochimie diminue.
- **La météo structure la pollution :** inverser les variables actives et supplémentaires montre que les conditions météorologiques expliquent une large part de la variabilité des polluants.
- **Le vent et la pluie dispersent surtout les polluants primaires.** Ils font baisser NOx et PM10, alors que l'ozone dépend davantage des conditions thermiques et photochimiques.

## Limites

- Le plan factoriel (1,2) n'explique qu'une part modérée de l'inertie totale.
- L'ACP met en évidence des corrélations, pas des liens de causalité.

## Reproduire l'analyse

1. Installer R (version 4.1 ou plus récente) et RStudio.
2. Installer les packages :
   ```r
   install.packages(c("tidyr", "dplyr", "ggplot2", "lubridate", "MASS", "FactoMineR",
                      "corrplot", "factoextra", "plotly", "naniar"))
   ```
3. Placer `ATMO-RDSM2.rda` dans `data/`.
4. Ouvrir `acp_pollution_meteo.Rmd` dans RStudio et cliquer sur **Knit**.

## Structure du dépôt

```
├── acp_pollution_meteo.Rmd   # Analyse complète (R Markdown)
├── projet.css                # Mise en forme du rapport HTML
└── data/
    └── README.md             # Description des données
```

## Outils

R, R Markdown, FactoMineR, factoextra, corrplot, ggplot2, dplyr.

## Auteurs

- **Jules Marin** – [LinkedIn](https://www.linkedin.com/in/jules-marin-64611035a/)
- **Antton Goyhetche**
