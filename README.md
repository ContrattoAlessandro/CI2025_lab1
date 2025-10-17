# Multidimensional Multiple Knapsack Problem (MMKP)

This repository provides a **Simulated Annealing (SA)** implementation to solve the **Multidimensional Multiple Knapsack Problem (MMKP)**.

## Problem Description

The MMKP is defined as follows:

* You have a set of **items**, each with:

  * a **value**
  * a set of **weights** corresponding to different dimensions (e.g., physical weight, volume, size)
* You also have several **knapsacks**, each with its own **capacity constraints** for all dimensions.

**Objective:** Assign items to knapsacks to **maximize the total value** of selected items while ensuring that no knapsack exceeds its capacity constraints in any dimension.

---

## Simulated Annealing Approach

The algorithm uses a **Simulated Annealing (SA)** metaheuristic:

* Inspired by the **physical process of annealing**, where a material is heated and slowly cooled.
* Gradually explores the solution space, **occasionally accepting worse solutions** to escape local optima.
* The probability of accepting worse solutions decreases as the **temperature** decreases.

---

## Algorithm Overview

### 1. Initialization

* The algorithm starts with a **random initial solution**.
* Each item is either:

  * Assigned to a knapsack, or
  * Left unassigned (denoted by `-1`).
* The **initial fitness** of this configuration is evaluated.

---

### 2. Evaluation Function

The `evaluate(solution)` function computes:

* The **total value** of assigned items
* The **load** of each knapsack across all dimensions
* A **penalty** for constraint violations (proportional to the amount by which capacities are exceeded)

---

### 3. Neighborhood Generation

* A new candidate solution is generated using the `tweak()` function:

  * Randomly **removes, reassigns, or swaps items**
  * The number of modifications is controlled by a **strength parameter**
* This introduces **controlled randomness** to explore neighboring solutions.

---

### 4. Acceptance Criterion

* If the new solution is **better** than the current one, it is **always accepted**.
* If it is **worse**, it may still be accepted with probability:

[
P = e^{-\Delta f / T}
]

Where:

* ( \Delta f ) = decrease in fitness
* ( T ) = current temperature

This allows the algorithm to escape **local optima** in early stages.

---

### 5. Cooling Schedule

* The **temperature decreases gradually** during the search.
* Typically, every fixed number of iterations, the temperature is **multiplied by a cooling coefficient**.
* This balances **exploration** (high temperature) with **exploitation** (low temperature).

---

### 6. Best Solution Tracking

* Any **feasible solution** (with zero penalty) that improves upon the previous best is recorded.
* Ensures that the algorithm always returns the **best valid solution**.

---

### 7. Termination

* After a fixed number of iterations (`MAX_STEPS`), the algorithm returns:

  * The **best feasible solution**
  * Its **total value**
  * Any **penalty** (should be zero)
  * Fitness
  * **Performance ratio** relative to the theoretical maximum value

---

## Algorithm Flow Summary

```text
Generate random initial solution
        ↓
Evaluate initial fitness
        ↓
Repeat for MAX_STEPS iterations:
        ↓
  Generate new candidate (tweak)
        ↓
  Evaluate candidate fitness
        ↓
  If better → accept
  If worse → accept with probability e^(-Δf/T)
        ↓
  Gradually decrease temperature
        ↓
Return the best feasible solution found
```

---

This README explains the structure, steps, and logic of the Simulated Annealing approach for MMKP.

---

Se vuoi, posso anche scrivere **una versione ancora più "GitHub-friendly"** con badge, requisiti Python, e snippet di esempio per eseguire il codice. Vuoi che lo faccia?
