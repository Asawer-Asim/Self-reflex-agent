# Simple Reflex Vacuum Cleaner Agent

A small Python demo of a **simple reflex agent** in the classic **two-square vacuum world** (from *Artificial Intelligence: A Modern Approach* by Russell & Norvig).

## Overview

The world has two locations, **A** and **B**. Each location is either Clean (`0`) or Dirty (`1`). A vacuum agent lives in this world and decides what to do using **only its current percept**: its location and whether that location is dirty. It has no memory of past states.

## Components

### `VacuumEnvironment`
Models the world.

| Member | Description |
|---|---|
| `status` | Dictionary with the state of each square, e.g. `{'A': 1, 'B': 0}` |
| `agent_location` | Where the agent currently is (`'A'` or `'B'`) |
| `percept()` | Returns `(location, status_of_that_location)` |
| `execute(action)` | Applies an action: `Suck`, `Left`, or `Right` |

By default, the initial state is randomized.

### `reflex_vacuum_agent(percept)`
The agent function, built from simple condition-action rules:

| Condition | Action |
|---|---|
| Current square is dirty | `Suck` |
| Clean and at `A` | `Right` |
| Clean and at `B` | `Left` |

## Actions

- `Suck` – cleans the current square
- `Left` – moves the agent to `A`
- `Right` – moves the agent to `B`

## Performance Measure

| Event | Score |
|---|---|
| Cleaning a square (`Suck`) | +10 |
| Moving (`Left` / `Right`) | -1 |

## How to Run

Requires Python 3 (no external libraries).

```bash
python vacuum_agent.py
```

## Example Output

The demo starts with both squares dirty and the agent at `B`:

```
Initial state : {'A': 1, 'B': 1} | Agent at B
Step 1: percept=('B', 1) -> action=Suck  | world={'A': 1, 'B': 0}
Step 2: percept=('B', 0) -> action=Left  | world={'A': 1, 'B': 0}
Step 3: percept=('A', 1) -> action=Suck  | world={'A': 0, 'B': 0}
Step 4: percept=('A', 0) -> action=Right | world={'A': 0, 'B': 0}
Final state   : {'A': 0, 'B': 0}
Performance score: 18
```

Score: +10 (Suck) − 1 (Left) + 10 (Suck) − 1 (Right) = **18**.

## Key Concepts

- **Simple reflex agent**: chooses actions based only on the current percept, ignoring history.
- **Limitation**: once both squares are clean, the agent keeps moving back and forth, wasting effort (-1 each move). A model-based agent with memory could stop (`NoOp`) when everything is clean.

## Possible Extensions

- Add a `NoOp` action and a model-based agent that remembers cleaned squares
- Add a penalty per time step, or make dirt reappear randomly
- Extend the world to more than two squares
