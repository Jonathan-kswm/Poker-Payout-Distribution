# 🃏 Poker Payout Distribution Tool

A desktop application for poker tournament organisers to visualise prize pool distributions, compare payout models, and calculate fair chop deals between remaining players.

---

## Overview

Running a poker tournament involves two tricky problems: deciding how to distribute the prize pool across paid places, and fairly splitting the remaining prize pool when players agree to "chop" at the final table. This tool tackles both.

The **Prize Pool Visualiser** lets you experiment with four different mathematical payout distribution models and instantly see the results as a bar chart. The **Chop Calculator** then lets you calculate a fair deal for remaining players using either a stack-size proportional chop or a full ICM (Independent Chip Model) calculation.

---

## Features

**Prize Pool Visualiser**
- Four selectable payout distribution models (see below)
- Live bar chart rendered with Matplotlib
- Configurable prize pool, number of paid places, 1st place percentage, and slope
- Itemised payout breakdown with running total and difference from prize pool
- Quick percentage calculator to convert a target cash amount into a percentage of the prize pool

**Chop Calculator**
- Supports any number of players with custom names, stack sizes, and payout structures
- Two chop methods: Stack Size Chop and ICM Chop
- Results displayed in a clean text panel within the popup window

---

## Distribution Models

All four models accept a prize pool total, number of paid places, and a first-place percentage as inputs. Where they differ is in *how steeply* the payouts fall off down the field.

**Distribution 1 — Geometric Decay** multiplies each successive payout by a fixed slope factor (default 0.5), so each place earns a fixed proportion of what the place above it earned. This produces a steep curve that heavily rewards the top finishers.

**Distribution 2 — Recursive Remainder** awards the first-place percentage of the *remaining* prize pool at each step. The pool shrinks after each payout is deducted, naturally producing diminishing returns without an explicit slope.

**Distribution 3 — Linear Step-Down** subtracts a fixed percentage increment (default 5%) from the winning percentage at each place. The drop-off is consistent and predictable across all paid positions.

**Distribution 4 — Uniform Step-Down** automatically calculates the step size as `1 / number of places`, ensuring the percentages evenly span the field regardless of how many places are paid.

---

## Chop Methods

**Stack Size Chop** guarantees every remaining player their minimum payout (the lowest prize on the payout schedule), then distributes the remaining prize pool proportionally to each player's chip stack. It is simple, transparent, and easy to explain at the table.

**ICM Chop** uses the Independent Chip Model to calculate each player's expected monetary value based on their probability of finishing in each remaining position. For each player, it sums the probability-weighted value of every possible finishing position. These probabilities are calculated by iterating over all permutations of finishing orders, making ICM mathematically precise but computationally heavier for large fields. It is the industry-standard method for final-table deal negotiations.

---

## Requirements

- Python 3.8+
- `tkinter` (usually bundled with Python)
- `matplotlib`
- `pandas`

Install the dependencies with:

```bash
pip install matplotlib pandas
```

---

## Running the App

```bash
python poker_payout.py
```

The main window will open with the Prize Pool Visualiser on the right and controls on the left. Click **Open Chop Calculator** to launch the deal-making tool in a separate window.

---

## Usage

1. Enter your **Prize Pool**, **Places Paid**, **1st Place %**, and **Slope** in the left panel.
2. Select a **Distribution Type** from the dropdown.
3. Click **Generate Chart** to render the bar chart and see the itemised payouts.
4. Use the **Quick Percentage Calculator** to find what percentage of the prize pool a specific cash target represents.
5. For end-of-tournament deals, click **Open Chop Calculator**, enter player names, their current chip stacks, and the remaining payouts, then select ICM or Stack Size chop and click **Calculate Chop**.

---

## Project Structure

```
poker_payout.py    # Single-file application containing all logic and the GUI
```

---

## Acknowledgements

GUI layout assisted with ChatGPT. ICM probability calculations implemented using Python's `itertools.permutations` for exact combinatorial evaluation.
