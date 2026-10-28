# K-Means Load Balancing in CloudAnalyst

A K-Means based virtual machine (VM) load balancer implemented in the CloudAnalyst simulator. It clusters VMs into two groups by MIPS and RAM so that incoming tasks are matched to the capability of each machine. It is compared against Round Robin (RR), Equally Spread Current Execution Load (ESCEL) and Throttled.

## Overview

- Load balancing is based on clustering VMs by **MIPS** and **RAM**.
- It is implemented by modifying the Java source of CloudAnalyst.
- It is evaluated under three service broker policies:
  - Closest Data Center (CDC)
  - Optimize Response Time (ORT)
  - Dynamic Reconfiguration (DR)
- The workload is six user bases spread over different regions, with millions of peak users.

## Key Results

- K-Means outperforms RR and ESCEL under all three broker policies.
- Under the DR policy, K-Means reduces data center processing time (DCPT) by **92.17%** compared to RR and **67.61%** compared to ESCEL.
- Under ORT and DR, Throttled gives slightly lower DCPT than K-Means. Even so, resource-profile-aware cluster dispatch is more effective than concurrency-capping, and it lets the broker policy become more dynamic.

## Repository Structure

| Path | Description |
|---|---|
| `CloudAnalyst/` | Modified CloudAnalyst Eclipse project |
| `CloudAnalyst/source/cloudsim/ext/datacenter/KMean.java` | K-Means clustering implementation |
| `CloudAnalyst/source/cloudsim/ext/datacenter/KMeanVmLoadBalancer.java` | K-Means VM load balancer |
| `simulation-configs/` | Simulation configurations (`CA1.sim` – `CA4.sim`) |
| `results/` | Result reports for RR, ESCEL, Throttled and K-Means under each broker policy |
| `results-scalability/` | Scalability results (K-Means vs Throttled) |

## Requirements

- Java Runtime Environment (JRE)

## Running the Simulator

From inside the `CloudAnalyst/` folder:

**Windows**
```bash
run.bat
```

**Linux / macOS**
```bash
java -cp "jars/simjava2.jar:jars/gridsim.jar:jars/iText-2.1.5.jar:classes:." cloudsim.ext.gui.GuiMain
```

## Reproducing the Experiments

1. Launch CloudAnalyst using the command above.
2. Load a configuration file from `simulation-configs/` (for example `CA1.sim`).
3. Select the load balancing policy (RR, ESCEL, Throttled or K-Means).
4. Select the service broker policy (Closest Data Center, Optimize Response Time or Dynamic Reconfiguration).
5. Run the simulation and compare the output with the reports in `results/`.

## Acknowledgements

This work is built on [CloudAnalyst](https://www.cloudbus.org/cloudsim/) and CloudSim from the CLOUDS Laboratory, University of Melbourne. The original licence terms apply to the base simulator code.
