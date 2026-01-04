<!--
██████╗ ██████╗ ██╗██████╗  █████╗ ██╗   ██╗
██╔══██╗██╔══██╗██║██╔══██╗██╔══██╗██║   ██║
██████╔╝██████╔╝██║██║  ██║███████║██║   ██║
██╔═══╝ ██╔══██╗██║██║  ██║██╔══██║██║   ██║
██║     ██║  ██║██║██████╔╝██║  ██║╚██████╔╝
╚═╝     ╚═╝  ╚═╝╚═╝╚═════╝ ╚═╝  ╚═╝ ╚═════╝
-->

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=rect&color=gradient&height=105&section=header&text=LATTeYES+:+A+Intelligent+Monitoring+&fontSize=38&fontColor=F7F7F7" width="100%">

<br>

</div>

---
## 🎬 Project Demo

🔗 [LATTeYES](drive.google.com/file/d/1cqlzGmkXeBn0ObO6PWiPKCzetKCerxg5/view?usp=drivesdk)

---
<br>
LATTeyes is an ultra-low-power, fully offline Edge-AI vision system designed for real-time surveillance across wildlife reserves, industrial zones, border security, and remote perimeters.  
The system is built entirely on a Lattice CertusPro-NX FPGA, combining AI-based object detection** with PIR motion sensing to achieve high accuracy with minimal false positives.
Unlike cloud-dependent systems, LATTeyes performs end-to-end processing on the FPGA, from camera capture to inference and alert generation.
</div>


## ✨ Key Features

- ⚡ **Fully FPGA-based Edge AI** (no CPU / GPU dependency)
- 🎯 **INT8 Quantized MobileNetV2-SSD** for real-time detection
- 🔋 **Ultra-low power** (< 3W operation)
- 🧠 **Multi-Sensor Fusion** (Vision + PIR)
- 🌐 **Offline & Field-Deployable**
- 🎥 **Live Annotated Video Streaming (USB 3.0)**
- 🛡️ **Multi-Mode Surveillance Dashboard**

---

## 🎯 Detection Classes

The system detects and classifies:

- 👤 Human (Intruder)
- 🐘 Wildlife (Elephant, Rhino, Deer, Tiger, Bear)
- 🔥 Fire
- 🚗 Vehicle
- 🚁 Drone

---

## 🧠 System Architecture

### High-Level Pipeline

Camera (HM0360) -->
Image Capture & Resize (FPGA)-->
CNN Accelerator (MobileNetV2-SSD)-->
Bounding Box & NMS-->
Validated Decision Logic-->
Overlay + Alert Generation-->
USB 3.0 Video Streaming-->
---

## 🧩 Hardware Components

| Component | Description |
|--------|------------|
| **FPGA** | Lattice CertusPro-NX (LFCPNX-100) |
| **Camera** | Himax HM0360-MWA (Monochrome CMOS) |
| **Motion Sensor** | HC-SR501 PIR |
| **USB Controller** | Cypress FX3 (USB 3.0) |

---

## 📷 Input Sensors

### Camera – HM0360
- Low-power monochrome CMOS sensor
- Parallel video output
- I²C configuration
- Continuous live frame streaming to FPGA

### PIR Motion Sensor
- Acts as **wake-up trigger**
- Enables **inference only when motion is detected**
- Reduces false positives from shadows, wind, or background motion

---

## ⚙️ FPGA Processing Unit

The **CertusPro-NX FPGA** performs:

- Camera data capture & buffering
- Frame resizing to **224×224**
- AI inference execution
- Post-processing (confidence filtering & NMS)
- Bounding-box rendering
- Decision logic & alert generation

All processing is implemented using **Verilog HDL**.

---

## 🤖 AI / ML Model

### Model Architecture
- **MobileNetV2-SSD**
- Input: `224 × 224`
- Optimized for **real-time edge inference**

### Why MobileNetV2-SSD?
- Lightweight and FPGA-friendly
- Depthwise separable convolutions
- Native support in **Lattice sensAI**
- Balanced accuracy and resource usage

