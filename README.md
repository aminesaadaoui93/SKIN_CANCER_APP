# 🏥 SKIN CANCER APP - Medical AI Detection System

A web-based application for **early detection and classification of skin cancer** using deep learning and machine learning techniques. This system combines VGG16 neural networks with a Flask web interface to help medical professionals identify malignant and benign skin lesions.

---

## 🎯 Features

✅ **AI-Powered Detection**: VGG16 model trained to classify skin lesions as malignant or benign  
✅ **Web Interface**: User-friendly Flask web application with responsive design  
✅ **User Authentication**: Secure login system with default admin account  
✅ **Patient Management**: Complete patient tracking and history  
✅ **Real-time Predictions**: Instant AI analysis with confidence scores  
✅ **Database Integration**: SQLite for persistent data storage  
✅ **Report Generation**: Detailed analysis reports for each prediction  

---

## 🚀 Quick Start

### Prerequisites

- Python 3.8+
- pip (Python package manager)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/aminesaadaoui93/SKIN_CANCER_APP.git
   cd SKIN_CANCER_APP
   ```

2. **Create a virtual environment** (recommended)
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the application**
   ```bash
   python app.py
   ```

5. **Access the application**
   - Open your browser and go to: `http://localhost:5000`
   - Default login credentials:
     - **Username**: `admin`
     - **Password**: `admin123`

---

## 📋 Project Structure

```
SKIN_CANCER_APP/
├── app.py                          # Main Flask application
├── requirements.txt                # Python dependencies
├── skin_cancer.db                  # SQLite database
├── database.sql                    # Database schema (if needed)
├── SKIN_CANCER_APP.code-workspace # VS Code workspace config
├── model/                          # ML models directory
│   └── vgg16_malignant_vs_bengin.h5  # Pre-trained VGG16 model
├── static/                         # Static files (CSS, JS, images)
│   └── uploads/                    # User uploaded images
├── templates/                      # HTML templates
│   ├── login.html                  # Login page
│   ├── dashboard.html              # Dashboard with statistics
│   ├── predict.html                # Image upload & prediction
│   ├── result.html                 # Prediction results
│   └── patients.html               # Patient history
└── .gitignore                      # Git ignore rules
```

---

## 🔧 Core Technologies

| Technology | Purpose |
|-----------|---------|
| **Flask** | Web framework for building the application |
| **TensorFlow/Keras** | Deep learning framework |
| **VGG16** | Pre-trained convolutional neural network for image classification |
| **SQLite** | Lightweight database for patient records |
| **Pillow (PIL)** | Image processing and manipulation |
| **NumPy** | Numerical computing |

---

## 🌐 Application Routes

| Route | Method | Description |
|-------|--------|-------------|
| `/` | GET | Redirects to login page |
| `/login` | GET, POST | User authentication |
| `/dashboard` | GET | Shows statistics and overview |
| `/predict` | GET, POST | Upload image for AI analysis |
| `/result/<id>` | GET | Display prediction results |
| `/patients` | GET | View all patient records |
| `/logout` | GET | Clear session and logout |

---

## 🗄️ Database Schema

### Users Table
```sql
CREATE TABLE users (
    id       INTEGER PRIMARY KEY AUTOINCREMENT,
    username TEXT NOT NULL UNIQUE,
    password TEXT NOT NULL
);
```

### Patients Table
```sql
CREATE TABLE patients (
    id          INTEGER PRIMARY KEY AUTOINCREMENT,
    name        TEXT,
    age         INTEGER,
    result      TEXT,              -- 'Malignant' or 'Benign'
    confidence  REAL,              -- Prediction confidence percentage
    image_path  TEXT,              -- Path to uploaded image
    date_added  TEXT               -- Timestamp of analysis
);
```

---

## 🧠 AI Model Details

