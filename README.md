# cheese
This project aims to solve an optimization problem for a cheese supply chain using different optimizations.
The main methods used are bio-inspired optimizations, done by using already implemented libraries.

# Model
The initially proposed model aims to simplify an already established optimization model *(not shown here)* in the framework of this project.
The variables defined for this model are the following sets:

| **Variable** | **Description**        |
|--------------|------------------------|
| $cacopios$   | Collection centers set |
| $clientes$   | Clients set            |
| $productos$  | Products set           |

Every collection center has a defined inventory `capacity`, this capacity $` stock `$ represents the current cheese capacity of that center given on a consistent unit.
The stock has a defined **cost per unit**, $` price `$.
Each collection center also has a set transport cost to that client,  

## Schema
The $` n `$ collection centers are represented as a vector, each with a defined quantity $` x `$.
The quantity for the $`i`$th position represents the amount of the total demand $` D `$ that collection center $` j_i `$ is going to supply.

$$
\begin{array} {|r|r|r|r|r|r|}
    \hline x_0 & x_1 & x_2 & x_3 & \cdots & x_n \\
    \hline
\end{array}
\quad \therefore \quad x_i = cacopios_i
$$

## Objective function
Minimize the total costs for the supply chain

$$
\begin{align*}
Min(f(x)) &= \sum_{i=0}^{n} \left(cacopios_i \times price_i \right) + transport_i 
\end{align*}
$$

where

$$
\begin{align*}
\sum_{i=0}^{n} x_i &= D \\
x_i &\leq stock_i
\end{align*}
$$

This function operates within the restrictions above


