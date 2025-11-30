# RL-DynaMOSA: Controlling Test Case Generation with Reinforcement Learning

![Java](https://img.shields.io/badge/Java-8-orange)
![EvoSuite](https://img.shields.io/badge/EvoSuite-1.2.1-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Research](https://img.shields.io/badge/Research-Master%20Thesis-red)

> **Research Project**: Dynamic parameter control for automated test case generation using Reinforcement Learning (Q-Learning) integrated with EvoSuite's DynaMOSA algorithm.

---

## 📖 Abstract

Software testing consumes approximately 50% of software development costs. While tools like **EvoSuite** automate unit test generation using genetic algorithms (DynaMOSA), they typically rely on static parameter configurations (e.g., crossover and mutation rates).

**RL-DynaMOSA** introduces an adaptive controller based on **Q-Learning** to dynamically adjust these parameters during the search process. By continuously interacting with the environment and learning from coverage feedback, the agent optimizes the balance between exploration and exploitation, leading to higher code coverage and more efficient test generation for complex classes.

**Key Contribution:**
- Integration of a **Q-Learning Agent** into EvoSuite.
- Dynamic adjustment of **Crossover Rate** and **Mutation Rate**.
- Extensive evaluation on **100 Java classes** from the SF110 dataset.

---

## 🚀 Features

- **Adaptive Parameter Control**: Replaces static parameter tuning with dynamic, reinforcement-learning-based adjustments.
- **Q-Learning Integration**:
  - **State**: Defined by fitness trends (e.g., improvement, stagnation).
  - **Action**: Increase/Decrease crossover or mutation rates.
  - **Reward Function**: Rewards fitness improvements and efficient parameter changes; penalizes excessive mutation instability.
- **Seamless Integration**: Built on top of EvoSuite 1.2.1, fully compatible with existing DynaMOSA workflows.

---

## 🏗 Architecture

The RL controller interacts with EvoSuite's evolutionary cycle every 10 iterations:

graph TD
A[EvoSuite Search Loop] -->|State: Fitness & Rates| B(RL Agent)

B -->|Action: Adjust Param| C{Q-Learning Policy}

C -->|Update| D[New Crossover/Mutation Rates]

D -->|Apply| A

A -->|Feedback| E[Reward Calculation]

E -->|Update Q-Table| B


---

## 📊 Experimental Results

We evaluated RL-DynaMOSA against the default EvoSuite configuration on 100 Java classes (SF110 dataset) with 20 repetitions per class.

| Metric | Performance |
| :--- | :--- |
| **Code Coverage** | **Improved in 29% of classes** (Significantly better in complex classes like `EncodingFactory`). |
| **Time Efficiency** | **Reduced execution time in 84% of classes** (Avg. reduction ~1.8s). |
| **Exception Discovery** | detected more exceptions in **22%** of classes. |

**Trend Analysis**:
For classes with improved coverage (e.g., `ghm.follow.gui.TabbedPane`), RL-DynaMOSA successfully learned to:
1. Start with **high mutation rates** (Exploration).
2. Gradually shift to **higher crossover rates** (Exploitation) as the search converged.

---

## 🛠 Installation & Usage

### Prerequisites
- **Java Development Kit (JDK) 8** (Required by EvoSuite)
- Maven 3.x

### Build from Source
git clone https://github.com/qin-coder/Master_Thesis_Xuwei.git

cd Master_Thesis_Xuwei

mvn clean install


### Running RL-DynaMOSA
You can run the tool just like standard EvoSuite, but enabled with the RL controller:

java -jar evosuite-master-1.2.1.jar

-class <TargetClass>

-projectCP <Classpath>

-criterion branch:line:weakmutation

-Dalgorithm=DynaMOSA

-Dsearch_budget=300


---

## 📂 Project Structure

├── evosuite_RL_version/ # Source code of the modified EvoSuite
├── Experiment scripts/ # Python/Bash scripts for running batch experiments
├── Experiment results/ # Raw CSV data from the evaluation (SF110)
└── Master_Thesis.pdf # Full thesis text



---

## 👤 Author

**Xuwei Qin**  
M.Sc. Computer Science, Humboldt-Universität zu Berlin  
*Specialization: Software Engineering, Reinforcement Learning, Automated Testing*

---

*This project was submitted as a Master's Thesis at the Institute for Computer Science, Humboldt-Universität zu Berlin.*

