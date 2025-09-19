# Vercel Deployment Guide

## 🚀 Deploy PM Internship Recommender to Vercel

### Prerequisites
1. **Install Git**: Download from https://git-scm.com/download/win
2. **Create GitHub account**: https://github.com/
3. **Create Vercel account**: https://vercel.com/ (sign up with GitHub)

### Step 1: Install Git
```powershell
# Download and install Git from: https://git-scm.com/download/win
# Or use Windows Package Manager:
winget install Git.Git
```

### Step 2: Initialize Git Repository
```powershell
# In your project directory
git init
git add .
git commit -m "Initial commit - PM Internship Recommender"
```

### Step 3: Create GitHub Repository
1. Go to https://github.com/new
2. Repository name: `pm-internship-recommender`
3. Description: `AI-powered internship recommendation system for PM Internship Scheme`
4. Set to Public
5. Click "Create repository"

### Step 4: Connect to GitHub
```powershell
# Replace YOUR_USERNAME with your GitHub username
git remote add origin https://github.com/YOUR_USERNAME/pm-internship-recommender.git
git branch -M main
git push -u origin main
```

### Step 5: Deploy to Vercel

#### Option A: Vercel Website (Recommended)
1. Go to https://vercel.com/
2. Sign in with GitHub
3. Click "New Project"
4. Import your `pm-internship-recommender` repository
5. Configure project:
   - **Framework Preset**: Other
   - **Root Directory**: `.` (leave as default)
   - **Build Command**: `cd backend && pip install -r requirements.txt`
   - **Output Directory**: `frontend`
6. Click "Deploy"

#### Option B: Vercel CLI
```powershell
# Install Vercel CLI
npm i -g vercel

# Login and deploy
vercel login
vercel

# Follow the prompts:
# - Link to existing project? N
# - Project name: pm-internship-recommender
# - Directory: ./ (current)
# - Want to override settings? Y
# - Build Command: cd backend && pip install -r requirements.txt
# - Output Directory: frontend
```

### Step 6: Your Live URLs
After deployment, you'll get:

**Main Application**: `https://pm-internship-recommender-YOUR_USERNAME.vercel.app/`

**API Endpoints**:
- Health Check: `https://pm-internship-recommender-YOUR_USERNAME.vercel.app/api/`
- Recommendations: `https://pm-internship-recommender-YOUR_USERNAME.vercel.app/api/recommend`
- All Internships: `https://pm-internship-recommender-YOUR_USERNAME.vercel.app/api/internships`
- Sectors: `https://pm-internship-recommender-YOUR_USERNAME.vercel.app/api/sectors`

### Step 7: Update Frontend API URL
After deployment, update the API URL in `frontend/script.js`:

```javascript
// Change this line:
const API_BASE_URL = 'http://localhost:5000/api';

// To this (replace with your actual Vercel URL):
const API_BASE_URL = 'https://pm-internship-recommender-YOUR_USERNAME.vercel.app/api';
```

Then commit and push the change:
```powershell
git add frontend/script.js
git commit -m "Update API URL for production"
git push
```

### Environment Variables (if needed)
If you add environment variables later:
1. Go to your Vercel project dashboard
2. Settings → Environment Variables
3. Add variables like `FLASK_ENV=production`

### Troubleshooting

**Issue**: Build fails
**Solution**: Make sure `backend/requirements.txt` exists and is valid

**Issue**: API endpoints not working
**Solution**: Check that `vercel.json` is in the root directory

**Issue**: CORS errors
**Solution**: Flask-CORS is already configured in `backend/app.py`

**Issue**: Frontend not loading
**Solution**: Ensure `frontend/index.html` exists and references are correct

### Updating Your Deployed App
```powershell
# Make changes, then:
git add .
git commit -m "Your change description"
git push

# Vercel automatically redeploys on push to main branch
```

### Quick Commands Reference
```powershell
# Check Git status
git status

# Add all changes
git add .

# Commit changes
git commit -m "Description of changes"

# Push to GitHub (triggers Vercel deployment)
git push

# View deployment logs
vercel logs
```

Your app will be live at: `https://pm-internship-recommender-YOUR_USERNAME.vercel.app/`