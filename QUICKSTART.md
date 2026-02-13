# 🚀 QUICK START GUIDE - Vasanthi Foods

## ⚠️ Important: Node.js Version

**You're currently on Node.js 10.19.0 which is outdated.**

### Upgrade Node.js (Recommended)

**Option 1 - Using nvm (Recommended):**
```bash
# Install nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# Close and reopen terminal, then:
nvm install 14
nvm use 14
node --version  # Should show v14.x.x
```

**Option 2 - Direct Installation:**
- macOS: Download from https://nodejs.org (choose LTS version)
- Windows: Download installer from https://nodejs.org
- Ubuntu: `sudo apt-get install nodejs npm`

### If You Can't Upgrade Node

The application has been configured to work with Node 10, but some features may be limited.

## 🎯 What You've Got

A complete, production-ready cloud kitchen ordering system with:
✅ Full-stack application (Frontend + Backend + Database)
✅ User authentication & authorization
✅ Menu management system
✅ Shopping cart & checkout
✅ Multiple payment integrations (Razorpay, Stripe, PayPal, COD)
✅ Order tracking with status updates
✅ Coupon/discount system
✅ Admin dashboard
✅ Mobile responsive design
✅ Beautiful UI with your color palette

## ⚡ Get Started in 5 Minutes

### 1️⃣ Install Requirements
```bash
# You need Node.js and MongoDB installed
# Check if you have them:
node --version  # Should be v14+
mongod --version  # Should be v4.4+
```

### 2️⃣ Navigate to the Project
```bash
cd vasanthi-foods-app
```

### 3️⃣ Install Dependencies
```bash
npm install
```

### 4️⃣ Start MongoDB
```bash
# macOS: brew services start mongodb-community
# Ubuntu: sudo systemctl start mongod
# Windows: net start MongoDB
```

### 5️⃣ Run the Application
```bash
npm start
```

### 6️⃣ Open Your Browser
```
http://localhost:3000
```

## 🔑 Default Admin Login

**Email:** admin@vasanthifoods.com  
**Password:** admin123

⚠️ **IMPORTANT:** Change this password immediately after first login!

## 📁 Project Files

```
vasanthi-foods-app/
├── server.js              # Backend API server
├── package.json           # Dependencies
├── .env.example          # Environment variables template
├── README.md             # Full documentation
├── DEPLOYMENT.md         # Deployment guide
└── public/
    └── index.html        # Frontend application
```

## 🎨 Your Color Palette

- **Primary:** #628141 (Olive Green)
- **Accent:** #F1C40F (Bright Yellow)
- **Background:** #F9F9F9 (Off-White)
- **Secondary:** #40513B (Dark Green)

## 💡 Next Steps

### For Testing
1. Login as admin (credentials above)
2. Add some menu items
3. Create a customer account
4. Place a test order
5. Update order status from admin panel

### For Production
1. Read `DEPLOYMENT.md` for deployment options
2. Get payment gateway API keys:
   - Razorpay: https://razorpay.com
   - Stripe: https://stripe.com
3. Update `.env` with your keys
4. Deploy to Heroku/DigitalOcean/AWS
5. Setup your domain

## 🔧 Configuration

Create `.env` file:
```bash
cp .env.example .env
```

Edit `.env` and add:
```
MONGODB_URI=mongodb://localhost:27017/vasanthi-foods
JWT_SECRET=change-this-to-random-string
RAZORPAY_KEY_ID=your_key
RAZORPAY_KEY_SECRET=your_secret
```

## 📱 Features Overview

### Customer Side
- Browse menu by category
- Add items to cart
- Apply discount coupons
- Multiple payment options
- Track order status
- View order history

### Admin Side
- Dashboard with statistics
- Add/edit/delete menu items
- Update pricing
- Manage orders
- Create discount coupons
- View all customers

## 🆘 Common Issues

**MongoDB Connection Error?**
→ Make sure MongoDB is running

**Port 3000 already in use?**
→ Change PORT in .env file or kill the process

**Payment not working?**
→ Add your payment gateway keys in .env

## 📚 Documentation

- `README.md` - Complete documentation
- `DEPLOYMENT.md` - How to deploy to production
- Code comments - Inline documentation

## 🎉 You're All Set!

Your cloud kitchen application is ready to use. Start by logging in as admin and adding your menu items!

For questions, check the README.md or review the code comments.

---
**Built for:** Vasanthi Foods  
**Created:** February 2026
