# Lab M2.07 - Deploy Node.js Application

**Repository:** [https://github.com/cloud-engineering-bootcamp/ce-lab-deploy-nodejs-app](https://github.com/cloud-engineering-bootcamp/ce-lab-deploy-nodejs-app)

**Activity Type:** Individual  
**Estimated Time:** 45-60 minutes

## Learning Objectives

- [ ] Deploy complete Node.js application to EC2
- [ ] Configure environment variables securely
- [ ] Set up application as systemd service
- [ ] Implement health checks
- [ ] Monitor application with PM2

## Your Task

Deploy a production-ready Node.js Express application:
1. Install Node.js and dependencies
2. Deploy application code from Git
3. Configure environment variables
4. Set up PM2 process manager
5. Configure Nginx reverse proxy
6. Add health check endpoint

**Success:** Application running, accessible from internet, survives reboot

## Sample Application

```javascript
// app.js
const express = require('express');
const app = express();
const port = process.env.PORT || 8080;

app.get('/', (req, res) => {
  res.json({
    message: 'Week 2 Deployment Lab',
    hostname: process.env.HOSTNAME,
    uptime: process.uptime(),
    environment: process.env.NODE_ENV || 'development'
  });
});

app.get('/health', (req, res) => {
  res.json({ status: 'healthy', timestamp: new Date() });
});

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

## Deployment Commands

```bash
# Install Node.js
curl -sL https://rpm.nodesource.com/setup_18.x | sudo bash -
sudo yum install -y nodejs

# Deploy application
mkdir ~/app && cd ~/app
npm init -y
npm install express

# Create app.js (paste above code)

# Install PM2
sudo npm install -g pm2

# Start with PM2
pm2 start app.js --name myapp
pm2 startup
pm2 save

# Configure Nginx
sudo yum install -y nginx
sudo tee /etc/nginx/conf.d/app.conf <<EOF
server {
    listen 80;
    location / {
        proxy_pass http://localhost:8080;
        proxy_http_version 1.1;
        proxy_set_header Host \$host;
    }
}
EOF

sudo systemctl start nginx
sudo systemctl enable nginx
```

## 📤 What to Submit

**Submission Type:** GitHub Repository

Create a **public** GitHub repository named `ce-lab-deploy-nodejs` containing:
- Application code
- Deployment script
- Nginx configuration
- PM2 configuration
- Screenshots
- README with process

## Grading: 100 points
- Application deployed: 30pts
- PM2 configured: 20pts
- Nginx proxy working: 20pts
- Health check: 15pts
- Documentation: 15pts
