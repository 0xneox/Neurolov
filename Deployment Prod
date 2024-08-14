# Production Deployment Guide for NeuroLov GPU Tapping Game Backend

## 1. Choose a Hosting Provider

Select a cloud provider that suits your needs. Popular options include:
- Amazon Web Services (AWS)
- Google Cloud Platform (GCP)
- DigitalOcean
- Heroku

For this guide, we'll assume you're using AWS.

## 2. Set Up a Virtual Private Cloud (VPC)

- Create a new VPC in your chosen region
- Set up public and private subnets
- Configure route tables and internet gateways

## 3. Launch EC2 Instances

- Launch EC2 instances in the private subnet for your application servers
- Use a load balancer in the public subnet to distribute traffic

## 4. Set Up a Database

- Launch a MongoDB instance using Amazon DocumentDB or set up a MongoDB Atlas cluster
- Ensure it's in the private subnet and not publicly accessible

## 5. Set Up Redis (if used)

- Launch an Amazon ElastiCache for Redis instance in the private subnet

## 6. Configure Security Groups

- Set up security groups to control inbound and outbound traffic
- Allow only necessary ports (e.g., 80, 443 for web traffic)

## 7. Set Up a CI/CD Pipeline

- Use AWS CodePipeline or a service like Jenkins
- Configure it to pull from your GitHub repository, run tests, and deploy to EC2

## 8. Prepare Your Application

- Update your `config.js` to use environment variables
- Create a `ecosystem.config.js` for PM2 process management

```javascript
module.exports = {
  apps: [{
    name: 'neurolov-backend',
    script: 'app.js',
    instances: 'max',
    autorestart: true,
    watch: false,
    max_memory_restart: '1G',
    env: {
      NODE_ENV: 'production',
      PORT: 3000
    }
  }]
};
```

## 9. Set Up SSL

- Obtain an SSL certificate (use AWS Certificate Manager if using AWS)
- Configure your load balancer to use HTTPS

## 10. Configure Domain Name

- Register a domain name if you haven't already
- Set up DNS records to point to your load balancer

## 11. Environment Variables

Set up the following environment variables on your EC2 instances:

```
NODE_ENV=production
PORT=3000
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
TELEGRAM_BOT_TOKEN=your_telegram_bot_token
REDIS_URL=your_redis_url
CORS_ORIGIN=https://your-frontend-domain.com
```

## 12. Deployment Steps

1. SSH into your EC2 instance
2. Clone your repository
3. Install dependencies: `npm install --production`
4. Install PM2 globally: `npm install pm2 -g`
5. Start your application: `pm2 start ecosystem.config.js`
6. Save the PM2 process list: `pm2 save`
7. Set up PM2 to start on system boot: `pm2 startup systemd`

## 13. Monitoring and Logging

- Set up CloudWatch for monitoring EC2 instances and logs
- Configure Prometheus and Grafana for application-specific metrics
- Set up log rotation to manage log files

## 14. Backup Strategy

- Set up regular backups for your MongoDB database
- Use AWS Backup for EC2 instances and EBS volumes

## 15. Scaling Strategy

- Set up Auto Scaling groups for EC2 instances
- Configure scaling policies based on CPU utilization or custom metrics

## 16. Security Measures

- Enable AWS GuardDuty for threat detection
- Use AWS WAF (Web Application Firewall) to protect against common exploits
- Regularly update and patch your systems

## 17. Performance Optimization

- Set up Amazon CloudFront as a CDN
- Optimize your Node.js application (e.g., enable gzip compression)

## 18. Testing

- Perform load testing using tools like Apache JMeter
- Conduct security testing (e.g., penetration testing)

## 19. Documentation

- Update API documentation for the production endpoints
- Prepare runbooks for common operational tasks

## 20. Compliance

- Ensure your deployment meets necessary compliance standards (e.g., GDPR if applicable)

## 21. Rollback Plan

- Prepare a rollback strategy in case of critical issues post-deployment

## 22. Post-Deployment Verification

- Verify all API endpoints are working as expected in the production environment
- Check monitoring and logging systems are capturing data correctly

## 23. Frontend Integration

- Provide the production API base URL to the frontend team
- Assist in updating any environment-specific configurations in the frontend code

Remember to test thoroughly in a staging environment that mirrors your production setup before going live. Once deployed, monitor the application closely for any issues or performance bottlenecks.
