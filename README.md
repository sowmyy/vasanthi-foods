# Vasanthi Foods - Cloud Kitchen Ordering System

A complete full-stack web application for managing cloud kitchen orders with authentication, payment integration, and admin panel.

## 🌟 Features

### Customer Features
- **User Authentication** - Secure signup and login
- **Browse Menu** - View delicious Indian cuisine by category
- **Shopping Cart** - Add items and manage quantities
- **Coupon System** - Apply discount codes at checkout
- **Multiple Payment Options** - Razorpay (UPI, Cards, Wallets), Stripe, PayPal, Cash on Delivery
- **Order Tracking** - Real-time order status updates
- **Order History** - View all past orders
- **Delivery Time Estimates** - Know when to expect your food
- **Mobile Responsive** - Works perfectly on all devices

### Admin Features
- **Dashboard** - View key metrics (orders, revenue, customers)
- **Menu Management** - Add, edit, delete menu items
- **Order Management** - Update order status in real-time
- **Coupon Management** - Create and manage discount codes
- **Pricing Control** - Update item prices anytime

## 🎨 Design
- **Color Palette:**
  - Primary: #628141 (Olive Green)
  - Accent: #F1C40F (Bright Yellow)
  - Background: #F9F9F9 (Off-White)
  - Secondary: #40513B (Dark Green)
- **Flat Design** with modern UI components
- **Mobile-first responsive** design

## 🛠️ Technology Stack

### Backend
- **Node.js** with Express.js
- **MongoDB** with Mongoose ODM
- **JWT** for authentication
- **bcryptjs** for password hashing

### Frontend
- **React** (via CDN)
- **Vanilla CSS** with custom design system
- **Responsive Grid** layouts

### Payment Integrations
- **Razorpay** - For Indian payments (UPI, Cards, Wallets)
- **Stripe** - For international cards
- **PayPal** - Alternative payment method
- **Cash on Delivery** option

## 📋 Prerequisites

Before you begin, ensure you have installed:
- **Node.js** (v14 or higher)
- **MongoDB** (v4.4 or higher)
- **npm** or **yarn**

## 🚀 Installation & Setup

### 1. Clone or Download the Project
```bash
cd vasanthi-foods-app
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Setup Environment Variables
Create a `.env` file in the root directory:
```bash
cp .env.example .env
```

Edit `.env` and add your configuration:
```env
MONGODB_URI=mongodb://localhost:27017/vasanthi-foods
JWT_SECRET=your-super-secret-jwt-key-change-this
PORT=3000

# Payment Gateway Keys
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret
STRIPE_SECRET_KEY=your_stripe_secret_key
```

### 4. Start MongoDB
Make sure MongoDB is running on your system:
```bash
# On macOS with Homebrew
brew services start mongodb-community

# On Ubuntu/Debian
sudo systemctl start mongod

