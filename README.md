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

To solve the first two problems i used a **Simulated Annealing (SA)** metaheuristic, while to solve the last one i used a simpler hill climbing approach.
