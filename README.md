# Metaheuristic Optimization Project (CS467)
This project implements and compares two metaheuristic algorithms, Simulated Annealing (SA), and Genetic Algorithm (GA) to solve the Traveling Salesman Problem (TSP).  

# A. Requirements & Installation

This project was developed and executed entirely using **Google Colab**, so no local installation is required.

To run Simulated Annealing (SA) or Genetic Algorithm (GA):

1. Open the corresponding Colab notebook.
2. Upload the dataset file (e.g., berlin52.tsp) when required.
3. Run all cells in the notebook in order.

No additional setup, package installation, or environment configuration is needed beyond what Google Colab provides by default.

# B. Dataset & Experimental Setup

### B.1 Dataset Description
Both algorithms use the **berlin52** dataset from **TSPLIB**, which contains the coordinates of 52 cities.  
These coordinates are converted into a distance matrix and used to evaluate the total length of each TSP tour.

We intentionally used the **same dataset** for all experiments to ensure a fair comparison between SA and GA.

---

### B.2 Dataset Loading Methods

In this project, we used **two different methods** to load the same dataset:

#### **A. SA Dataset Loading (from Kaggle)**
For the SA notebook, the berlin52 dataset was imported **directly from an online Kaggle source** inside Google Colab.  
The file is loaded automatically without requiring any manual download.

#### **B. GA Dataset Loading (manual upload)**
For the GA notebook, the dataset was **downloaded locally** and then **uploaded manually into Google Colab**.  

This demonstrates that both algorithms can work with datasets loaded online or manually.


# 1. Simulated Annealing (SA)

## 1.1 **Overview**

This project addresses the Traveling Salesman Problem (TSP) using Simulated Annealing (SA) as the main metaheuristic algorithm, enhanced with two improvement methods:

- 2-OPT Local Search (integrated inside the Simulated Annealing loop to improve every accepted solution)

- Tabu Search Improvement (applied after SA)

The notebook includes full implementation, visualization, comparisons and optional user input.


# 1.3 **Run the Algorithms**

**A. Run Simulated Annealing**

This is the main optimization algorithm in the project.

It generates the initial solution used by all improvement methods.

SA features:

*   Random initial route
*   Neighbor generation
*   Cooling schedule
*   Accepting worse moves to escape local minima
*   Produces a complete TSP tour

Outputs:
*   SA Best Distance
*   SA Best Route
*   Convergence plot

Robustness:

To evaluate the robustness of Simulated Annealing, multiple initial temperatures (T0 = 100, 200, 300) were tested.
Each temperature was executed for five independent runs to measure consistency.
Robustness was evaluated using the standard deviation of the results.
A lower standard deviation indicates a more stable configuration.
Based on the experiments, T0 = 100 provided the most robust performance and was selected for the remaining analysis.

**B. Run Tabu Search**

Tabu Search is used as an improvement AFTER Simulated Annealing.

It starts from SA’s best route:

best_route_tabu, best_distance_tabu, evolution_tabu = tabu_improve(best_route_sa, coords)

Outputs:
- Tabu-improved distance
- Improved route
- Tabu convergence curve
- Route visualization

**C. 2-OPT Local Search**

2-OPT is a local improvement algorithm applied after Simulated Annealing.
It removes crossing edges and shortens the route.

How it works:
- Takes the SA route as input
- Reverses sub-paths to reduce total distance
- Repeats until no further improvement is possible

Outputs:
- 2-OPT improved distance
- Improved route visualization

**C. Comparison Section**
The notebook compares:

- SA only
- SA + 2-OPT
- SA + Tabu

It prints all distances and identifies which method is best.
A bar chart is also generated.

# **4. User Input **

The user can enter the number of cities and then enter x,y coordinates for each city.
The program then runs SA, SA+2OPT and SA+Tabu on the user’s data.

# **5. Outputs**

The notebook displays:

Best route (for SA, SA+2opt, SA+Tabu)

Best distances

Convergence curves

2D route visualizations

Comparison plots

"""

---

# 2. Genetic Algorithm (GA)

## 2.1 **Overview**

The Genetic Algorithm (GA) is a **population-based evolutionary optimization method** inspired by natural selection.  
Instead of working on one solution like SA, GA evolves a **population** of candidate routes across generations.

GA uses:

- **Selection**
- **Ordered Crossover**
- **Mutation**
- **Replacement**

The process gradually improves tour quality until a near-optimal route is found.

---

## 2.3 **Run the Algorithm**

**A. Run Genetic Algorithm**

GA features:

*   Random initial population  
*   Fitness evaluation based on route distance  
*   Tournament selection  
*   Order-based crossover  
*   Swap mutation  
*   Produces a complete TSP tour  

Outputs:

*   GA Best Distance  
*   GA Best Route  
*   Convergence plot  

Robustness:

To improve the reliability of GA results, different parameter combinations  
(population size, mutation rate, generations) can be tested.  
Stable configurations can be chosen based on consistent performance across runs.

---

## 2.4 Parameter Fine-Tuning

To improve the performance and stability of the Genetic Algorithm, several parameter combinations were tested.  
The tuning process focused on identifying configurations that consistently produced strong solutions across multiple runs.

The following GA parameters were varied during experimentation:

- Population Size (e.g., 30, 50, 80)
- Number of Generations (e.g., 200, 300, 500)
- Mutation Rate (e.g., 0.01, 0.02, 0.05)
- Crossover Rate
- Tournament Size

Each parameter set was executed multiple times to evaluate consistency.  
Performance was assessed based on:

- Best distance achieved
- Average performance
- Stability across repeated runs

Through fine-tuning, parameter values that provided **more reliable and higher-quality solutions** were selected for the final GA configuration used in this project.

---

## 2.5 **Outputs**

The GA implementation displays:

- Best route  
- Best distance  
- Convergence curve (best fitness per generation)  
- 2D visualization of the final tour  

