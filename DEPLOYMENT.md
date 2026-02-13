# Deployment Guide - Vasanthi Foods

## 🚀 Deploying to Production

### Option 1: Deploy to Heroku (Recommended for Beginners)

#### Prerequisites
- Heroku account ([signup here](https://signup.heroku.com/))
- Heroku CLI installed

#### Steps

1. **Install Heroku CLI**
```bash
# macOS
brew tap heroku/brew && brew install heroku

# Ubuntu
curl https://cli-assets.heroku.com/install.sh | sh

# Windows
# Download from https://devcenter.heroku.com/articles/heroku-cli
```

2. **Login to Heroku**
```bash
heroku login
```

3. **Create Heroku App**
```bash
heroku create vasanthi-foods-app
```

4. **Add MongoDB**
```bash
heroku addons:create mongolab:sandbox
```

5. **Set Environment Variables**
```bash
heroku config:set JWT_SECRET=your-super-secret-jwt-key
heroku config:set RAZORPAY_KEY_ID=your_razorpay_key
heroku config:set RAZORPAY_KEY_SECRET=your_razorpay_secret
```

6. **Deploy**
```bash
git init
git add .
git commit -m "Initial commit"
git push heroku main
```

7. **Open App**
```bash
heroku open
```

### Option 2: Deploy to DigitalOcean

#### Prerequisites
- DigitalOcean account
- SSH access to droplet

#### Steps

1. **Create Droplet**
   - Choose Ubuntu 22.04
   - Select plan (minimum $6/month)
   - Add SSH key

2. **Connect to Droplet**
```bash
ssh root@your_droplet_ip
```

3. **Install Node.js & MongoDB**
```bash
# Update system
apt update && apt upgrade -y

# Install Node.js
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
apt install -y nodejs

# Install MongoDB
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-6.0.list
apt update
apt install -y mongodb-org
systemctl start mongod
systemctl enable mongod
```

4. **Clone & Setup Application**
```bash
cd /var/www
git clone your_repository_url vasanthi-foods
cd vasanthi-foods
npm install
```

5. **Configure Environment**
```bash
nano .env
# Add your configuration
```

6. **Install PM2 (Process Manager)**
```bash
npm install -g pm2
pm2 start server.js --name vasanthi-foods
pm2 startup
pm2 save
```

7. **Setup Nginx**
```bash
apt install -y nginx

# Create Nginx config
nano /etc/nginx/sites-available/vasanthi-foods
```

Add this configuration:
```nginx
server {
    listen 80;
    server_name your_domain.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

```bash
# Enable site
ln -s /etc/nginx/sites-available/vasanthi-foods /etc/nginx/sites-enabled/
nginx -t
systemctl restart nginx
```

8. **Setup SSL (Optional but Recommended)**
```bash
apt install -y certbot python3-certbot-nginx
certbot --nginx -d your_domain.com
```

### Option 3: Deploy to AWS EC2

#### Steps

1. **Launch EC2 Instance**
   - Choose Ubuntu Server 22.04
   - t2.micro (free tier eligible)
   - Configure security groups (allow ports 22, 80, 443, 3000)

2. **Connect & Setup**
```bash
ssh -i your-key.pem ubuntu@your-ec2-ip

# Follow similar steps as DigitalOcean above
```

### Option 4: Deploy to Railway

1. Visit [railway.app](https://railway.app)
2. Click "New Project"
3. Select "Deploy from GitHub"
4. Choose your repository
5. Add environment variables
6. Railway will auto-deploy

### Option 5: Deploy to Render

1. Visit [render.com](https://render.com)
2. Click "New +"
3. Select "Web Service"
4. Connect GitHub repository
5. Configure:
   - Build Command: `npm install`
   - Start Command: `npm start`
6. Add environment variables
7. Click "Create Web Service"

## 🔒 Production Checklist

Before deploying to production, ensure:

- [ ] Changed default admin password
- [ ] Updated JWT_SECRET to a strong random value
- [ ] Added real payment gateway credentials
- [ ] Set NODE_ENV=production
- [ ] Configured CORS properly
- [ ] Setup SSL certificate
- [ ] Configured database backups
- [ ] Setup monitoring (e.g., PM2, New Relic)
- [ ] Setup error logging (e.g., Sentry)
- [ ] Tested all payment flows
- [ ] Removed console.log statements
- [ ] Optimized images and assets
- [ ] Setup CDN for static files (optional)
- [ ] Configure rate limiting
- [ ] Setup automated backups

## 🔐 Security Best Practices

1. **Use Environment Variables**
   - Never commit `.env` to git
   - Use different keys for dev/prod

2. **Enable HTTPS**
   - Use Let's Encrypt for free SSL
   - Redirect HTTP to HTTPS

3. **Secure MongoDB**
   - Enable authentication
   - Use strong passwords
   - Whitelist IP addresses

4. **Rate Limiting**
   - Add rate limiting to prevent abuse
   - Use express-rate-limit package

5. **Input Validation**
   - Validate all user inputs
   - Sanitize data before storing

6. **Regular Updates**
   - Keep dependencies updated
   - Monitor security advisories

## 📊 Monitoring & Maintenance

### Setup PM2 Monitoring
```bash
pm2 install pm2-logrotate
pm2 set pm2-logrotate:max_size 10M
pm2 set pm2-logrotate:retain 7
```

### Database Backups
```bash
# Create backup script
nano /root/backup-db.sh
```

```bash
#!/bin/bash
BACKUP_DIR="/backups/mongodb"
DATE=$(date +%Y%m%d_%H%M%S)
mkdir -p $BACKUP_DIR
mongodump --out=$BACKUP_DIR/$DATE
# Keep only last 7 days
find $BACKUP_DIR -mtime +7 -delete
```

```bash
chmod +x /root/backup-db.sh
# Add to crontab (daily at 2 AM)
crontab -e
0 2 * * * /root/backup-db.sh
```

## 🌐 Domain & DNS Setup

1. **Purchase Domain**
   - GoDaddy, Namecheap, Google Domains, etc.

2. **Configure DNS**
   - Add A record pointing to your server IP
   - Wait for DNS propagation (can take 24-48 hours)

3. **Update Application**
   - Update CORS settings to include your domain
   - Configure SSL certificate

## 📱 Mobile App (Future)

To convert to mobile app:
1. Use React Native or Flutter
2. Keep the same backend API
3. Or use Capacitor to wrap the web app

## 🎯 Performance Optimization

1. **Enable Compression**
```javascript
const compression = require('compression');
app.use(compression());
```

2. **Add Caching**
```javascript
const mcache = require('memory-cache');
// Cache middleware
```

3. **Database Indexing**
```javascript
// Add indexes to frequently queried fields
MenuItemSchema.index({ category: 1, available: 1 });
OrderSchema.index({ userId: 1, createdAt: -1 });
```

4. **Use CDN**
   - Host static assets on CDN
   - Cloudflare, AWS CloudFront, etc.

## 🆘 Support

For deployment issues:
- Check application logs: `pm2 logs vasanthi-foods`
- Check Nginx logs: `tail -f /var/log/nginx/error.log`
- Check MongoDB logs: `journalctl -u mongod`

Good luck with your deployment! 🚀
