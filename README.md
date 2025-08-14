ThreatFox ETL Data Connector
📌 Overview

This project implements an ETL (Extract, Transform, Load) pipeline that retrieves recent threat intelligence data from the ThreatFox API, processes it for MongoDB compatibility, and stores it in a MongoDB collection for further analysis.The pipeline is implemented in Python with modular functions for extracting, transforming, and loading data, and follows security best practices by storing sensitive credentials in environment variables.

📂 Features

Extract: 
Fetches JSON threat data from ThreatFox API endpoint.

Transform:
Cleans keys with prohibited characters (. and $) for MongoDB.Adds ingestion timestamps for tracking.

Load: 
Inserts cleaned documents into MongoDB for persistence.
Secure Config: API URLs and MongoDB connection strings are stored in a .env file and ignored by Git.

🔗 API Details

Base URL: Stored in .env as THREATFOX_JSON_URL
Authentication: No API key required for public endpoint.

Example Endpoint:
https://threatfox.abuse.ch/export/json/recent/

⚙️ Project Structure
custom-python-etl-data-connector-krishnaraj710/
│
├── threatfox_connector/
│   ├── etl_connector.py    # Main ETL script
│
├── .gitignore              # Ignores sensitive files
├── README.md               # Project documentation
└── requirements.txt        # Python dependencies

🔧 Environment Variables

Create a .env file inside the threatfox_connector/ directory:

🚀 Installation & Setup

Clone the repository
git clone https://github.com/Kyureeus-Edtech/custom-python-etl-data-connector-krishnaraj710.git
cd custom-python-etl-data-connector-krishnaraj710/threatfox_connector

Create and activate a virtual environment
python3 -m venv venv
source venv/bin/activate

Install dependencies
pip install -r requirements.txt

Run MongoDB locally
sudo service mongod start

Run the ETL script
python etl_connector.py

After running the ETL, you can verify inserted documents in MongoDB shell:

mongosh
use etl_db
db.threatfox_recent.find().pretty()

Testing & Validation

Empty Payloads: Handled gracefully with warnings.
Invalid JSON: Raises exceptions with detailed logs.
MongoDB Key Issues: All . and $ in keys are replaced to ensure compatibility.
