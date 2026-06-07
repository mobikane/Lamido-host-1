# 🚀 Lamido Host - Automated Website Deployment Agent

**Lamido Host** is an intelligent, self-healing deployment agent that automates website hosting with minimal intervention. Push your website files to GitHub, and the agent handles building, deploying, and maintaining your sites across multiple hosting platforms.

## ✨ Features

- **🤖 Fully Automated Deployment**: Push files → Automatic build & deploy
- **🏥 Self-Healing**: Auto-recovery on deployment failures
- **👀 Continuous Monitoring**: Real-time health checks with auto-recovery
- **🌍 Multi-Platform Support**: 
  - GitHub Pages (Static)
  - Vercel (Node.js, Static)
  - Netlify (Dynamic, Static)
  - AWS EC2/S3 (Bring your own)
  - Self-hosted servers
- **🔄 Smart Change Detection**: Only deploy when files change
- **📊 Advanced Intervention Options**: Manual controls for advanced users
- **📝 Easy Configuration**: YAML-based setup

## 🎯 Quick Start

### 1. **Setup**

Clone or fork this repository:
```bash
git clone https://github.com/mobikane/Lamido-host-1.git
cd Lamido-host-1
```

### 2. **Configure Your Hosting Platform**

Edit `config/platforms.yml`:
```yaml
platforms:
  github_pages:
    enabled: true
    type: static
    
  vercel:
    enabled: false
    token: ${{ secrets.VERCEL_TOKEN }}
    
  netlify:
    enabled: false
    token: ${{ secrets.NETLIFY_TOKEN }}
    
  aws:
    enabled: false
    access_key: ${{ secrets.AWS_ACCESS_KEY }}
    secret_key: ${{ secrets.AWS_SECRET_KEY }}
    
  self_hosted:
    enabled: false
    ssh_host: your-server.com
    ssh_user: deploy-user
    ssh_key: ${{ secrets.SSH_PRIVATE_KEY }}
```

### 3. **Add Your Website**

Create a directory in `/websites`:
```
websites/
  ├── my-portfolio/
  │   ├── index.html
  │   ├── styles.css
  │   ├── script.js
  │   └── .lamido-config.yml
  └── blog/
      ├── package.json
      ├── src/
      └── .lamido-config.yml
```

### 4. **Configure Each Website**

Create `.lamido-config.yml` in each website directory:
```yaml
site:
  name: my-portfolio
  type: static  # or 'node', 'python', 'static'
  
build:
  enabled: true
  command: npm run build  # Leave empty for static sites
  output_dir: dist

deploy:
  platform: github_pages  # or vercel, netlify, aws, self_hosted
  branch: gh-pages
  
health_check:
  enabled: true
  interval: 300  # seconds (5 minutes)
  endpoints:
    - https://my-portfolio.github.io
    - https://my-portfolio.github.io/about
  timeout: 10
  
auto_recovery:
  enabled: true
  retry_count: 3
  retry_delay: 60  # seconds
```

### 5. **Push & Deploy**

```bash
git add .
git commit -m "Add my-portfolio website"
git push origin main
```

The agent automatically:
- ✅ Detects changes
- ✅ Builds your site (if needed)
- ✅ Deploys to your platform
- ✅ Runs health checks
- ✅ Recovers on failure

## 📋 Directory Structure

```
Lamido-host-1/
├── .github/
│   └── workflows/
│       ├── deploy.yml              # Main deployment workflow
│       ├── health-check.yml        # Continuous health monitoring
│       ├── auto-recovery.yml       # Auto-recovery on failures
│       └── manual-intervention.yml # Advanced manual controls
├── config/
│   ├── platforms.yml               # Hosting platform configuration
│   ├── sites.yml                   # Website configurations
│   └── health-checks.yml           # Health check rules
├── scripts/
│   ├── deploy.sh                   # Deployment orchestrator
│   ├── health-check.sh             # Health check logic
│   ├── recovery.sh                 # Auto-recovery logic
│   └── detect-changes.sh           # Change detection
├── websites/
│   ├── example-static/             # Example static website
│   └── example-node/               # Example Node.js website
├── docs/
│   ├── platforms-setup.md          # Platform setup guide
│   ├── website-config.md           # Website configuration
│   ├── health-checks.md            # Health checks
│   ├── auto-recovery.md            # Recovery system
│   └── troubleshooting.md          # Troubleshooting
├── .github-secrets-template.md     # GitHub secrets setup guide
└── README.md                       # This file
```

## 🔑 GitHub Secrets Setup

Add these secrets to your repository settings (Settings → Secrets and variables → Actions):

```
VERCEL_TOKEN=your_vercel_token
NETLIFY_TOKEN=your_netlify_token
AWS_ACCESS_KEY=your_aws_key
AWS_SECRET_KEY=your_aws_secret
SSH_PRIVATE_KEY=your_ssh_private_key
GITHUB_TOKEN=your_github_token
```

## 🚨 Advanced Features

### Manual Intervention
Dispatch workflows manually via GitHub Actions tab:
- `manual-deploy` - Force deploy a specific site
- `manual-health-check` - Run health checks on demand
- `manual-recovery` - Trigger recovery for a site

### Custom Hooks
Add pre/post deployment scripts in `.lamido-config.yml`:
```yaml
hooks:
  pre_build: ./scripts/pre-build.sh
  post_deploy: ./scripts/post-deploy.sh
```

### Monitoring Dashboard
View deployment status, health checks, and recovery logs in the Actions tab.

## 📖 Documentation

- [Platform Setup Guide](docs/platforms-setup.md)
- [Website Configuration](docs/website-config.md)
- [Health Checks & Monitoring](docs/health-checks.md)
- [Auto-Recovery System](docs/auto-recovery.md)
- [Troubleshooting](docs/troubleshooting.md)

## 🤝 Contributing

To add a new website:
1. Create a directory in `/websites`
2. Add your files and `.lamido-config.yml`
3. Push to main
4. Agent handles the rest!

## 🆘 Support

Having issues? Check:
- [GitHub Actions Logs](../../actions)
- [Troubleshooting Guide](docs/troubleshooting.md)

## 📄 License

MIT License - See LICENSE file

---

**Made with ❤️ for Muhammad Lamido Abubakar**