
# HGS-CVRP: A modern implementation of the Hybrid Genetic Search for the CVRP

This is a modern implementation of the Hybrid Genetic Search (HGS) with Advanced Diversity Control of [1], specialized to the Capacitated Vehicle Routing Problem (CVRP).

The C++ code of this algorithm has been designed to be transparent, specialized, and extremely concise, retaining only the core elements that make this method a success.
Beyond a simple reimplementation of the original algorithm, this code also includes speed-up strategies and methodological improvements learned over the past decade of research and dedicated to the CVRP.
In particular, it relies on an additional neighborhood called SWAP* which consists in exchanging two customers between different routes without an insertion in place.

## References

When using this algorithm (or part of it) in derived academic studies, please refer to the following works:

[1] Vidal, T., Crainic, T. G., Gendreau, M., Lahrichi, N., Rei, W. (2012). 
A hybrid genetic algorithm for multidepot and periodic vehicle routing problems. Operations Research, 60(3), 611-624. (Available [HERE](https://w1.cirrelt.ca/~vidalt/papers/HGS-CIRRELT-2011.pdf) in technical report form).

[2] Vidal, T. (2020). Hybrid genetic search for the CVRP: Open-source implementation and SWAP* neighborhood. Technical Report PUC-Rio (Under Review -- Available [HERE](https://w1.cirrelt.ca/~vidalt/papers/HGS-CVRP-2020.pdf) in technical report form).

## Scope

This code has been designed to solve the ``canonical'' Capacitated Vehicle Routing Problem (CVRP).
It can also directly handle asymmetric distances and eventual duration constraints (see LocalSearch.h for the calculation of duration values).

This version of the code has been designed and calibrated for medium-scale instances with up to 1,000 customers. 
It is **not** designed in its current form to run very-large scale instances (e.g., with over 5,000 customers), as this requires additional solution strategies (e.g., decompositions and additional neighborhood limitations).
If you need to solve problems that are outside of the scope of this algorithm, do not hesitate to contact me at <vidalt@inf.puc-rio.br>.

## Running the algorithm

* Enter the Program directory: `cd Program`
* Run the make command: `make test`
* Try another example: `./genvrp ../Instances/CVRP/X-n157-k13.vrp mySolution.sol -seed 1 -t 30`

The following options are supported:
```
Usage:
  ./genvrp instancePath solPath [-it nbIter] [-t myCPUtime] [-bks bksPath] [-seed mySeed] [-veh nbVehicles]
Available options:
  -it           Sets a maximum number of iterations without improvement. Defaults to 20,000
  -t            Sets a time limit in seconds. If this parameter is set, the code will be restart iteratively until the time limit
  -bks          Sets an optional path to a BKS in CVRPLib format. This file will be overwritten in case of improvement 
  -seed         Sets a fixed seed. Defaults to 0     
  -veh          Sets a prescribed fleet size. Otherwise a reasonable UB on the the fleet size is calculated
```

## Code structure

The code structure is documented in [2] and organized in the following manner:
* **Individual**: Represents an individual solution in the genetic algorithm, also provide I/O functions to read and write individual solutions in CVRPLib format.
* **Population**: Stores the solutions of the genetic algorithm into two different groups according to their feasibility. Also includes the functions in charge of diversity management.
* **Genetic**: Contains the main procedures of the genetic algorithm as well as the crossover.
* **LocalSearch**: Includes the local search functions, including the SWAP* neighborhood.
* **LocalSearch**: A small code used to represent and manage arc sectors (to efficienty restrict the SWAP* neighborhood).
* **Params**: Stores the method parameters, instance data and I/O functions.
* **Commandline**: Reads the line of command.
* **Solver**: Contains all of the HGS algorithm's population mechanisms.
* **main**: Main code to start the algorithm.

## Contributing

Thank you for your interest in this code.
Your help is welcome to maintain and improve this code.
Before any major pull request or contribution, I recommend to contact me by email at <vidalt@inf.puc-rio.br>.

The goal of this code is to stay **simple** and **specialized** to the CVRP. 
Therefore, contributions that aim to extend this approach to different variants of the vehicle routing problem should usually remain in a separate repository.
Similarly, contributions that require additional libraries are usually not recommended to ensure portability.

There are two main types of contributions:
* Changes that do not impact the sequence of solutions found by the HGS algorithm when running `make test` or testing other instances with a fixed seed. This is visible by comparing the average solution value in the population and diversity through a test run.
Such contributions include refactoring, simplification and code optimization. In this case, please attach the new log obtained before and after your changes. Pull requests of this type are likely to be integrated more quickly.
* Changes that impact the sequence of solutions found by the algorithm when running `make test`. 
In this case, I recommend to contact me beforehand and to provide a detailed description of the changes, with detailed results on 10 runs of the algorithm on each of the 100 instances of Uchoa et al. (2017) with the same termination criterion as used in [2], before and after the changes.

If your contribution involves some components that impact the sequence of solutions, and other that do not impact it, then I recommend to make two separate pull requests to facility review of these changes.

## License

[![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)

- **[MIT license](http://opensource.org/licenses/mit-license.php)**
- Copyright(c) 2020 Thibaut Vidal




