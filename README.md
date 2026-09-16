# LeakWatch

### Machine Learning for Water-Leak Detection, Localization, and Emergency Dispatch

LeakWatch is my MS Data Science project focused on using machine learning and water-network simulation to detect and locate water leaks and support emergency repair-crew dispatch.

The main idea is simple:

**Water-pressure sensor readings → leak detection → leak localization → emergency dispatch**

The project is being developed step by step, starting with simulated water-network data and gradually adding the machine-learning and dispatch components.

---

## What is this project?

LeakWatch is designed to analyze pressure readings from sensors placed on a water-distribution network.

The final system will answer three main questions:

1. **Is there a leak?** — Leak detection
2. **Where is the leak?** — Leak localization
3. **Which repair crew should be sent?** — Emergency dispatch

The goal is to develop a pipeline where sensor data is processed and converted into a useful decision for responding to a possible water leak.

---

## Why I picked this project

Water leaks in underground distribution networks can be difficult to detect because the pipes are not directly visible.

A leak can cause changes in the pressure behavior of the network. If these changes can be detected from sensor measurements, machine-learning methods may help identify abnormal conditions and estimate where a leak has occurred.

I chose this project because it combines several areas of my Data Science coursework:

* Machine learning
* Feature engineering
* Time-series sensor data
* Network analysis
* Simulation
* Data visualization
* Optimization and shortest-path routing

---

## Current Project Stage

The project is currently in the **initial development stage**.

My first goal is to build the water-network simulation and generate the dataset that will be used for the machine-learning models.

### Current focus

* Understand the EPANET water-network model
* Work with WNTR in Python
* Load the Net3 water network
* Identify suitable sensor nodes
* Simulate normal network conditions
* Introduce controlled leaks
* Record pressure changes
* Create a labeled dataset

The machine-learning detection, localization, and emergency-dispatch components will be developed after the initial dataset-generation stage.

---

## How I get the data

A major part of this project is creating a controlled dataset using water-network simulation.

I use:

* **EPANET** — water-distribution network simulation
* **WNTR (Water Network Tool for Resilience)** — Python-based tools for working with water networks

I use the **Net3** network as the initial test network.

The general process is:

1. Load the Net3 water network.
2. Run the network under normal conditions.
3. Select sensor locations.
4. Introduce a simulated leak at a selected location.
5. Change the leak size and timing for different scenarios.
6. Run the simulation.
7. Record pressure readings from the selected sensors.
8. Store the results as labeled data.

Because the leak location and leak conditions are controlled during simulation, the expected leak condition is known for each generated scenario.

---

## How the project will work

The final project will be developed as a pipeline.

### Step 1 — Generate Data

Create multiple normal and leak scenarios using EPANET/WNTR.

Different scenarios will use different:

* Leak locations
* Leak sizes
* Leak start times
* Network conditions

---

### Step 2 — Feature Engineering

The pressure measurements will be processed to create features that make leak-related changes easier to identify.

One important feature I plan to investigate is the **pressure residual**.

A residual represents the difference between an expected pressure and the observed pressure.

For example:

```text
Residual = Expected Pressure - Observed Pressure
```

The residual can help highlight pressure changes caused by abnormal conditions such as leaks.

---

### Step 3 — Leak Detection

A machine-learning model will be developed to classify the network condition as:

```text
Normal
   or
Leak
```

The model will be trained using the simulated labeled data and evaluated on data that was not used during training.

---

### Step 4 — Leak Localization

After detecting a leak, another model will be developed to estimate the location of the leak based on the pressure-change pattern observed by the sensors.

Because sensor coverage is limited, the initial goal is to estimate the **leak location or network area**, rather than assume that the exact pipe can always be identified.

---

### Step 5 — Emergency Dispatch

The water network can also be represented as a graph.

* Nodes → water-network locations
* Edges → connections between locations
* Crew locations → starting points
* Detected leak → destination

NetworkX will be used to investigate shortest-path routing and determine a suitable route for a repair crew.

---

### Step 6 — Evaluation

The final system will be evaluated using appropriate metrics for detection and localization.

Possible evaluation measures include:

* Accuracy
* Precision
* Recall
* F1-score
* Confusion matrix
* Localization accuracy
* Localization distance/error
* Response/processing time

I also plan to investigate how sensor noise affects the performance of the system.

---

## Tools and Technologies

* **Python** — Main programming language
* **EPANET** — Water-network simulation
* **WNTR** — Python tools for water-network analysis
* **NumPy** — Numerical processing
* **pandas** — Dataset processing
* **scikit-learn** — Machine-learning models
* **NetworkX** — Network and shortest-path analysis
* **Matplotlib** — Data visualization
* **Google Colab** — Development and experimentation
* **GitHub** — Project version control and documentation

---

## Planned Project Structure

```text
LeakWatch/
│
├── README.md
│
├── notebooks/
│   └── MS_Project.ipynb
│
├── data/
│   └── simulated_data.csv
│
├── results/
│   └── figures/
│
└── src/
    └── helper_scripts/
```

This structure will be expanded as the project develops.

---

## Project Workflow

The planned workflow is:

```text
EPANET / WNTR
       ↓
Water Network Simulation
       ↓
Normal + Leak Scenarios
       ↓
Pressure Sensor Data
       ↓
Feature Engineering
       ↓
Leak Detection
       ↓
Leak Localization
       ↓
Network Graph
       ↓
Emergency Crew Dispatch
       ↓
Evaluation
```

---

## My Contribution

The main contribution of this project will be the development of the complete workflow rather than creating a new water-network simulator or inventing new machine-learning algorithms.

My work will include:

* Creating simulated leak scenarios
* Generating a labeled dataset
* Selecting and processing sensor measurements
* Engineering pressure-based features
* Developing leak-detection models
* Developing leak-localization methods
* Building the network-based dispatch component
* Comparing the machine-learning approach with baseline methods
* Testing the system under different conditions
* Evaluating the final results

---

## Limitations

There are several limitations that I am considering during development.

### Simulated Data

The initial dataset is generated using a water-network simulator rather than collected directly from a physical water distribution system.

### Limited Sensors

Only selected network locations will be treated as sensor locations. Therefore, the system may not always be able to identify the exact pipe containing a leak.

### Network Assumptions

The initial experiments will use a controlled simulation environment. Real-world water networks can contain additional uncertainties and operational conditions.

### Real-World Validation

A later stage of the project may investigate public water-leak benchmarks such as **BattLeDIM** to evaluate how the approach performs on real-world data.

---

## Current Status

### Completed

* Project idea defined
* Overall system workflow planned
* EPANET/WNTR selected as the simulation environment
* Net3 selected as the initial water-network model

### In Progress

* Setting up the EPANET/WNTR environment
* Understanding the Net3 network
* Selecting sensor locations
* Creating the first leak simulation
* Generating the initial pressure dataset

### Planned

* Generate multiple leak scenarios
* Build the pressure-residual features
* Develop the leak-detection model
* Develop the localization model
* Implement emergency dispatch
* Evaluate the complete pipeline
* Investigate validation using public benchmark data

---

## References

* WNTR Documentation — https://usepa.github.io/WNTR/
* EPANET — U.S. Environmental Protection Agency — https://www.epa.gov/water-research/epanet
* BattLeDIM — https://battledim.ucy.ac.cy/
* BattLeDIM Dataset — https://zenodo.org/records/4017659
* LeakDB — https://github.com/KIOS-Research/LeakDB

---

## Note

This project is currently under development. The README will be updated as new components, experiments, datasets, and results are added.