- **Model Architecture**: VGG16 (Visual Geometry Group)
- **Training Data**: Malignant vs Benign skin lesion classification
- **Input Size**: 224x224 RGB images
- **Output**: Binary classification
  - **> 0.5**: Malignant (cancerous)
  - **≤ 0.5**: Benign (non-cancerous)
- **Confidence Score**: Normalized prediction value as percentage

### Model Prediction Process

1. User uploads a dermatological image
2. Image is resized to 224x224 pixels
3. Image is normalized (0-1 range)
4. Model produces confidence score
5. Classification: Malignant or Benign
6. Results saved to database

---

## 👤 User Roles & Authentication

### Default Admin Account
- **Username**: `admin`
- **Password**: `admin123`

⚠️ **Security Note**: Change the default password in production!

---

## 📊 Dashboard Features

- **Total Patients**: Count of all analyzed cases
- **Malignant Cases**: Number of positive cancer detections
- **Benign Cases**: Number of negative cases
- **Patient Statistics**: Visual overview of predictions

---

## 🛡️ Security Features

- Session-based authentication
- Flash messages for user feedback
- Secure image uploads to isolated directories
- Database injection prevention using parameterized queries

---

## 📝 How to Use

### 1. Login
- Navigate to `http://localhost:5000`
- Enter credentials (default: admin/admin123)

### 2. Predict
- Click "Predict" in the navigation
- Enter patient name and age
- Upload a skin lesion image (JPG, PNG, etc.)
- Click "Analyze"

### 3. View Results
- See instant AI prediction with confidence percentage
- Result is automatically saved to database

### 4. View Patient History
- Access "Patients" page to see all analyzed cases
- Click on any patient for detailed report

---

## ⚙️ Configuration

### Change Secret Key (Production)
Edit `app.py` line 10:
```python
app.secret_key = "your-secure-random-string-here"
```

### Change Database Path
Edit `app.py` line 15:
```python
DATABASE = 'path/to/your/database.db'
```

### Configure Upload Folder
Edit `app.py` line 64:
```python
UPLOAD_FOLDER = 'path/to/your/uploads'
```

---

## 📦 Dependencies Overview

### Key Libraries
- **Flask**: Web framework
- **TensorFlow 2.21.0**: Deep learning
- **Keras**: High-level neural network API
- **Pillow**: Image processing
- **NumPy 2.4.4**: Scientific computing
- **SQLite3**: Database (built-in)

See `requirements.txt` for complete list of all 42 dependencies.

---

## 🐛 Troubleshooting

### Model Not Loading
```
⚠️ ATTENTION: Le modèle n'a pas pu être chargé.
```
**Solution**: Ensure `model/vgg16_malignant_vs_bengin.h5` exists and is accessible.

### Database Errors
**Solution**: Delete `skin_cancer.db` to reset (it will be recreated on next run).

### Upload Failures
**Solution**: Ensure `static/uploads/` directory is writable.

### Port Already in Use
**Solution**: Change port in `app.py` line 192:
```python
app.run(debug=True, port=5001)
```

---

## 📈 Future Enhancements

- [ ] Multi-class classification (more cancer types)
- [ ] API endpoints for integration
- [ ] Advanced user management & roles
- [ ] Export reports to PDF
- [ ] Dark mode UI
- [ ] Mobile app version
- [ ] Batch processing capability
- [ ] Model versioning and updates

---

## ⚖️ License

This project is provided as-is for educational and medical research purposes.

---

## 👨‍💻 Author

**Amine Saadaoui** - [GitHub Profile](https://github.com/aminesaadaoui93)

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

---

## ⚠️ Medical Disclaimer

This application is a **support tool** and should NOT replace professional medical diagnosis. Always consult with qualified dermatologists and medical professionals for accurate skin cancer diagnosis and treatment.

---

## 📞 Support

For issues, questions, or suggestions, please open a GitHub issue in the repository.

---

**Last Updated**: May 14, 2026  
**Status**: Active Development
