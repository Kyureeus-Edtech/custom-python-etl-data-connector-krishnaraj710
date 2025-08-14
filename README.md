
# ThreatFox ETL Data Connector

## 📌 Overview
The **ThreatFox ETL Data Connector** is a Python-based pipeline that retrieves recent threat intelligence data from the [ThreatFox API](https://threatfox.abuse.ch/), transforms it for MongoDB compatibility, and stores it for further analysis.  

This tool is designed for security analysts, researchers, and developers who wish to integrate up-to-date threat data into a MongoDB-backed datastore for analytics, visualization, or further automated processing.

***

## ✨ Features

### **Extract**
- Fetches latest **JSON threat data** from the ThreatFox API.
- Uses endpoint URL stored in a `.env` file for flexibility.

### **Transform**
- Cleans keys containing prohibited characters (`.` and `$`) for MongoDB compatibility.
- Adds ingestion timestamps for tracking data freshness.

### **Load**
- Inserts cleaned threat data into MongoDB.
- Ensures persistence for historical analysis.

### **Security**
- API URLs and MongoDB credentials are stored securely in environment variables.
- `.env` file is ignored by Git to avoid accidental credential leaks.

***

## 🔗 API Details
- **Base URL:** stored in `.env` as `THREATFOX_JSON_URL`
- **Authentication:** None (public endpoint)
- **Example Endpoint:**  
  ```
  https://threatfox.abuse.ch/export/json/recent/
  ```

***

## 📂 Project Structure
```
custom-python-etl-data-connector-krishnaraj710/
│
├── threatfox_connector/
│   ├── etl_connector.py    # Main ETL script
│
├── .gitignore              # Ignore sensitive files
├── README.md               # Project documentation
└── requirements.txt        # Python dependencies
```

***

## 🔧 Environment Variables
Create a `.env` file inside the `threatfox_connector/` directory:

```env
THREATFOX_JSON_URL=https://threatfox.abuse.ch/export/json/recent/
MONGO_URI=mongodb://localhost:27017/
MONGO_DB=etl_db
MONGO_COLLECTION=threatfox_recent
```

***

## 🚀 Installation & Setup

### **1. Clone the repository**
```bash
git clone https://github.com/Kyureeus-Edtech/custom-python-etl-data-connector-krishnaraj710.git
cd custom-python-etl-data-connector-krishnaraj710/threatfox_connector
```

### **2. Create and activate a virtual environment**
```bash
python3 -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate
```

### **3. Install dependencies**
```bash
pip install -r requirements.txt
```

### **4. Start MongoDB locally**
```bash
sudo service mongod start
```

### **5. Run the ETL script**
```bash
python etl_connector.py
```


## 📊 Verifying the Data
After running the ETL process, check inserted documents in MongoDB:

```bash
mongosh
use etl_db
db.threatfox_recent.find().pretty()
```

## 🧪 Testing & Validation
- **Empty Payloads:** Handled gracefully with warnings.
- **Invalid JSON:** Raises exceptions with detailed logging.
- **MongoDB Key Compatibility:** Replaces all `.` and `$` in keys.

