# Ising Model 

This repository is primarily for my final undergraduate year thesis on machine learning approaches to the ising model. It will contain multiple useful and efficient algorithms such as Metropolis, as well as pre-built functions for visualizing, creating models and more.

Language: **Python 3**

## Functions & Algorithms

### Fast Metropolis (Markov Chain Monte Carlo) Implementation

Using numba to run certain parts of code, I have achieved roughly x150 speed-up from most numpy implementations found online or in other repos. The algorithm can currently do around 15,000,000 to 30,000,000 MCMC iterations per second on 1 core of a consumer cpu, meaning that even larger systems such as 200x200 can converge within a couple of minutes on 1 CPU core.

Function Name: **mcmc_ising()**

This function is easy to use, example is *mcmc_ising(n = 200, T = 1, nsteps = 2000000)*


### Plots with information

I created a quick function that will produce plots taking in details from the Metropolis function.

Function Name: **plot_ising_array()**

This function takes in the numpy array, the temperature and steps and returns a plot such as:

![low_temperature](https://i.imgur.com/YcN4oWq.png)
![high_temperature](https://i.imgur.com/S1qRJua.png)

Where we can see two systems, one in low temperature and one in high temperature, they are 200x200 with 1 billion MCMC steps.

## The Ising Model

Wikipedia link: https://en.wikipedia.org/wiki/Ising_model

The **Ising Model** is a simple model for describing a magnetic system. It is represented as an n-dimensional lattice, in which the nodes of the lattice have binary values, usually <a href="https://www.codecogs.com/eqnedit.php?latex=\sigma_i&space;\in&space;\{\pm1\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sigma_i&space;\in&space;\{\pm1\}" title="\sigma_i \in \{\pm1\}" /></a> due to the electron spin notation. Each node can then interact only with it's nearest neighbours and if there is a resultant magnetic field, or changes in energy, a node can flip from one state to the other. If enough of these nodes flip and align in one direction we have a resultant magnetic field (ferromagnetism). The Ising Model is the simplest way of describing this process, and is what I investigate in my thesis.

It has been solved in 1-dimension by Ising and 2-dimensions for the isotropic case with no external field by Onsager. 


The energy of such a system is described by the hamiltonian:

<a href="https://www.codecogs.com/eqnedit.php?latex=H(\sigma)&space;=&space;-&space;\sum_{\langle&space;i&space;j&space;\rangle}&space;J_{ij}\sigma_i\sigma_j&space;-&space;\mu\sum_{j}&space;h_j&space;\sigma_j" target="_blank"><img src="https://latex.codecogs.com/gif.latex?H(\sigma)&space;=&space;-&space;\sum_{\langle&space;i&space;j&space;\rangle}&space;J_{ij}\sigma_i\sigma_j&space;-&space;\mu\sum_{j}&space;h_j&space;\sigma_j" title="H(\sigma) = - \sum_{\langle i j \rangle} J_{ij}\sigma_i\sigma_j - \mu\sum_{j} h_j \sigma_j" /></a>

where <a href="https://www.codecogs.com/eqnedit.php?latex=J_{ij}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?J_{ij}" title="J_{ij}" /></a> is the coupling parameter (i,j are adjacent nodes), <a href="https://www.codecogs.com/eqnedit.php?latex=\sigma_{i,j}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sigma_{i,j}" title="\sigma_{i,j}" /></a> is the spin of a node, and <a href="https://www.codecogs.com/eqnedit.php?latex=\mu" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mu" title="\mu" /></a> is an external magnetic field.

Where the Partition function is described by:

<a href="https://www.codecogs.com/eqnedit.php?latex=Z&space;=&space;\sum_{states}&space;e^{-\beta&space;H}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Z&space;=&space;\sum_{states}&space;e^{-\beta&space;H}" title="Z = \sum_{states} e^{-\beta H}" /></a>

where <a href="https://www.codecogs.com/eqnedit.php?latex=\beta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\beta" title="\beta" /></a> is <a href="https://www.codecogs.com/eqnedit.php?latex=\frac{1}{k_B&space;T}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{1}{k_B&space;T}" title="\frac{1}{k_B T}" /></a> where <a href="https://www.codecogs.com/eqnedit.php?latex=k_B" target="_blank"><img src="https://latex.codecogs.com/gif.latex?k_B" title="k_B" /></a> is Botlzmanns constant and T is the temperature of the system.

The probability of being in a specific microstate is then: 

<a href="https://www.codecogs.com/eqnedit.php?latex=p_i&space;=&space;\frac{e^{-\beta&space;\epsilon_i}}{\sum^{N_{states}}_{j=1}e^{-\beta&space;\epsilon_j}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?p_i&space;=&space;\frac{e^{-\beta&space;\epsilon_i}}{\sum^{N_{states}}_{j=1}e^{-\beta&space;\epsilon_j}}" title="p_i = \frac{e^{-\beta \epsilon_i}}{\sum^{N_{states}}_{j=1}e^{-\beta \epsilon_j}}" /></a>
