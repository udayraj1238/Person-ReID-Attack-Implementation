# Adversarial Attacks on Person Re-Identification (advPattern Replication)

This repository contains a PyTorch implementation of adversarial attacks against Deep Person Re-Identification (Re-ID) systems. This project replicates and validates the findings of the **"advPattern"** method (ICCV 2019), demonstrating how adversarially transformable patterns can fool state-of-the-art Re-ID models in digital environments.

The project implements two primary attack modes:
1.  **Evading Attack**: An untargeted attack that makes the model fail to identify the person (making them "invisible").
2.  **Impersonation Attack**: A targeted attack that forces the model to misidentify the adversary as a specific target person.

## 🏆 Experimental Results

We evaluated the robustness of our implementation on the **Market-1501** dataset using a standard ResNet-50 baseline (Model B). Below are the detailed performance metrics.

### 1. Evading Attack Results (Table 2)
The goal of the Evading Attack is to drop the Rank-1 accuracy of the model, effectively hiding the person from the surveillance system.

**Summary Statistics (Average over 5 Identities):**

| Condition | Rank-1 | Rank-5 | Rank-10 | mAP | SS |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Original** | 96.0% | 100.0% | 100.0% | 70.8% | 0.953 |
| **Attack (TS)** | **37.0%** | 49.0% | 58.0% | 14.1% | 0.726 |

> **Observation:** The attack successfully reduced the Rank-1 accuracy by **59%** (from 96.0% down to 37.0%), proving the effectiveness of the generated chest patterns in confusing the model.

<details>
<summary><strong>Click to view detailed logs per identity</strong></summary>

We tested the attack on 5 random identities. The drop in Rank-1 accuracy (R1) is shown below:

* **PID 154**: R1 dropped 80.0% → **40.0%**
* **PID 921**: R1 dropped 100.0% → **0.0%** (Perfect Evasion)
* **PID 1241**: R1 dropped 100.0% → **25.0%**
* **PID 710**: R1 dropped 100.0% → **60.0%**
* **PID 233**: R1 dropped 100.0% → **60.0%**

</details>

---

### 2. Impersonation Attack Results (Table 3)
The Impersonation Attack is significantly harder, as it requires the model to match the adversary to a specific target while simultaneously suppressing the adversary's true identity.

**Summary Statistics (Average over 5 Random Pairs):**

| Matched Person | Rank-1 | Rank-5 | Rank-10 | mAP | SS |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Target (Success)** | **46.7%** | 88.0% | 96.0% | 40.1% | 0.820 |
| **Adversary (Fail)** | **0.0%** | 0.0% | 0.0% | 0.3% | 0.497 |

> **Observation:**
> * **Success Rate:** We achieved a **46.7% Rank-1 Success Rate** in mimicking the target. This aligns closely with the original paper's benchmark (~47%).
> * **Identity Suppression:** We achieved a **0.0% Rank-1** match for the adversary's original identity, meaning the system completely failed to recognize the true person behind the disguise.

<details>
<summary><strong>Click to view detailed logs per pair</strong></summary>

We evaluated the attack on 5 random `Adversary -> Target` pairs:

* **Pair 1 (791 → 1190)**: Target Rank-1 **50.0%**
* **Pair 2 (807 → 1498)**: Target Rank-1 **60.0%**
* **Pair 3 (1317 → 19)**: Target Rank-1 **83.3%** (High Success)
* **Pair 4 (1429 → 1109)**: Target Rank-1 **20.0%**
* **Pair 5 (101 → 692)**: Target Rank-1 **20.0%**

</details>

## 🚀 Getting Started

### Prerequisites
* Python 3.x
* PyTorch & Torchvision
* Market-1501 Dataset

### Usage
1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/yourusername/AdvPattern-ReID-PyTorch.git](https://github.com/yourusername/AdvPattern-ReID-PyTorch.git)
    cd AdvPattern-ReID-PyTorch
    ```
2.  **Download the Market-1501 dataset** and place it in the root directory.
3.  **Run the notebooks:**
    * `Evading_Attack.ipynb`: Reproduces the evasion results (Table 2).
    * `Impersonation_Attack.ipynb`: Reproduces the impersonation results (Table 3).

## 📄 References
* *Wang et al., "advPattern: Physical-World Attacks on Deep Person Re-Identification via Adversarially Transformable Patterns", ICCV 2019.*
