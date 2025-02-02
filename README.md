# Analytics Platform - Setup Guide

## Project Overview

This project is a data analytics platform that retrieves time-series data from MongoDB and visualizes it using Chart.js. It allows users to:

- Filter data by date range
- Select specific fields for analysis
- View statistical metrics such as average, min, max, and standard deviation

## Prerequisites

Before running the project, install the following:

1. Node.js (v16+ recommended) – https://nodejs.org/
2. MongoDB Community Edition – https://www.mongodb.com/try/download/community
3. MongoDB Compass (GUI for MongoDB) – https://www.mongodb.com/products/compass
4. A web browser (Chrome, Firefox, Edge, etc.)

## Step-by-Step Installation Guide

### Step 1: Open PowerShell as Administrator

Press Win + S, type "PowerShell," right-click it, and select "Run as administrator."

### Step 2: Install Dependencies

Run the following command in PowerShell to install required dependencies:

```
npm install -g nodemon
```

### Step 3: Clone or Download the Repository

Navigate to the directory where you want to save the project and run:

```
git clone https://github.com/your-repository/analytics-platform.git
cd analytics-platform
```

If the project was downloaded as a ZIP file, extract it manually.

### Step 4: Start MongoDB

#### Option 1: Using Command Line

Create a data directory for MongoDB:

```
mkdir C:\data\db
```

Start MongoDB:

```
mongod --dbpath C:\data\db
```

#### Option 2: Using MongoDB as a Windows Service

If installed via MSI, start it with:

```
net start MongoDB
```

### Step 5: Verify MongoDB is Running

Check if MongoDB is running by opening MongoDB Shell:

```
mongosh
```

Then type:

```
show dbs
```

If MongoDB is working, it should list available databases.

### Step 6: Import Sample Data

If the database is empty, open MongoDB Shell and run:

```
use analytics
db.measurements.insertMany([
  { timestamp: new Date("2025-01-01T12:00:00Z"), field1: 22.5, field2: 65, field3: 400 },
  { timestamp: new Date("2025-01-01T13:00:00Z"), field1: 23.1, field2: 67, field3: 420 },
  { timestamp: new Date("2025-01-01T14:00:00Z"), field1: 21.8, field2: 64, field3: 410 }
])
```

Then exit:

```
exit
```

### Step 7: Setup Backend

Navigate to the backend folder:

```
cd backend
npm install
```

#### Installed Dependencies:

The backend dependencies are in package.json:

```
"dependencies": {
  "express": "^4.21.2",
  "mongoose": "^8.9.6"
}
```

### Step 8: Start the Backend Server

Run the backend:

```
node index.js
```

If successful, the output should be:

```
Server running on port 3000
```

### Step 9: Test API Endpoints

Open PowerShell or Postman and run:

Fetch time-series data:

```
curl "http://localhost:3000/api/measurements?field=field1&start_date=2025-01-01&end_date=2025-01-02"
```

Fetch statistical metrics:

```
curl "http://localhost:3000/api/measurements/metrics?field=field1"
```

If errors occur, ensure MongoDB is running (`mongod`) and the backend server is started (`node index.js`).

### Step 10: Setup Frontend

Navigate to the frontend folder:

```
cd ../frontend
```

#### Frontend Dependencies

The frontend uses Chart.js, which is loaded via CDN in index.html:

```
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
```

### Step 11: Open Frontend

Simply open index.html in a browser:

- Windows: Double-click index.html
- Linux/Mac: Open it manually in Chrome/Firefox

The interface should display a form where users can select the field, enter start and end dates, and fetch the data.

## Troubleshooting

### MongoDB Not Found?

Run:

```
where mongod
```

If not found, add its path to your system PATH variable.

### Port 3000 is Already in Use?

Find the process:

```
netstat -ano | findstr :3000
```

Kill it:

```
taskkill /PID <PROCESS_ID> /F
```

### npm install Fails?

Ensure package.json exists inside `backend/`. If missing, recreate it:

```
cd backend
npm init -y
```

## Conclusion

The project should now be fully operational with:

- A running MongoDB database
- A working backend API on port 3000
- A frontend UI displaying analytics
