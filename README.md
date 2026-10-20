# Factorio modular designer

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/bhedelius/factorio-modular-designer/blob/main/factorio_modular_designer.ipynb)

Diagrams of the items per second and machines required to make a product in Factorio, so that builds can be planned as self-contained modules.

![Chemical science pack production graph](examples/chemical-science-pack.png)

Each node shows the product on top of the machine that makes it. The number in the top right is the production rate in items per second and the number in the bottom right is how many machines are needed. Raw materials are drawn without a machine, since they are supplied from outside the module. When an ingredient feeds more than one product, each arrow is labeled with the items per second flowing along it. An ingredient with a single consumer leaves the arrow unlabeled, since its icon already shows that rate.

![Electronic circuit production graph](examples/electronic-circuit.png)

Recipes with several outputs work too. Outputs that nothing in the diagram consumes hang off the machine as leftovers with their rates, here heavy and light oil from advanced oil processing feeding plastic:

![Plastic from advanced oil processing](examples/plastic-bar.png)

## Usage

The whole tool is the notebook `factorio_modular_designer.ipynb`, laid out as two form cells. Open it in Colab with the badge above:

1. Run **Setup** once. It picks the dataset, `2.0` for the base game or `spa` for Space Age, and loads recipes, machines, modules, and icons.
2. Fill in **Design** and run it: product, items per second, preferred machines, and modules. Everything is named as in the game, so type "Chemical science pack" rather than an internal id. Picking "All science packs" as the product draws every science pack instead. The diagram appears under the cell and is saved to `output/`.
3. Under the Design cell, raw materials are chosen in a searchable picker, and any item in the diagram with more than one recipe gets a dropdown. The diagram redraws on each change.

Machines are chosen per recipe from a comma-separated preference list, defaulting to the dataset's upgraded preset (electric mining drill, electric furnace, assembling machine 3). A recipe that none of the preferred machines can run uses its most advanced producer. Two module dropdowns cover mixed loadouts: the secondary module takes its count of slots in each machine and the primary module fills the rest. Productivity modules are only applied where the game allows them, and machines with built-in productivity such as the foundry include it.

To run it locally instead:

```bash
python -m venv .venv && .venv/bin/pip install -r requirements.txt
brew install graphviz   # or apt install graphviz; the dot binary is required
```

Outside Colab the form fields are plain variables at the top of each cell. The code is hidden in Colab behind the "Show code" toggle.

## Data

All game data comes from [FactorioLab](https://github.com/factoriolab/factoriolab)'s published datasets: one JSON file per game version with items, recipes and their producers, machine speeds and module slots, module effects, and a sprite sheet of icons. Nothing about the game is hardcoded in the notebook, so a new game version or the Space Age expansion is a dataset switch. The Setup cell prints the game version the dataset was built from.

## Limitations

- Beacons, quality, and mining productivity research are not modeled.
- Recipes are chosen per item, not balanced: picking advanced oil processing for petroleum gas shows the heavy and light oil as leftovers rather than cracking them.
- One module loadout applies to every machine.
- Machine counts are shown unrounded so you can choose how to round them.

The `blueprints/` directory holds Factorio blueprint strings for builds designed from these diagrams. `notes.txt` is a running list of planned work.
