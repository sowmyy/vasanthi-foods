# Payment Integration Setup Guide

## Important Note

Due to network restrictions, the payment gateway SDKs (Stripe, Razorpay) are not installed by default.
The application works perfectly without them for Cash on Delivery orders.

## Current Payment Options

✅ **Cash on Delivery** - Works out of the box, no setup needed

## Adding Payment Gateways (Optional)

### Option 1: Add Later When Deploying

When you deploy to a production server (Heroku, DigitalOcean, AWS), you'll have proper internet access to install payment packages.

Add to package.json dependencies:
```json
"stripe": "^10.0.0",
"razorpay": "^2.8.0"
```

### Option 2: Manual Setup for Testing

If you want to test payments locally:

1. **Get API Keys** (Test Mode)
   - Razorpay: https://dashboard.razorpay.com/signup
   - Stripe: https://dashboard.stripe.com/register

2. **Add to .env file:**
   ```
   RAZORPAY_KEY_ID=rzp_test_xxxxxxxxxx
   RAZORPAY_KEY_SECRET=xxxxxxxxxxxxx
   STRIPE_SECRET_KEY=sk_test_xxxxxxxxxxxxx
   ```

3. **Update frontend** (public/index.html):
   - Replace `rzp_test_DEMO_KEY` with your actual Razorpay Key ID (line ~1360)

4. **Install packages when you have internet:**
   ```bash
   npm install razorpay stripe --save
   ```

### Option 3: Use COD Only (Recommended for Now)

The application works perfectly with Cash on Delivery. You can:
- Take orders
- Track orders
- Manage menu
- Use coupons
- Everything except online payment processing

When customers select COD:
- Order is created immediately
- Status is set to "pending"
- Admin can confirm and process
- Payment is collected on delivery

## Testing Without Payment Gateways

1. Start the application: `npm start`
2. Register as a customer
3. Add items to cart
4. Select "Cash on Delivery"
5. Place order
6. Login as admin to manage the order

## For Production Deployment

When you're ready to go live:

1. Deploy to proper hosting (Heroku/DigitalOcean/AWS)
2. Install payment packages on the server
3. Add your production payment keys
4. Test with small amounts first
5. Enable production mode on payment dashboards

## Payment Gateway Documentation

- **Razorpay Docs**: https://razorpay.com/docs/
- **Stripe Docs**: https://stripe.com/docs
- **PayPal Docs**: https://developer.paypal.com/docs/

## Need Help?

For now, use Cash on Delivery for testing. When deploying to production with proper internet access, you can easily add payment gateways by following the documentation links above.
