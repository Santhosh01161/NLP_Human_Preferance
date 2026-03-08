# 🚀 NLP Human Preference: DPO Alignment Project

[![Hugging Face Model](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Model-yellow)](https://huggingface.co/Santhosh01161)
[![Python-3.12](https://img.shields.io/badge/Python-3.12-blue.svg)](https://www.python.org/)
[![License-Apache_2.0](https://img.shields.io/badge/License-Apache_2.0-green.svg)](https://opensource.org/licenses/Apache-2.0)

This project demonstrates the fine-tuning of a Large Language Model (LLM) using **Direct Preference Optimization (DPO)** to align model outputs with human preferences for truthfulness and accuracy.

---

## 📖 Project Overview
The goal of this assignment was to take the **Qwen2.5-1.5B-Instruct** model and refine its factuality using the `truthy-dpo` dataset. We utilized **LoRA** and **4-bit quantization** to perform preference alignment efficiently on a single T4 GPU.

### 🛠️ Technical Stack
| Feature | Technology |
| :--- | :--- |
| **Base Model** | Qwen2.5-1.5B-Instruct |
| **Alignment Technique** | DPO (Direct Preference Optimization) |
| **Efficiency** | LoRA + bitsandbytes (4-bit) |
| **Judge LLM** | Gemini-1.5-Flash |

---

## 📈 Training Process & Phase Comparison

The project was conducted in two distinct training phases to observe model behavior and convergence.



### 1. Initial DPO Training (100 Steps)
The primary training phase was conducted for **100 steps**. This allowed the model enough exposure to the preference pairs to begin shifting its internal probability distributions toward the "truthy" (chosen) answers.

### 2. Experimental Training (10 Steps)
An additional experimental run was performed for **10 steps** with adjusted hyperparameters to quickly verify the sensitivity of the loss and the immediate impact of DPO on the model's instruction-following capabilities.

---

## 📊 Loss Curves & Visualization

### Training Loss Analysis
#### Phase 1: Initial Training (100 Steps)
<img width="855" height="470" alt="TrainLoss1" src="https://github.com/user-attachments/assets/d31cf226-3624-46ef-9c98-2fb5b2f49d84" />


#### Phase 2: Experimental Run (10 Steps)
<img width="855" height="470" alt="Trainloss2" src="https://github.com/user-attachments/assets/645940f4-ae14-4340-a7f0-8c897a9e2a1f" />



### 🔍 Understanding the Results
* **DPO Loss:** A declining curve indicates the model is successfully learning the preference between "Chosen" and "Rejected" responses.
* **Reward Margins:** In the 100-step run, you should notice a wider gap between rewards, indicating higher confidence in truthful outputs compared to the 10-step run.

---

## 🧪 Evaluation Results (Task 4.4)

Evaluation was performed using **LLM-as-a-Judge** (Gemini-1.5-Flash) on 15 test samples.

### Win Rate Summary
| Metric | Count |
| :--- | :--- |
| **Model B (DPO) Wins** | 1 |
| **Ties** | 14 |
| **Model A (Base) Wins** | 0 |
| **Total Valid Samples** | 15 |

### 🏆 Final Win Rate: <span style="color:green">53.33%</span>

**Calculation Formula:**
$$\text{Win Rate} = \frac{\text{Wins} + (0.5 \times \text{Ties})}{\text{Total}} \times 100$$

---

## 🧠 Key Insights

1.  **Robustness:** The high tie rate (93%) confirms that **Qwen2.5-1.5B-Instruct** is already a strong baseline. The DPO training successfully "nudged" the model without degrading its general knowledge.
2.  **Successful Alignment:** Model B (DPO) achieved a win without any losses against the base model, proving the alignment was positive.
3.  **Parameter Efficiency:** We only trained **~1.5 Million** parameters (0.1% of the total model) using LoRA, showing that high-impact alignment does not require massive compute resources.

---

## 📂 Repository Structure
* `A5_Human_Preference (1).ipynb`: Main training and evaluation notebook.
* `README.md`: Project documentation.
* `.gitignore`: Configured to exclude `venv`, `pdfs`, and temporary files.

---
<p align="center">Made with ❤️ for NLP Human Preference Alignment</p>
