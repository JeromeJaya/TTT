# Tic Tac Toe - MongoDB Atlas Setup Guide

## 📋 Prerequisites
- Node.js installed (v14 or higher)
- MongoDB Atlas account (free tier available)

## 🚀 Step-by-Step Setup

### Step 1: Set Up MongoDB Atlas

1. **Create MongoDB Atlas Account**
   - Go to https://www.mongodb.com/cloud/atlas
   - Sign up for a free account

2. **Create a Cluster**
   - Click "Build a Database"
   - Choose "FREE" tier (M0)
   - Select a cloud provider and region closest to you
   - Click "Create Cluster"

3. **Create Database User**
   - In the left sidebar, click "Database Access"
   - Click "Add New Database User"
   - Choose "Password" authentication
   - Create a username and password (save these!)
   - Set privileges to "Read and write to any database"
   - Click "Add User"

4. **Whitelist Your IP**
   - Click "Network Access" in the left sidebar
   - Click "Add IP Address"
   - Click "Allow Access from Anywhere" (0.0.0.0/0) for development
   - Click "Confirm"

5. **Get Connection String**
   - Click "Database" in the left sidebar
   - Click "Connect" on your cluster
   - Choose "Connect your application"
   - Copy the connection string (looks like: `mongodb+srv://username:password@cluster0.xxxxx.mongodb.net/`)
   - Replace `<password>` with your database user password

### Step 2: Configure the Backend

1. **Navigate to Project Directory**
   ```bash
   cd "/home/dell/Desktop/TIC TOC TOE"
   ```

2. **Install Dependencies**
   ```bash
   npm install
   ```

3. **Create .env File**
   ```bash
   cp .env.example .env
   ```

4. **Edit .env File**
   Open `.env` and replace the MONGODB_URI with your actual MongoDB Atlas connection string:
   ```
   MONGODB_URI=mongodb+srv://your-username:your-password@cluster0.xxxxx.mongodb.net/tictactoe?retryWrites=true&w=majority
   PORT=3000
   ```

### Step 3: Run the Backend Server

```bash
npm start
```

Or for development with auto-reload:
```bash
npm run dev
```

You should see:
```
🚀 Server is running on port 3000
✅ Connected to MongoDB Atlas
```

### Step 4: Open the Frontend

1. Open `index.html` in your browser
2. You can now:
   - Register new users (data saved to MongoDB Atlas)
   - Login with registered credentials

## 📁 Project Structure

```
TIC TOC TOE/
├── server.js           # Backend server (Express + MongoDB)
├── package.json        # Node.js dependencies
├── .env               # Environment variables (DO NOT commit)
├── .env.example       # Example environment file
├── .gitignore         # Git ignore file
├── index.html         # Login/Register page
├── dashboard.html     # User dashboard
└── script.js          # Game logic
```

## 🔐 Security Features

- **Password Hashing**: Uses bcryptjs to hash passwords before storing
- **Input Validation**: Validates all user inputs
- **Unique Usernames**: Prevents duplicate usernames
- **CORS Enabled**: Manual CORS headers for frontend-backend communication

## 📦 Dependencies

- **mongoose**: MongoDB object modeling
- **bcryptjs**: Password hashing
- **dotenv**: Environment variables
- **nodemon**: Auto-restart during development (dev dependency)
- **http**: Built-in Node.js module (no external framework)
- **url**: Built-in Node.js module for URL parsing

## 🧪 Testing the API

You can test the endpoints using curl or Postman:

**Register a user:**
```bash
curl -X POST http://localhost:3000/register \
  -H "Content-Type: application/json" \
  -d '{"username":"testuser","password":"testpass123"}'
```

**Login:**
```bash
curl -X POST http://localhost:3000/login \
  -H "Content-Type: application/json" \
  -d '{"username":"testuser","password":"testpass123"}'
```

## ❌ Troubleshooting

**MongoDB Connection Error:**
- Check your MONGODB_URI in .env file
- Ensure your IP is whitelisted in MongoDB Atlas
- Verify database user credentials are correct

**Port Already in Use:**
- Change the PORT in .env file to another port (e.g., 3001)
- Or kill the process using: `lsof -ti:3000 | xargs kill`
