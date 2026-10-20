# Factorio modular designer

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/bhedelius/factorio-modular-designer/blob/main/factorio_modular_designer.ipynb)

Diagrams of the items per second and machines required to make a product in Factorio, so that builds can be planned as self-contained modules.

![Chemical science pack production graph](examples/chemical-science-pack.png)

Each node shows the product on top of the machine that makes it. The number in the top right is the production rate in items per second and the number in the bottom right is how many machines are needed. Items declared as raw materials are drawn without a machine, since they are supplied from outside the module. Each arrow is labeled with the items per second flowing from an ingredient to the product that consumes it.

![Electronic circuit production graph](examples/electronic-circuit.png)

## Usage

The whole tool is the notebook `factorio_modular_designer.ipynb`. Open it in Colab with the badge above, fill in the **Settings** form (product, rate, assembler and furnace tiers, raw materials), and choose Runtime > Run all. The diagram appears inline and is saved under `output/`. The optional last cell draws every science pack with the same settings.

To run it locally instead:

```bash
python -m venv .venv && .venv/bin/pip install -r requirements.txt
brew install graphviz   # or apt install graphviz; the dot binary is required
```

Outside Colab the form cells are plain code, so edit the variables at the top of the Settings cell. The code in every cell is hidden in Colab behind the "Show code" toggle.

Recipe data is read from the [factorio-data](https://github.com/wube/factorio-data) repository at the pinned version and icons from [icons-factorio](https://github.com/deniszholob/icons-factorio), so nothing from the game needs to be installed.

## Limitations

- Recipes with more than one output (oil processing, uranium processing, Kovarex enrichment) and recipes whose output is named differently from the recipe (cracking, solid fuel, nuclear fuel reprocessing) are skipped. Their products, such as petroleum gas and solid fuel, therefore behave as raw materials. Each skipped recipe is logged as a warning.
- Modules and beacons are not modeled.
- Machine counts are shown unrounded so you can choose how to round them.

The `blueprints/` directory holds Factorio blueprint strings for builds designed from these diagrams. `notes.txt` is a running list of planned work.