---

## 🧪 Model Training & Optimization

### Dataset
- ~3,500 annotated images
- Humans, animals, fire, vehicles, drones
- Diverse lighting and environmental conditions

### Training
- TensorFlow **1.14**
- Transfer learning from ImageNet
- Custom fine-tuning for surveillance scenarios

### Quantization
- **INT8 Post-Training Quantization**
- Model size reduced by **~75%**
- < 2% accuracy loss
- Fully compliant with CertusPro-NX constraints

---

## 🛠️ FPGA Deployment Using Lattice sensAI

### Toolchain
- **Lattice sensAI Neural Network Compiler (v7.0)**
- **CNN Accelerator IP Core v4.0**

### Deployment Flow

1. **Model Analysis**
   - Graph validation
   - Resource estimation
   - Unsupported layer removal

2. **Fixed-Point Quantization**
   - FP32 → INT8
   - BatchNorm folding
   - Accuracy validation

3. **ML Firmware Generation**
   - Accelerator command streams
   - Optimized memory layout

4. **AI System Generation**
   - FPGA bitstream
   - CNN firmware
   - Host control APIs
   - Radiant/Propel build scripts

5. **Flashing & Execution**
   - FPGA programmed
   - Live inference triggered via USB/UART

---

## 🔗 Multi-Sensor Fusion Logic

The fusion system ensures **high confidence detection**:

- PIR acts as **motion validation gate**
- CNN confidence thresholding
- Temporal filtering across frames
- Final detection only when **vision + PIR agree**

➡️ This drastically reduces **false alarms** while maintaining reliability.

---

## 🖥️ Surveillance Modes

Although detection runs for all classes simultaneously, the **dashboard allows mode-based alert filtering**:

| Mode | Trigger Conditions |
|----|----------------|
| **Intruder Detection** | Human only |
| **Wildlife Anti-Poaching** | Human or protected animals |
| **Industrial Safety** | Human or fire |
| **Border Defense** | Vehicles and drones |

---

## 📺 Output & Visualization

- Live video streamed via **USB 3.0**
- Bounding boxes with:
  - Class label
  - Confidence score
- Alert logs with timestamps
- Real-time dashboard monitoring

---

## 🧪 Simulation & Verification

### FPGA Simulation
- Verilog testbenches (Radiant)
- PIR trigger validation
- Sensor fusion timing verification

### AI Simulation
- TensorFlow & TensorFlow Lite
- INT8 accuracy comparison

### Verified Modules
- I²C camera initialization
- CSI-to-parallel video output
- FIFO-based UART
- USB 3.0 data formatting

---

## 🧰 Hardware Implementation

- Prototyped on Lattice Evaluation Board
- Final deployment on CertusPro-NX
- Sensors directly interfaced via FPGA GPIO
- Fully standalone operation

---

## 📊 Results & Performance

- Real-time inference latency: **< 100 ms**
- Power consumption: **< 3 W**
- High detection accuracy with minimal false positives
- Stable operation in indoor & outdoor conditions

---

## 🏁 Conclusion

**LATTeyes** demonstrates a **field-ready, low-power, FPGA-only Edge-AI surveillance system** capable of reliable real-time detection without cloud dependency.

By combining **AI acceleration**, **sensor fusion**, and **hardware-optimized design**, the system delivers a scalable solution for **wildlife conservation, industrial safety, and border security**.

---

## 📚 References

- Lattice Semiconductor – CertusPro-NX Datasheet  
- Lattice sensAI Neural Network Compiler User Guide  
- Himax HM0360 CMOS Sensor Datasheet  
- Lattice Edge-AI Reference Designs  

---

## 👥 Team

- SENTHIL KUMAR MAHALINGAM  
- S S JHOTHEESHWAR
- RAMAPRAKASH B   
- **PRIYADHARSAN D**  

**Mentor:** Ms. P. Malini  
**Institute:** Chennai Institute of Technology
---

⭐ *If you like this project, consider starring the repository!*
