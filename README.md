# 🌾 Agriculture Crop Disease Detection & Advisory System

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![TensorFlow 2.19](https://img.shields.io/badge/TensorFlow-2.19-orange.svg)](https://tensorflow.org/)
[![React 19](https://img.shields.io/badge/React-19.0-61dafb.svg)](https://react.dev/)
[![Node.js 18+](https://img.shields.io/badge/Node.js-18+-green.svg)](https://nodejs.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-47A248.svg)](https://www.mongodb.com/)

A comprehensive full-stack platform designed to assist farmers and agricultural professionals in detecting **45 crop diseases across 14 crops** directly from leaf images with **96.18% validation accuracy**. The system couples a transfer-learning convolutional neural network with a bilingual advisory engine (English & Nepali) to provide actionable, farmer-friendly treatment guidance and historical disease analytics.

---

## 📋 Table of Contents
- [Project Overview](#-project-overview)
- [Key Features](#-key-features)
- [Supported Crops & Diseases](#-supported-crops--diseases)
- [System Architecture](#-system-architecture)
- [Technology Stack](#-technology-stack)
- [Model Performance & Evaluation](#-model-performance--evaluation)
- [Installation & Setup](#-installation--setup)
- [API Documentation](#-api-documentation)
- [Advisory Knowledge Base](#-advisory-knowledge-base)
- [Repository Structure](#-repository-structure)
- [Core Team & Contributors](#-core-team--contributors)
- [Future Roadmap](#-future-roadmap)
- [License](#-license)
- [Acknowledgments](#-acknowledgments)

---

## 🎯 Project Overview

Early and accurate identification of crop diseases is essential to preventing yield loss and ensuring food security. Smallholder farmers often lack access to timely plant pathology expertise.

This system bridges that gap by offering:
- **Instant Visual Diagnosis:** Fast leaf image classification powered by MobileNetV2 deep learning.
- **Actionable Treatment Plans:** Step-by-step disease management, fungicide/pesticide recommendations, and preventive cultural practices.
- **Multilingual Support:** Native bilingual guidance (English and Nepali) to ensure accessibility.
- **Farmer Dashboard:** Secure history tracking of previous crop scans and diagnostic records.
- **Confidence Calibration:** Multi-class probability scoring so users understand diagnostic reliability.

---

## ✨ Key Features

### For Farmers & Field Workers
| Feature | Description |
| :--- | :--- |
| 📸 **Leaf Image Upload** | Drag-and-drop or select photos directly from mobile devices or desktop |
| ⚡ **Instant Inference** | Receive disease classification with probability scores within 1-2 seconds |
| 💊 **Targeted Advisory** | Practical chemical, organic, and cultural recommendations |
| 🌐 **Bilingual Interface** | Toggle between English and Nepali seamlessly |
| 📊 **Scan History Dashboard** | Review past scans, diagnose recurrence patterns, and manage records |
| 🛡️ **Confidence Indicator** | Clear metrics indicating prediction certainty |

### For System Administrators & Developers
| Feature | Description |
| :--- | :--- |
| 🔐 **Secure Authentication** | JWT-authenticated user management with encrypted passwords |
| 🗄️ **MongoDB Image Metadata** | Structured records linking user profiles to upload histories and detections |
| ⚙️ **Modular API Engine** | Clean RESTful endpoints separating advisory data, auth, and image processing |
| 🧪 **Jupyter Pipeline Suite** | Five reproducible notebooks covering exploration, preprocessing, training, evaluation, and demo inference |

---

## 🌱 Supported Crops & Diseases

The classification pipeline identifies **45 distinct disease classes** across **14 major agricultural crops**:

| Crop | Classes Covered |
| :--- | :--- |
| **Apple** | Apple Scab, Black Rot, Cedar Apple Rust, Healthy |
| **Banana** | Panama Disease, Sigatoka Leaf Spot, Healthy |
| **Cherry** | Powdery Mildew, Healthy |
| **Coffee** | Coffee Leaf Rust, Healthy / No Rust |
| **Corn (Maize)** | Cercospora Leaf Spot (Gray Leaf Spot), Common Rust, Northern Leaf Blight, Healthy |
| **Grape** | Black Rot, Esca (Black Measles), Leaf Blight (Isariopsis), Healthy |
| **Mango** | Anthracnose, Healthy |
| **Orange** | Huanglongbing (Citrus Greening), Healthy |
| **Peach** | Bacterial Spot, Healthy |
| **Pepper (Bell)** | Bacterial Spot, Healthy |
| **Potato** | Early Blight, Late Blight, Healthy |
| **Strawberry** | Leaf Scorch, Healthy |
| **Sugarcane** | Red Rot, Bacterial Blight, Healthy |
| **Tomato** | Bacterial Spot, Early Blight, Late Blight, Leaf Mold, Septoria Leaf Spot, Spider Mites (Two-spotted spider mite), Target Spot, Yellow Leaf Curl Virus, Mosaic Virus, Healthy |

---

## 🏗️ System Architecture

```text
┌────────────────────────────────────────────────────────┐
│                   React + Vite UI                      │
│   (AuthContext, Axios Client, Dashboard, Upload Modal) │
└──────────────────────────┬─────────────────────────────┘
                           │ HTTP / REST (JWT)
                           ▼
┌────────────────────────────────────────────────────────┐
│               Node.js + Express Server                 │
│  ├── /api/auth     : User Registration & Login         │
│  ├── /api/images   : Multer Upload & Scan History      │
│  └── /api/advisory : Disease Treatment Recommendations │
└─────────────┬───────────────────────────┬──────────────┘
              │                           │
              ▼                           ▼
┌──────────────────────────┐  ┌──────────────────────────┐
│     MongoDB Database     │  │   Flask / ML Inference   │
│ (Users, Scans, Advisory) │  │  (MobileNetV2 CNN Model) │
└──────────────────────────┘  └──────────────────────────┘
```

---

## 🛠️ Technology Stack

### Deep Learning & Data Science
* **Framework:** TensorFlow 2.19, Keras
* **Base Architecture:** MobileNetV2 (Transfer Learning with custom classification head)
* **Image Processing:** OpenCV, Pillow, Albumentations / Keras Preprocessing
* **Analytics & Metrics:** Scikit-Learn, Pandas, NumPy, Matplotlib, Seaborn

### Backend API
* **Runtime:** Node.js, Express.js
* **Database:** MongoDB (Mongoose ODM)
* **Authentication:** JSON Web Tokens (JWT), bcryptjs
* **File Handling:** Multer multipart/form-data middleware

### Frontend Client
* **Framework:** React 19, Vite
* **Styling:** TailwindCSS
* **Routing & State:** React Router v7, React Context API
* **HTTP Client:** Axios with bearer token interceptors

---

## 📊 Model Performance & Evaluation

The deep learning model was fine-tuned over 38 epochs with early stopping and learning rate reduction on plateau:

| Evaluation Metric | Score |
| :--- | :--- |
| **Validation Accuracy** | **96.18%** |
| **Macro F1-Score** | **95.16%** |
| **Weighted F1-Score** | **96.22%** |
| **ROC AUC** | **0.999+** |
| **Test Error Rate** | **3.82%** |

### Evaluation Assets Available
* `Modeling/reports/evaluation_results/classification_report.csv`
* `Modeling/reports/evaluation_results/confusion_matrices/confusion_matrix.png`
* `Modeling/reports/evaluation_results/roc_curves.png`
* `Modeling/reports/evaluation_results/predictions.csv`

---

## 💻 Installation & Setup

### Prerequisites
- Node.js (v18+)
- Python (v3.10+)
- MongoDB (Local instance or MongoDB Atlas connection string)
- Git

### 1. Clone the Repository
```bash
git clone https://github.com/tusharpatel0504/Agriculture-Crop-Disease-Detection.git
cd Agriculture-Crop-Disease-Detection
```

### 2. Backend Setup
```bash
cd backend
npm install
```

Create a `.env` file in the `backend/` directory:
```env
PORT=5000
MONGO_URI=mongodb://localhost:27017/crop_disease
JWT_SECRET=your_jwt_secret_key_here
```

Seed the advisory knowledge base:
```bash
node seedAdvisory.js
```

Start the backend server:
```bash
npm start
```
*Backend runs at `http://localhost:5000`.*

### 3. Frontend Setup
```bash
cd ../frontend
npm install
npm run dev
```
*Frontend runs at `http://localhost:5173`.*

### 4. ML Model Inference Service
```bash
cd ../Modeling
pip install -r requirements.txt
python app.py
```
*Inference application starts and serves model predictions.*

---

## 📡 API Documentation

### Authentication (`/api/auth`)
* `POST /api/auth/register` - Create a new user account
* `POST /api/auth/login` - Authenticate user and return JWT bearer token

### Leaf Scans (`/api/images`)
* `POST /api/images/upload` - Upload leaf image for disease diagnosis (Requires JWT)
* `GET /api/images/my-images` - Fetch current user's scan history
* `DELETE /api/images/:id` - Remove a scan record from history

### Advisory (`/api/advisory`)
* `GET /api/advisory` - Retrieve all advisory records
* `GET /api/advisory/:disease` - Get disease symptoms, treatment procedures, and prevention measures

---

## 📚 Advisory Knowledge Base

The advisory system (`Modeling/configs/advisory_system.json`) contains structured clinical guidance for each disease:
- **Symptoms:** Early and late visual indicators on leaves, stems, and fruits.
- **Causative Agents:** Fungal, bacterial, or viral pathogens.
- **Treatment Steps:** Organic treatments, chemical fungicides, and dosage recommendations.
- **Preventive Measures:** Crop rotation, spacing, drip irrigation, and resistant varieties.
- **Multilingual Support:** All recommendations are mapped in both English and Nepali.

---

## 📁 Repository Structure

```text
Agriculture-Crop-Disease-Detection/
├── .devcontainer/                  # DevContainer Docker configuration
├── .vscode/                        # VS Code workspace settings
├── Modeling/                       # Machine Learning core
│   ├── configs/                    # Hyperparameters & advisory data
│   │   ├── advisory_system.json    # Bilingual treatment knowledge base
│   │   ├── class_indices.json      # Class index mapping
│   │   ├── class_weights.json      # Class imbalance correction weights
│   │   └── preprocessing_config.yaml
│   ├── Crop Disease Dataset/       # Train, validation & test image sets
│   ├── models/                     # Best & final saved weights (.keras, .h5)
│   ├── notebooks/                  # End-to-end experimental workflows
│   │   ├── 01_data_exploration.ipynb
│   │   ├── 02_data_preprocessing.ipynb
│   │   ├── 03_model_training.ipynb
│   │   ├── 04_model_evaluation.ipynb
│   │   └── 05_inference_demo.ipynb
│   ├── reports/                    # Figures, confusion matrices & logs
│   ├── app.py                      # Flask inference API server
│   └── requirements.txt            # Python dependencies
├── backend/                        # Node.js + Express API
│   ├── config/db.js                # MongoDB connection
│   ├── controllers/                # Advisory, auth & image controllers
│   ├── middleware/                 # JWT validation & Multer upload
│   ├── models/                     # User, Image & Advisory Mongoose schemas
│   ├── routes/                     # Express REST routes
│   ├── seedAdvisory.js             # Advisory database seeder
│   └── server.js                   # Application entrypoint
├── frontend/                       # React 19 + Vite client
│   ├── src/
│   │   ├── api/                    # Axios API client modules
│   │   ├── components/             # Reusable UI (Navbar, AdvisoryModal, ImageCard)
│   │   ├── context/                # AuthContext state provider
│   │   ├── pages/                  # Dashboard, Upload, Login, Register, Error
│   │   ├── App.jsx                 # Routing and layout structure
│   │   └── main.jsx
│   ├── package.json
│   └── vite.config.js
└── README.md                       # Main documentation
```

---

## 👥 Core Team & Contributors

### Contributing Developers
* **Tushar Patel** ([@tusharpatel0504](https://github.com/tusharpatel0504)) - **Project Lead & Architecture**  
  Overall project leadership, system architecture, advisory schema design, API integration, and final deployment.
* **Shiva** ([@Workingshivayadav-ui](https://github.com/Workingshivayadav-ui)) - **Frontend Lead**  
  React/Vite architecture, UI/UX implementation, authentication flows, upload previews, and responsive dashboard.
* **Manikant** ([@Manikant2324](https://github.com/Manikant2324)) - **Backend Lead**  
  Express API server, MongoDB schemas, JWT authentication middleware, Multer file upload pipelines, and routes.
* **Sudhanshu Katiyar** ([@uffy-957](https://github.com/uffy-957)) - **Machine Learning Lead**  
  MobileNetV2 transfer learning, dataset structuring, CNN model training, checkpoint management, and inference pipelines.
* **Arnav** ([@arnav240306](https://github.com/arnav240306)) - Dataset summary analysis, metric callbacks, and UI notification components.
* **Ankit Sharma** ([@AnkitSharma5304](https://github.com/AnkitSharma5304)) - Class configuration mapping, modeling documentation, and frontend API modules.
* **Shivam Gautam** ([@gautama-28](https://github.com/gautama-28)) - Data distribution visualizations and backend environment configs.
* **Baibhav** ([@blazoxx](https://github.com/blazoxx)) - Data augmentation visualizations, confusion matrices, and ROC curve evaluations.
* **Sandeep** ([@SANDEEP-K15](https://github.com/SANDEEP-K15)) - Class weights calculation, Image scan schemas, and database seed scripts.
* **Prince** ([@Prince-Tiwari14](https://github.com/Prince-Tiwari14)) - Image preprocessing pipelines and model evaluation notebooks.

---

## 🗺️ Future Roadmap
- [ ] Mobile Application (React Native) with on-device offline inference (TFLite).
- [ ] Weather-informed disease vulnerability forecasting based on local humidity and temperature.
- [ ] Extension to staple grain crops including rice, wheat, and barley.
- [ ] Voice-based spoken advisory in regional dialects.

---

## 📝 License
This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments
- **PlantVillage Dataset** for providing open-access agricultural leaf image benchmarks.
- **TensorFlow & Keras** for the deep learning framework.
- **Agricultural Extension Services** for domain validation of disease treatment recommendations.

---

*Empowering farmers with accessible, AI-powered agricultural intelligence.* 🌾
