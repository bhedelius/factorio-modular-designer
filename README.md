# Factorio modular designer

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/bhedelius/factorio-modular-designer/blob/main/factorio_modular_designer.ipynb)

Diagrams of the items per second and machines required to make a product in Factorio, so that builds can be planned as self-contained modules.

![Chemical science pack production graph](examples/chemical-science-pack.png)

Each node shows the product on top of the machine that makes it. The number in the top right is the production rate in items per second and the number in the bottom right is how many machines are needed. Items declared as raw materials are drawn without a machine, since they are supplied from outside the module. When an ingredient feeds more than one product, each arrow is labeled with the items per second flowing along it. An ingredient with a single consumer leaves the arrow unlabeled, since its icon already shows that rate.

![Electronic circuit production graph](examples/electronic-circuit.png)

## Usage

The whole tool is the notebook `factorio_modular_designer.ipynb`, laid out as two form cells. Open it in Colab with the badge above:

1. Run **Setup** once. It installs dependencies and downloads recipe and icon data for the chosen Factorio version.
2. Fill in **Design** and run it: product, items per second, assembler and furnace tiers, modules, and an option to draw every science pack at once. The diagram appears under the cell and is saved to `output/`.
3. Raw materials are chosen in a searchable picker under the Design cell. Type to search, press Enter to add, click a tag to remove, and the diagram redraws on each change.

Two module dropdowns cover mixed loadouts: the secondary module takes its count of slots in each machine and the primary module fills the rest, so "productivity 3 primary, speed 3 secondary, count 1" means three productivity and one speed module in an assembling machine 3. Productivity modules are only applied to recipes the game allows them on, using the `allow_productivity` flag in the recipe data; those slots stay empty elsewhere.

To run it locally instead:

```bash
python -m venv .venv && .venv/bin/pip install -r requirements.txt
brew install graphviz   # or apt install graphviz; the dot binary is required
```

Outside Colab the form fields are plain variables at the top of each cell. The code is hidden in Colab behind the "Show code" toggle.

Recipe data is read from the [factorio-data](https://github.com/wube/factorio-data) repository at the pinned version and icons from [icons-factorio](https://github.com/deniszholob/icons-factorio), so nothing from the game needs to be installed.

## Limitations

- Recipes with more than one output (oil processing, uranium processing, Kovarex enrichment) and recipes whose output is named differently from the recipe (cracking, solid fuel, nuclear fuel reprocessing) are skipped. Their products, such as petroleum gas and solid fuel, therefore behave as raw materials.
- Beacons are not modeled, and all machines of a kind share one module choice.
- Machine counts are shown unrounded so you can choose how to round them.

The `blueprints/` directory holds Factorio blueprint strings for builds designed from these diagrams. `notes.txt` is a running list of planned work.