# On Windows
net start MongoDB
```

### 5. Run the Application
```bash
npm start
```

For development with auto-reload:
```bash
npm run dev
```

### 6. Access the Application
Open your browser and navigate to:
```
http://localhost:3000
```

## 🔐 Default Admin Credentials

The application automatically creates a default admin account:

- **Email:** admin@vasanthifoods.com
- **Password:** admin123

⚠️ **Important:** Change these credentials immediately after first login!

## 💳 Payment Gateway Setup

### Razorpay Setup
1. Sign up at [https://razorpay.com](https://razorpay.com)
2. Get your API keys from Dashboard → Settings → API Keys
3. Add `RAZORPAY_KEY_ID` to your `.env` file
4. Update the Razorpay key in `public/index.html` (search for `rzp_test_DEMO_KEY`)

### Stripe Setup
1. Sign up at [https://stripe.com](https://stripe.com)
2. Get your API keys from Dashboard → Developers → API keys
3. Add `STRIPE_SECRET_KEY` to your `.env` file

### PayPal Setup
1. Sign up at [https://developer.paypal.com](https://developer.paypal.com)
2. Create an app to get Client ID and Secret
3. Add credentials to your `.env` file

## 📱 Usage Guide

### For Customers

1. **Sign Up / Login**
   - Click "Sign Up" to create a new account
   - Fill in your details including delivery address
   - Login with your credentials

2. **Browse Menu**
   - View menu items by category
   - See prices and descriptions
   - Filter by category tabs

3. **Add to Cart**
   - Click "Add to Cart" on any item
   - View cart by clicking the cart icon
   - Adjust quantities using +/- buttons

4. **Checkout**
   - Enter delivery address and phone
   - Apply coupon code if available
   - Select payment method
   - Place order

5. **Track Orders**
   - View "My Orders" to see all orders
   - Check order status and estimated delivery time
   - View order history

### For Admins

1. **Login**
   - Use admin credentials
   - Access admin dashboard automatically

2. **Manage Menu**
   - Add new items with name, description, price, category
   - Edit existing items
   - Mark items as available/unavailable
   - Delete items

3. **Manage Orders**
   - View all customer orders
   - Update order status in real-time
   - See customer details

4. **Manage Coupons**
   - Create discount codes
   - Set percentage or fixed discounts
   - Set minimum order requirements
   - Set maximum discount limits

## 📂 Project Structure

```
vasanthi-foods-app/
├── server.js           # Backend server & API endpoints
├── package.json        # Dependencies & scripts
├── .env.example        # Environment variables template
├── README.md          # This file
└── public/
    └── index.html     # Frontend React application
```

## 🔧 API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/me` - Get current user

### Menu
- `GET /api/menu` - Get available menu items
- `GET /api/menu/all` - Get all menu items (admin)
- `POST /api/menu` - Add menu item (admin)
- `PUT /api/menu/:id` - Update menu item (admin)
- `DELETE /api/menu/:id` - Delete menu item (admin)

### Orders
- `POST /api/orders` - Create new order
- `GET /api/orders/my-orders` - Get user's orders
- `GET /api/orders/all` - Get all orders (admin)
- `GET /api/orders/:id` - Get order details
- `PUT /api/orders/:id/status` - Update order status (admin)
- `POST /api/orders/:id/payment` - Update payment status

### Coupons
- `GET /api/coupons` - Get all coupons (admin)
- `POST /api/coupons/validate` - Validate coupon code
- `POST /api/coupons` - Create coupon (admin)
- `PUT /api/coupons/:id` - Update coupon (admin)
- `DELETE /api/coupons/:id` - Delete coupon (admin)

### Stats
- `GET /api/stats` - Get dashboard statistics (admin)

## 🔒 Security Features

- Password hashing with bcryptjs
- JWT token-based authentication
- Role-based access control (customer/admin)
- Protected API routes
- Input validation

## 📱 Mobile Responsive

The application is fully responsive and works on:
- Desktop (1200px+)
- Tablet (768px - 1199px)
- Mobile (< 768px)

## 🎯 Future Enhancements

Potential features to add:
- SMS/Email notifications for order updates
- Rating and review system
- Image uploads for menu items
- Advanced analytics dashboard
- Customer favorites/wishlists
- Delivery person tracking
- Multi-language support
- Push notifications

## 🐛 Troubleshooting

### MongoDB Connection Error
```
Error: connect ECONNREFUSED 127.0.0.1:27017
```
**Solution:** Make sure MongoDB is running. Start it using the commands in step 4 above.

### Port Already in Use
```
Error: listen EADDRINUSE: address already in use :::3000
```
**Solution:** Either kill the process using port 3000 or change the PORT in `.env` file.

### Payment Gateway Errors
**Solution:** Ensure you've added the correct API keys in `.env` and updated the frontend code with your publishable keys.

## 📄 License

This project is open source and available for personal and commercial use.

## 👨‍💻 Support

For issues and questions:
1. Check the troubleshooting section
2. Review the code comments
3. Ensure all dependencies are installed
4. Verify environment variables are set correctly

## 🎉 Enjoy Vasanthi Foods!

Thank you for using our cloud kitchen ordering system. We hope it serves your business well!
