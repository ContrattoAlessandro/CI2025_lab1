The Multidimensional Multiple Knapsack Problem (MMKP)
There is a set of items, each characterized by a value and a set of "weights" corresponding to different dimensions (e.g., physical weight, volume, or size). We also have several knapsacks, each with its own capacity constraints in those same dimensions.

The objective is to assign items to knapsacks in order to maximize the total value of the selected items, while ensuring that no capacity constraint is violated.

The Simulated Annealing Approach
To tackle this problem, i implemented a Simulated Annealing (SA) metaheuristic. SA is inspired by the physical process of annealing, where a material is heated and then slowly cooled. In the optimization context, this analogy translates into a gradual exploration of the solution space, where the algorithm can occasionally accept worse solutions to escape local optima, progressively reducing such acceptance as the “temperature” decreases.

Algorithm Overview
Initialization The algorithm starts with a randomly generated solution. Each item is either:

assigned to one of the available knapsacks, or
left unassigned (represented by -1). The fitness of this initial configuration is evaluated using a custom evaluation function.
Evaluation Function The function evaluate(solution) computes:

the total value of the assigned items;
the load of each knapsack across all dimensions;
a penalty for constraint violations, proportional to the amount by which any capacity limit is exceeded.
Neighborhood Generation A new candidate solution is created by applying the tweak() function, which randomly modifies the current configuration. Specifically, one or more items (depending on a parameter strength) are reassigned to a different knapsack or marked as unassigned. This introduces controlled randomness to explore neighboring regions of the search space.

Acceptance Criterion Once the new solution is evaluated, it is compared with the current one:

If the new fitness is higher, the solution is always accepted.
If it is lower, it may still be accepted with a probability: e^(-Δf/T) where (Δf) is the fitness loss and (T) is the current temperature. This probabilistic acceptance allows the algorithm to escape local optima during early stages.
Cooling Schedule The temperature decreases gradually as the search progresses. Every 200 iterations, the temperature is multiplied by a coefficient. This cooling schedule balances exploration (at high temperatures) and exploitation (at low temperatures).

Best Solution Tracking Throughout the optimization process, any feasible solution (with zero penalty) that outperforms the previous best is recorded as the best valid solution.

Termination After a fixed number of iterations (MAX_STEPS), the algorithm returns the best feasible solution found, along with its total value, penalty, fitness, and performance ratio with respect to the theoretical maximum achievable value.

Algorithm Flow Summary
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
