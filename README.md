# Percolation on networks

An interactive, single-file web demo of the percolation transition on Erdős–Rényi random graphs and scale-free networks, and of why it decides whether an epidemic can spread. It is based on lecture slides by Sang Hoon Lee for an introductory network science course in a physics department, and it is a companion to the lattice percolation demo.

Everything runs in the browser. There is no build step, no server and no dependencies beyond an optional web font.

## Running it

Open `index.html` in any modern browser (Chrome, Edge, Firefox or Safari).

To publish it with GitHub Pages, push this repository, then go to **Settings → Pages**, choose **Deploy from a branch**, and select the branch and the root folder. The page will be served at `https://<user>.github.io/<repository>/`.

## What the page contains

**Live network.** A network of 200 to 500 nodes in one of three modes:

- **Erdős–Rényi G(N, p):** starts from the fully connected graph, and p is the connection probability that characterizes the graph. Each of the N(N − 1)/2 pairs is linked with probability p, from the empty graph at p = 0 to the complete graph at p = 1, and the giant component appears at p<sub>c</sub> = 1/(N − 1). A logarithmic p scale (on by default) spreads out the region near the threshold.
- **Erdős–Rényi, fixed ⟨k⟩:** a fixed Erdős–Rényi network with a chosen mean degree, and p is the chance that each link is kept.
- **Scale-free:** a configuration-model network with a chosen degree exponent γ and minimum degree, and p is the chance that each link is kept.

Each pair or link keeps its own random number, so raising p only adds links, and the components are colored as they form, with the largest in blue. A "Scan through p" button sweeps p over the slider's range at a chosen speed, and a chart under the network plots the largest component of that exact network against p, with the theory for an infinite network, a marker at the current p, and click-or-drag control. The largest component is drawn in blue with a halo and thicker links while the other components are grayed out (or all components can be colored). Readouts show the kept links, mean degree, density, the giant-component share S, the second-largest component, the number of components, the mean size ⟨s⟩ of the other components, and the threshold p<sub>c</sub> = ⟨k⟩/(⟨k²⟩ − ⟨k⟩) of the displayed network. An outbreak button spreads an infection generation by generation along the kept links, from a random node or the biggest hub, and shows that the outbreak fills exactly the first case's component.

**Density and the giant component.** Erdős–Rényi graphs with N = 1 000 to 100 000 nodes, built by adding links one at a time. It plots S and ⟨s⟩ against the mean degree ⟨k⟩ with the exact theory, S = 1 − e<sup>−⟨k⟩S</sup> and ⟨s⟩ = 1/(1 − ⟨k⟩ + ⟨k⟩S). It then measures the mean-field exponents β = 1, γ<sub>p</sub> = 1 and τ = 5/2, and the growth S<sub>max</sub> ∝ N<sup>2/3</sup> of the largest component at ⟨k⟩ = 1.

**Random versus scale-free networks.** Bond percolation on configuration-model scale-free networks and on Erdős–Rényi networks with the same mean degree, for N = 1 000, 10 000 and 100 000. It shows:

- the degree distributions
- S against p, with generating-function theory computed from the simulated degrees
- ⟨s⟩ against p
- the threshold p<sub>c</sub> against N: it stays at 1/⟨k⟩ for random graphs and falls toward zero for 2 < γ < 3, because ⟨k²⟩ grows with the largest hub
- a table of ⟨k⟩, ⟨k²⟩, the largest degree and both threshold estimates

**Epidemics and the vanishing threshold.** An outbreak with transmissibility T is bond percolation with p = T, so random networks have an epidemic threshold while scale-free networks with 2 < γ < 3 effectively do not. A table gives the threshold and the giant-component exponent β for each range of γ.

## Methods

| Topic | Approach |
| --- | --- |
| Components | Union–find with union by size and path halving |
| Curves | Links are added one at a time in random order, so one run covers a whole curve; runs are averaged. |
| Erdős–Rényi graphs | G(N, M): M distinct random pairs, with ⟨k⟩ = 2M/N |
| Scale-free graphs | Configuration model: degrees drawn from p(k) ∝ k<sup>−γ</sup> above a minimum degree, link ends paired at random, self-loops and repeated links removed |
| Theory for S(p) | Generating functions of the simulated degree distribution: u = 1 − p + p G<sub>1</sub>(u), S = 1 − G<sub>0</sub>(u) |
| Mean component size | ⟨s⟩ = Σ′ s² / Σ′ s over all components except the largest |
| Live layout | Force-directed (Fruchterman–Reingold style) on the full network, fixed while p changes |

Measured exponents come close to the theory but not exactly, because the networks are finite. "Add more samples" reduces random noise but not these finite-size effects.

## Files

```
index.html   the complete demo (HTML, CSS and JavaScript in one file)
README.md    this file
```

## Performance

The simulations start shortly after the page loads and run in small chunks, so the page stays responsive. The largest networks (100 000 nodes) take the most time and memory, which matters mostly on phones.

## References

1. P. Erdős and A. Rényi, "On the evolution of random graphs," *Publ. Math. Inst. Hung. Acad. Sci.* **5**, 17 (1960).
2. A.-L. Barabási and R. Albert, "Emergence of scaling in random networks," *Science* **286**, 509 (1999).
3. M. Molloy and B. Reed, "A critical point for random graphs with a given degree sequence," *Random Struct. Algorithms* **6**, 161 (1995).
4. M. E. J. Newman, S. H. Strogatz and D. J. Watts, "Random graphs with arbitrary degree distributions and their applications," *Phys. Rev. E* **64**, 026118 (2001).
5. D. S. Callaway, M. E. J. Newman, S. H. Strogatz and D. J. Watts, "Network robustness and fragility: Percolation on random graphs," *Phys. Rev. Lett.* **85**, 5468 (2000).
6. R. Cohen, K. Erez, D. ben-Avraham and S. Havlin, "Resilience of the Internet to random breakdowns," *Phys. Rev. Lett.* **85**, 4626 (2000).
7. R. Cohen, D. ben-Avraham and S. Havlin, "Percolation critical exponents in scale-free networks," *Phys. Rev. E* **66**, 036113 (2002).
8. M. E. J. Newman, "Spread of epidemic disease on networks," *Phys. Rev. E* **66**, 016128 (2002).
9. R. Pastor-Satorras and A. Vespignani, "Epidemic spreading in scale-free networks," *Phys. Rev. Lett.* **86**, 3200 (2001).
10. M. E. J. Newman and R. M. Ziff, "Efficient Monte Carlo algorithm and high-precision results for percolation," *Phys. Rev. Lett.* **85**, 4104 (2000).
11. A.-L. Barabási, *Network Science*, Cambridge University Press (2016).
12. M. E. J. Newman, *Networks*, 2nd ed., Oxford University Press (2018).

## Credits

Lecture slides: Sang Hoon Lee.

Created by Claude Opus 5.5.
