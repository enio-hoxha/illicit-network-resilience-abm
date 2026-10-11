# illicit-network-resilience-abm
Agent-based computational model in NetLogo simulating the Balloon Effect and Dark Resilience in scale-free drug trafficking networks under factorial law enforcement regimes.
# Dark Resilience: Agent-Based Modeling of Illicit Trafficking Networks Under Interdiction

[![Language](https://img.shields.io/badge/Language-NetLogo-darkgreen.svg)](https://ccl.northwestern.edu/netlogo/)
[![Methodology](https://img.shields.io/badge/Methodology-Agent--Based%20Modeling%20%7C%20SNA-orange)]()
[![Status](https://img.shields.io/badge/Status-Completed-success)]()
[![Domain](https://img.shields.io/badge/Domain-Criminology%20%7C%20Complex%20Systems-purple)]()

An agent-based computational economics and sociopolitical network simulation modeling the adaptive resilience of drug trafficking organizations (DTOs) facing law enforcement pressure.

The model formalizes the **Balloon Effect** and the thesis of **Dark Resilience**: demonstrating how targeted state interdiction shifts illicit flows from public, low-cost gray infrastructure into private, high-cost, covert yellow corridors (shadow infrastructure).

**Documentation:**
- **Project Presentation:** [Download Slides PDF](docs/Illicit_Network_Resilience_Presentation.pdf)

---

## Executive Summary and Core Insights

- **The Intelligence Premium:** Intelligence-led hub targeting for 5 ticks (Exp 1: 19.9% seizure rate) captures nearly twice the illicit volume of blind random interdiction deployed for 25 ticks (Exp 7: 11.4%), utilizing only one-fifth of the operational resources.
- **The Duijn Hardening Paradox:** The enforcement regimes achieving the highest operational seizure rates (~41% in Exp 5 and Exp 6) simultaneously drive the highest network hardening, expanding local clustering coefficients from 3.29% to ~10.5% and shifting over 45% of traffic onto clandestine shadow links.
- **Structural Destiny & Cultural Convergence:** While rigid (stubborn) cartels resist adaptation under brief pressure (0.0% displacement in Exp 4), sustained hub interdiction (25 ticks) erases organizational differences, forcing stubborn and adaptive cartels to converge to identical displacement equilibria (~45.2% FDI).
- **Incompressible Illicit Flows:** Across all experimental configurations (240 simulations across 8 factorial scenarios), criminal throughput was never eliminated; approximately 58% of shipments reached destinations even under maximum sustained targeted interdiction.

---

## Theoretical Foundations

```text
Theoretical Anchor                  Computational Operationalization
─────────────────────────────────   ──────────────────────────────────────────────────────────
Scale-Free Networks                 Barabási-Albert preferential attachment generating
(Barabási & Albert, 1999)           hub-and-spoke transit topologies vulnerable to central hits.

The Balloon Effect                  Flow Displacement Index (FDI) tracking spatial deflection
(Dorn et al., 2005)                 from public gray routes to private yellow corridors.

The Hardening Paradox               Dynamic local clustering metrics measuring how targeted
(Duijn et al., 2014)                interdiction induces modular, resilient cell structures.

Bounded Rationality                 Dynamic routing math: shipments minimize path weights
(Simon, 1955)                       combining physical base cost and perceived raid risk.
Behavioral Rules and Model Mechanics
1. Network Topology and Spatial Agents
Supply Nodes (Green): Generate shipment packets at a fixed spawn probability.

Demand Nodes (Red): Function as terminal market sinks recording completed deliveries.

Transit Backbone (Gray): Scale-free routing nodes sized proportionally to degree centrality. Raided hubs turn orange, spiking perceived risk to 100.

Shipments (Yellow Boxes): Navigate using Dijkstra-based dynamic shortest-path heuristics via the NetLogo nw:weighted-path-to primitive:
W_link = Base_Cost + Risk_Node1 + Risk_Node2

2. State Enforcement Regimes
Targeting Intelligence: Switches between Blind Patrols (uniform random node selection) and Intelligence-Led Patrols (targeting the highest-degree/busiest transit hub).

Resource Intensity: Governed by enforcement-chance (raid frequency) and enforcement-duration (holding traps for 5 ticks vs. 25 ticks).

Risk Memory: Once police vacate an occupied hub, perceived risk decays at a constant rate (-5 points per tick), restoring baseline transit confidence after 20 ticks.

3. Cartel Learning and Shadow Route Synthesis
Adaptive Memory: The cartel tracks operational failure rates over a rolling 90-tick memory window:
Failure_Rate = Seized_Shipments / Total_Shipments
When the failure rate exceeds the cartel's internal loss-tolerance-threshold, safe neighboring nodes synthesize a covert Yellow Link bypassing the compromised corridor.

Dark Residue: Inactive shadow routes are pruned only after 180 consecutive ticks of non-use; activated clandestine links persist as permanent organizational capital.

Factorial Experimental Design (30 Runs per Scenario)
The simulation evaluated 8 orthogonal experimental configurations holding network parameters constant (110 Nodes, 10% Supply, 10% Demand, 50% Spawn Rate, 40% Interdiction Chance) over 1,000-tick runs:
Experiment,Cartel Culture,Loss Tolerance,Targeting Mode,Raid Duration,Analytical Focus
Exp 1,Adaptive,5%,Busiest Transit,Short (5 ticks),Baseline Balloon Effect under smart policing
Exp 2,Stubborn,30%,Busiest Transit,Short (5 ticks),Organizational inertia under smart policing
Exp 3,Adaptive,5%,Random Transit,Short (5 ticks),Reactive cartel under blind policing
Exp 4,Stubborn,30%,Random Transit,Short (5 ticks),"Null baseline: rigid cartel, blind policing"
Exp 5,Adaptive,5%,Busiest Transit,Long (25 ticks),Sustained pressure on adaptive structure
Exp 6,Stubborn,30%,Busiest Transit,Long (25 ticks),Sustained pressure breaking cartel rigidity
Exp 7,Adaptive,5%,Random Transit,Long (25 ticks),Resource-heavy blind policing evaluation
Exp 8,Stubborn,30%,Random Transit,Long (25 ticks),Worst-case enforcement efficiency

Experiment,Mean Deliveries,Mean Seizures,Seizure Rate (%),Mean FDI (%),Clustering Coeff. (%)
"Exp 1 (Adaptive, Busiest, Short)","4,392.53","1,093.70",19.94%,42.03%,11.82%
"Exp 2 (Stubborn, Busiest, Short)","4,226.47","1,243.47",22.74%,18.94%,5.53%
"Exp 3 (Adaptive, Random, Short)","5,345.87",128.73,2.35%,9.53%,3.29%
"Exp 4 (Stubborn, Random, Short)","5,366.47",122.90,2.24%,0.00%,1.54%
"Exp 5 (Adaptive, Busiest, Long)","3,212.23","2,293.53",41.64%,45.15%,10.56%
"Exp 6 (Stubborn, Busiest, Long)","3,240.50","2,243.83",40.92%,45.22%,10.50%
"Exp 7 (Adaptive, Random, Long)","4,867.53",624.90,11.37%,25.59%,4.98%
"Exp 8 (Stubborn, Random, Long)","4,901.13",567.43,10.38%,3.55%,1.94%

Key Visualizations
1. Network Topology and Active Interdiction
Scale-free routing environment showing gray public hubs, orange interdicted nodes, and emergent yellow shadow corridors:

2. Targeting Efficiency vs. Brute Force
Seizure rate comparison proving that brief intelligence-led interdiction outperforms long-duration random patrol volume:

3. Factorial Flow Displacement Grid (FDI)
Heatmap quantifying the Balloon Effect across enforcement regimes, demonstrating the Exp 4 null result and Exp 5/6 convergence:

4. The Efficiency-Hardening Paradox (Duijn Dynamic)
Empirical mapping of how higher seizure rates systematically induce denser network clustering and structural hardening:

Policy Implications
Reallocating Enforcement Budgets: Interdiction strategies must prioritize targeting quality (intelligence) over operational volume (patrol hours). Holding arbitrary nodes for extended durations produces diminishing returns while consuming disproportionate resources.

The Seizure Metric Trap: High seizure volumes are counterproductive as a primary KPI; optimizing solely for seizures accelerates criminal network hardening, subsidizing the emergence of permanent clandestine corridors.

Containment vs. Elimination: Because supply flows adapt around interdicted nodes, public policy must reframe enforcement goals from total eradication to strategic disruption and operational cost escalation.

Repository Structure
├── docs/
│   └── Illicit_Network_Resilience_Presentation.pdf
├── images/
├── data/
├── model/
│   └── dark_resilience_model.nlogo
└── README.md

Authors
Enio Hoxha - Faculty of Economics and Management, Free University of Bozen-Bolzano
Teodora Atanasova - Faculty of Economics and Management, Free University of Bozen-Bolzano
