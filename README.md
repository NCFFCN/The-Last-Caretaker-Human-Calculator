# The Last Caretaker Human Calculator

A small CLI tool for solving lineage-style profession combinations in **The Last Caretaker**. It reads profession, food, memory, and inventory CSV files, then uses an integer linear optimization model to search for a valid item combination for a target profession while avoiding unwanted collateral professions.

## CSV Files

- Human data: `Human.csv` or `human.csv` or `Humans.csv` or `humans.csv`.
- Food data: `Food.csv` or `food.csv` or `Foods.csv` or `foods.csv`.
- Memory data: `Memory.csv` or `memory.csv` or `Memories.csv` or `memories.csv`.
- Inventory data: `Inventory.csv` or `inventory.csv` or `Inventories.csv` or `inventories.csv`.

## Requirements

Install the required Python packages:

```bash
pip install -r requirements.txt
```

The current dependency list includes `numpy`, `pandas`, and `pulp`.

## Usage

Run the calculator from the project folder:

```bash
python main.py
```

At the prompt, you can:

- Enter a profession name such as `Guardian of Humanity T4` or `Guardian of Humanity`.
- Enter multiple targets separated by commas, for example: `Guard T2, Site Guardian T3` or `Guard, Site Guardian`.
- Type `list` to show all available professions grouped by category.
- Type `q` to quit the program.

Example:

```text
Enter Target Profession (or 'list' to see all, 'q' to quit): Guard T2
```
```text
Enter Target Profession (or 'list' to see all, 'q' to quit): Guard, Site Guardian
```
```text
請輸入目標職業 (或輸入「list」查看全部, 輸入「q」退出): 量子工程師
```

Note: Profession name should be entered in the display language set in `main.py` (English, Traditional Chinese, or Simplified Chinese).

## Search logic

The solver prioritizes:

1. Lower priority cost
2. Fewer total items
3. Less excess stats
4. Fewer rejected collateral professions

## Search Settings

The search behavior is controlled directly in `main.py`:

- `UNLIMITED_SEARCH = False` means the solver stops after a limited number of attempts.
- `MAX_ATTEMPTS = 20` defines the maximum number of search attempts when unlimited search is disabled.
- `PRIORITY_WEIGHT` and `ITEM_COUNT_WEIGHT` control how strongly the solver prefers lower-priority-cost and lower-item-count solutions.
- `BIG_M` is used for exclusion constraints when rejecting failed collateral-profession combinations.

## Inventory Settings

The inventory update behavior is also controlled in `main.py`:

- `DEDUCT_INVENTORY = False` means successful combinations do not modify the inventory file.
- `SAVE_AS_NEW_FILE = True` means that when inventory deduction is enabled, the updated inventory is saved to a new timestamped CSV file instead of overwriting the original file.

The loader also supports filename variations such as `Inventory.csv` and `inventory.csv`, as well as similar case variations for other CSV inputs.

## Language Support

The display language is controlled by the `LANG` setting in `main.py`:

- `"en"` for English.
- `"tc"` for Traditional Chinese.
- `"sc"` for Simplified Chinese.

All translated text are defined in `translations.py`.

## Notes

- Only items available in the inventory file are considered by the solver.
- The stat list is defined by `ALL_STAT_COLS`, so the CSV headers and code must stay aligned for correct matching.
- Profession name input supports translated names and partial matching without requiring the tier suffix in some cases.

## AI Disclaimer

This project was created with the assistance of AI tools.****