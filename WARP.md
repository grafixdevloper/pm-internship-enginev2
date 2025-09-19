# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Development Commands

### Backend (Flask API)
```bash
# Install dependencies
cd backend
pip install -r requirements.txt

# Run development server
python app.py

# Run on custom port
python app.py --port 8000
```

### Frontend (Static Web App)
```bash
# Serve frontend locally
cd frontend
python -m http.server 8000

# Or on Windows PowerShell
cd frontend
python -m http.server 8000
```

### Testing API Endpoints
```bash
# Test health check
curl http://localhost:5000/

# Test recommendations (POST with JSON)
curl -X POST http://localhost:5000/api/recommend -H "Content-Type: application/json" -d '{
  "education": "12th",
  "skills": ["computer", "communication"],
  "interests": ["technology", "education"],
  "location": "bangalore"
}'

# Get all internships
curl http://localhost:5000/api/internships

# Get available sectors
curl http://localhost:5000/api/sectors
```

## Architecture Overview

### Technology Stack
- **Backend**: Python 3.7+ with Flask framework
- **Frontend**: Vanilla HTML5, CSS3, JavaScript (no frameworks)
- **Data Storage**: JSON files (development) - designed for easy migration to databases
- **API**: RESTful endpoints with JSON responses

### Core Components

#### Backend (`backend/`)
- `app.py`: Flask application with REST API endpoints
- `recommendation_engine.py`: Rule-based recommendation algorithm with weighted scoring
- `requirements.txt`: Python dependencies (Flask, Flask-CORS, python-dotenv)

#### Frontend (`frontend/`)
- `index.html`: Single-page mobile-first interface
- `script.js`: Vanilla JavaScript with API integration and fallback mock data
- `styles.css`: Mobile-responsive CSS with accessibility features

#### Data Layer (`data/`)
- `sample_internships.json`: Internship database with rich metadata
- `candidate_schema.json`: User profile structure
- `internship_schema.json`: Internship data structure

### Recommendation Algorithm
The system uses a weighted scoring approach:
- **Skills Matching (40%)**: Fuzzy matching between candidate skills and job requirements
- **Sector/Interest Matching (30%)**: Alignment between user interests and internship sectors
- **Location Matching (20%)**: Geographic proximity with remote work bonus
- **Education Matching (10%)**: Education level compatibility

Key features:
- Returns top 5 matches with explanatory reasons
- Handles edge cases (missing data, no matches)
- Supports remote work preferences
- Regional location grouping for better matching

## Project-Specific Context

### Target Audience
This application serves **first-generation learners** and **rural youth** applying for PM Internship Scheme with:
- Limited digital exposure
- Mobile-first usage patterns
- Low bandwidth connections
- Multilingual needs (future scope)

### Design Principles
- **Simplicity First**: Minimal cognitive load for users with limited digital literacy
- **Mobile Responsive**: Optimized for smartphone usage
- **Visual Cues**: Icons and colors guide user actions
- **Fast Loading**: Lightweight assets for low-bandwidth environments
- **Progressive Enhancement**: Works without JavaScript as fallback

### Data Model Key Points
Each internship record includes:
- `accessibility` field for rural-friendly, low-bandwidth, and flexible hour indicators
- `language_requirements` for regional language support
- `is_remote` boolean for location flexibility
- Rich metadata for better matching (company size, benefits, skills offered)

### API Error Handling
- Frontend gracefully falls back to mock data if backend unavailable
- All API responses include `success` boolean and error messages
- CORS enabled for frontend-backend communication

### File Structure Patterns
- Configuration files in root directory
- Static assets intended for `static/` directory (currently empty)
- Documentation in `docs/` directory
- Clear separation of concerns (backend/frontend/data)

## Development Notes

### Adding New Internships
1. Edit `data/sample_internships.json` following the schema in `data/internship_schema.json`
2. Ensure `accessibility` fields are properly filled for rural/remote users
3. Include appropriate `language_requirements` for regional support
4. Restart Flask server to reload data

### Modifying Recommendation Logic
Key methods in `recommendation_engine.py`:
- `calculate_match_score()`: Main scoring logic with weights
- `calculate_skills_match()`: Fuzzy string matching for skills
- `calculate_location_match()`: Geographic and remote work logic
- `is_same_region()`: Regional clustering (simplified implementation)

### Frontend Customization
- Form validation in `validateFormData()` function
- Mock data fallback in `getMockRecommendations()` for offline development
- Recommendation card HTML template in `createRecommendationCard()`

### Mobile Testing
Always test on actual mobile devices or browser dev tools mobile simulation:
- Touch-friendly form elements
- Readable text sizes
- Fast loading on slow connections
- Offline functionality with mock data