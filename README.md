# Quan podem predir el guanyador a League of Legends (solo queue)

**Com de d'hora podem predir quin equip guanyarà una partida rankejada de League of Legends?**

Aquest projecte compara models d'aprenentatge computacional que prediuen el guanyador d'una partida a partir d'estadístiques de joc (or, experiència, morts, objectius) registrades cada 2 minuts, des del minut 10 fins al final. L'objectiu és mesurar com millora la predicció a mesura que avança la partida i trobar el primer moment en què el resultat es pot predir de manera fiable.

Projecte de l'assignatura *Aprenentatge Computacional* (APC), Cas Kaggle 2026.

## Base de dades

- **Origen:** [League of Legends SOLO-Q Ranked Games](https://www.kaggle.com/datasets/bobbyscience/league-of-legends-soloq-ranked-games) (Kaggle, llicència CC0)
- **Contingut:** unes 25.000 partides rankejades de solo queue de nivell Platí, amb una fila per partida cada 2 minuts (242.572 files, 59 columnes)
- **Atribut a predir:** `hasWon`, si l'equip blau ha guanyat la partida
- **Tasca:** classificació binària

Les dades no s'inclouen al repositori per la seva mida. Per reproduir el projecte, descarregueu `lol_ranked_games.csv` des de la [pàgina de Kaggle](https://www.kaggle.com/datasets/bobbyscience/league-of-legends-soloq-ranked-games) i deseu-lo a la carpeta `data/`.

## Metodologia

- Cada partida apareix en diverses files (una per instant de temps), així que totes les particions es fan **agrupant per `gameId`** per evitar *data leakage* entre entrenament i test.
- Les columnes que només es coneixen quan acaba la partida (com `gameDuration`) s'exclouen dels atributs.
- Tot el preprocessament s'ajusta només amb les dades d'entrenament, dins de `Pipeline`s de scikit-learn.
- Es comparen com a mínim quatre models amb validació creuada i una cerca d'hiperparàmetres per a cadascun, respecte a una baseline.
- El conjunt de test s'utilitza una sola vegada, al final, amb el model final ja triat.

## Resultats

*En curs.*

## Estructura del repositori

```
lol-early-win-prediction/
├── data/          # base de dades (no inclosa, vegeu l'apartat Base de dades)
├── notebooks/     # notebooks d'anàlisi i de models
├── README.md
└── requirements.txt
```

## Com executar el projecte

1. Cloneu el repositori:
   ```bash
   git clone https://github.com/adam-perez25/lol-early-win-prediction.git
   cd lol-early-win-prediction
   ```
2. Creeu un entorn virtual i instal·leu les dependències:
   ```bash
   python -m venv .venv
   .venv\Scripts\activate        # Windows
   source .venv/bin/activate     # macOS / Linux
   pip install -r requirements.txt
   ```
3. Descarregueu la base de dades a `data/` (vegeu l'apartat Base de dades).
4. Executeu els notebooks de `notebooks/` en ordre.

Tots els processos aleatoris fan servir una llavor (*seed*) fixada per garantir la reproductibilitat.

## Autors

- El vostre nom (GitHub: [adam-perez25](https://github.com/adam-perez25))

## Declaració d'ús d'IA

*Pendent de completar: quines eines d'IA s'han fet servir i per a què.*