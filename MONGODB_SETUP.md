# MongoDB Setup Guide for AgRO NXT

The application requires MongoDB to store user data and other information. Here are three ways to set it up:

## Option 1: Install MongoDB Community Edition Locally (Recommended for Development)

### Windows:
1. Download MongoDB Community Edition from: https://www.mongodb.com/try/download/community
2. Run the installer and follow the default settings
3. MongoDB will be installed as a Windows Service and should start automatically
4. Verify installation by opening PowerShell and running:
   ```powershell
   mongod --version
   ```

### macOS (using Homebrew):
```bash
brew tap mongodb/brew
brew install mongodb-community
brew services start mongodb-community
```

### Linux (Ubuntu/Debian):
```bash
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
sudo systemctl start mongod
```

---

## Option 2: Use MongoDB Atlas (Cloud - No Installation Needed)

This is the easiest option if you don't want to install anything locally.

1. Go to: https://www.mongodb.com/cloud/atlas
2. Create a free account (M0 tier is free forever)
3. Create a new cluster
4. Get your connection string (it will look like):
   ```
   mongodb+srv://username:password@cluster.mongodb.net/agro-nxt?retryWrites=true&w=majority
   ```
5. Update the `.env` file in the `server` directory:
   ```
   MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/agro-nxt?retryWrites=true&w=majority
   ```

---

## Option 3: Use Docker (Easiest Alternative)

If you have Docker installed:

```powershell
# Start MongoDB in a Docker container
docker run -d -p 27017:27017 --name mongodb mongo

# Verify it's running
docker ps
```

The MongoDB URI remains: `mongodb://localhost:27017/agro-nxt`

To stop: `docker stop mongodb`
To remove: `docker rm mongodb`

---

## Verify MongoDB Connection

After setup, restart the backend server:

```bash
cd server
npm start
```

You should see: ✅ MongoDB connected successfully

Then try logging in with:
- **Email:** farmer@agro.com
- **Password:** password123

If the user doesn't exist, you need to seed the database:

```bash
cd server
npm run seed
```

---

## Troubleshooting

### "MongoDB connection error"
- Ensure MongoDB is running
- Check that `MONGODB_URI` in `.env` is correct
- For local MongoDB, make sure port 27017 is not blocked

### Port 27017 already in use
- Windows: `netstat -ano | findstr :27017`
- Mac/Linux: `lsof -i :27017`

### Atlas Connection Timeout
- Check your IP whitelist in MongoDB Atlas
- Ensure username/password are correct (special characters need to be URL-encoded)

---

## Next Steps

After MongoDB is running:

1. Seed demo data:
   ```bash
   cd server
   npm run seed
   ```

2. Start the development servers:
   ```bash
   ./start.bat  (Windows)
   ./start.sh   (Mac/Linux)
   ```

3. Access the application at: http://localhost:3000

---

## Default Demo Credentials (after seeding)
- **Email:** farmer@agro.com
- **Password:** password123
