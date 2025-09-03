# SpendAI Password Reset - Secure Deployment

This repository hosts the password reset page for the SpendAI mobile application with **secure credential management**.

## 🔒 Security Features

- **No hardcoded credentials** in source code
- **Build-time injection** of Supabase credentials from GitHub Secrets
- **Automatic validation** to ensure credentials are properly injected
- **Template-based approach** prevents accidental credential exposure

## 📁 Files

- `reset-password.template.html` - Template with placeholders for credentials
- `reset-password.html` - Generated file (created during deployment, not in source)
- `.github/workflows/deploy.yml` - GitHub Actions workflow for secure deployment

## 🚀 Setup Instructions

### 1. Add Repository Secrets

Go to **Settings** → **Secrets and variables** → **Actions** and add:

- `SUPABASE_URL` - Your Supabase project URL
- `SUPABASE_ANON_KEY` - Your Supabase anon public key

### 2. Enable GitHub Pages

- Go to **Settings** → **Pages**
- Source: **GitHub Actions** (not "Deploy from a branch")

### 3. Deployment Process

1. Push changes to `main` branch
2. GitHub Actions automatically:
   - Takes `reset-password.template.html`
   - Injects credentials from secrets
   - Creates `reset-password.html`
   - Deploys to GitHub Pages

## 🌐 Live URL

https://rdirisala.github.io/spendai-password-reset/reset-password.html

## 🔧 Development

For local testing, you can manually create the HTML file:
```bash
cp reset-password.template.html reset-password.html
sed -i "s|{{SUPABASE_URL}}|your-url-here|g" reset-password.html
sed -i "s|{{SUPABASE_ANON_KEY}}|your-key-here|g" reset-password.html
```

## 📋 Security Benefits

- **Source Code Clean**: No credentials visible in Git history
- **Secure Deployment**: Credentials only exist in deployed version
- **Failed Build Protection**: Build fails if credentials aren't properly injected
- **Secret Management**: Leverages GitHub's secure secret storage