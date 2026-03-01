# 🚀 AgRO NXT - Quick Start Guide

## Status: Project Running ✅

Your AgRO NXT project is now running! However, to use the full application, you need to set up MongoDB.

---

## ⚡ Quick Setup (5 minutes)

### Prerequisites:
- Node.js v16+ (Already installed ✓)
- MongoDB or Docker (Choose one option below)

### Choose Your Setup:

#### Option A: Docker (Easiest - No Installation) ⭐
```powershell
# Install Docker if you don't have it: https://www.docker.com/products/docker-desktop

# Start MongoDB
docker run -d -p 27017:27017 --name mongodb mongo

# Seed database with demo data
cd server
npm run seed

# Done! You can now log in
```

#### Option B: MongoDB Community Edition
1. Download: https://www.mongodb.com/try/download/community
2. Install with default settings
3. Open PowerShell and verify: `mongod --version`
4. Seed database:
   ```powershell
   cd server
   npm run seed
   ```

#### Option C: MongoDB Atlas (Cloud)
1. Create free account: https://www.mongodb.com/cloud/atlas
2. Create a cluster (M0 tier is free)
3. Get connection string from Atlas
4. Update `server/.env`:
   ```
   MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/agro-nxt?retryWrites=true&w=majority
   ```
5. Seed database:
   ```powershell
   cd server
   npm run seed
   ```

---

## 🎯 After Setup

### Test Login with Demo Credentials:
- **URL:** http://localhost:3000
- **Email:** farmer@agro.com
- **Password:** password123

### Server Status:
- **Frontend:** http://localhost:3000 (React)
- **Backend:** http://localhost:5000 (Express)
- **Health Check:** http://localhost:5000/api/health

---

## 📝 What's Fixed

✅ **Improved MongoDB Connection Handling**
- Better error messages and retry logic
- Connection pooling and timeouts
- Detailed logging for debugging

✅ **Enhanced Error Responses**
- Database connection errors now show helpful setup instructions
- Better error messages in authentication routes
- Fallback JWT secret in development

✅ **Improved Seed Script**
- Prevents duplicate data creation
- Better error handling
- Clear success/failure messages

✅ **Better Client Error Handling**
- Shows MongoDB setup instructions when database is unavailable
- Pre-filled demo credentials for easy testing
- Clear warning messages

---

## 🆘 Troubleshooting

### "Database connection failed"
→ Follow the "Choose Your Setup" section above

### "Port 27017 already in use"
- Another MongoDB instance is running
- Find it: `netstat -ano | findstr :27017`
- Stop it or use a different port

### "Windows PowerShell - command not found"
- Use `.\` prefix: `.\server\seed.js`
- Or use CMD interpreter

### Still having issues?
1. Check [MONGODB_SETUP.md](./MONGODB_SETUP.md) for detailed instructions
2. Verify all services are running:
   ```powershell
   netstat -ano | findstr :5000    # Backend
   netstat -ano | findstr :3000    # Frontend
   netstat -ano | findstr :27017   # Database
   ```

---

## 📚 Project Structure

```
agri_nxt-portal/
├── client/                 # React Frontend
│   ├── src/
│   │   ├── components/    # Reusable components
│   │   ├── pages/         # Page components
│   │   └── services/      # API services
│   └── package.json
├── server/                 # Node.js Backend
│   ├── models/            # Database schemas
│   ├── routes/            # API endpoints
│   ├── middleware/        # Auth & error handling
│   ├── seed.js            # Database seeding
│   └── package.json
├── MONGODB_SETUP.md       # Detailed MongoDB setup
└── README.md              # Project overview
```

---

## 🎓 Features

- **Dashboard:** Real-time farm analytics
- **Crop Recommendation:** AI-powered crop suggestions
- **Profit Simulation:** Financial forecasting
- **Government Schemes:** Scheme eligibility checker
- **Farm Management:** CRUD operations for farms
- **Sustainability:** Environmental impact calculation
- **Voice Assistant:** Coming soon!

---

## ✨ Next Steps

1. **Set up MongoDB** (choose Option A, B, or C above)
2. **Run seed script:** `npm run seed` in server directory
3. **Visit:** http://localhost:3000
4. **Log in** with demo credentials
5. **Explore** all features!

---

**Need help?** Check the detailed guides:
- [MONGODB_SETUP.md](./MONGODB_SETUP.md) - Complete MongoDB setup
- [PROJECT_STRUCTURE.md](./PROJECT_STRUCTURE.md) - Codebase overview
- [IMPLEMENTATION.md](./IMPLEMENTATION.md) - Feature details
