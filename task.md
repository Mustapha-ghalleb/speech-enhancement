
# 🔥 **TASK: Generate a COMPLETE, FULLY WORKING IPYNB NOTEBOOK implementing the entire project described below.**

The notebook must run **end-to-end** with **NO manual edits needed**.

You must output a **single .ipynb** file containing executable code cells + explanations.

---

## 🎯 **Project Requirements**

Build a full Deep Learning pipeline for **speech enhancement (vocal rehaussement)** using PyTorch, including:

### **1. Data**

* Automatically download a speech enhancement dataset such as:

  * **VoiceBank-DEMAND dataset** *(preferred)*
  * OR any open speech + noise dataset if easier.
* Prepare noisy audio + clean audio pairs.
* Resample to 16kHz.
* Frame into sequences suitable for LSTM/BiLSTM.
* Create train/validation/test PyTorch datasets and dataloaders.

---

### **2. Model Architecture**

Implement a **BiLSTM-based speech enhancement model**:

* 2–4 stacked LSTM/BiLSTM layers.
* Linear projection to audio frames.
* Treat the model as a **selective filter** from noisy → clean audio.

Model must output:

* Denoised audio waveform.

---

### **3. Training (FP32 baseline)**

* Train the model in FP32.
* Save:

  * baseline_model.pth
  * sample enhanced audio files for testing.

---

### **4. Quantization Pipeline**

Follow the professor’s EXACT pipeline:

#### **Step 1 — FP32 model**

Train original LSTM model (already done above).

#### **Step 2 — PTQ & QAT**

Implement both:

##### **PTQ**

* Use PyTorch **post training static quantization**.
* Calibrate using training samples.
* Extract quantization parameters:

  * scale
  * zero_point
  * quantized dtype

##### **QAT**

* Use PyTorch's quantization aware training utilities:

  * prepare_qat
  * convert

#### **⚠️ Notes to respect**

* LSTM quantized models **cannot be exported to ONNX**.
* Only extract the quantization parameters.

#### **Step 3 — Dequantize back to FP32**

* Convert quantized weights back to FP32.
* Rebuild a FP32 LSTM architecture.
* Insert extracted quantization parameters as metadata.

#### **Step 4 — Export FP32 model to ONNX**

* Export as:

  * model_for_gap9.onnx

#### **Step 5 — Manual quantization (simulated)**

* Using the parameters from PTQ/QAT, perform manual INT8 quantization on:

  * weights
  * activations
    (simulate GAP9 toolkit behavior).

#### **Step 6 — Simulate deployment**

* Run inference using:

  * FP32 baseline
  * PTQ simulated GAP9 model
  * QAT simulated GAP9 model

---

### **5. Evaluation Metrics**

Compute and compare:

#### **A. Quantization error metrics**

* **QSNR** (Quantization Signal-to-Noise Ratio)
* **Cosine Similarity**

#### **B. Runtime & model size**

(table comparing baseline/PTQ/QAT)

#### **C. Audio output examples**

* Save WAV files for:

  * Noisy input
  * Clean target
  * FP32 model output
  * PTQ output
  * QAT output

---

## 📦 **Notebook Output Requirements**

The generated notebook MUST include:

### ✔ Fully executable PyTorch code

### ✔ Dataset download

### ✔ Preprocessing

### ✔ BiLSTM model

### ✔ FP32 training

### ✔ PTQ quantization

### ✔ QAT quantization

### ✔ Dequantization step

### ✔ ONNX export

### ✔ Manual quantization (GAP9-style)

### ✔ Final evaluation metrics

### ✔ Model size comparison

### ✔ Inference + saved audio files

### ✔ Zero missing cells or TODOs

---

## 📌 IMPORTANT: Notebook must contain

* Markdown explanations for each step.
* Proper section titles.
* Reproducible code.
* No placeholder functions.
* No missing implementations.
* No “fill this later”.

---

## 🧠 **Deliverable**

Output a **single IPYNB file** containing the complete implementation.

---

