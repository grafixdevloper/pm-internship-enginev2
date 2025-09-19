# PM Internship Recommender - Setup Guide

## Quick Start

### Prerequisites
- Python 3.7 or higher
- Modern web browser (Chrome, Firefox, Safari, Edge)

### Installation Steps

1. **Navigate to the project directory**
   ```bash
   cd pm-internship-recommender
   ```

2. **Install Python dependencies**
   ```bash
   cd backend
   pip install -r requirements.txt
   ```

3. **Start the backend server**
   ```bash
   python app.py
   ```
   The API server will start at `http://localhost:5000`

4. **Open the frontend**
   - Navigate to the `frontend` directory
   - Open `index.html` in your web browser
   - Or use a simple HTTP server:
     ```bash
     # If you have Python installed
     cd frontend
     python -m http.server 8000
     ```
     Then visit `http://localhost:8000`

## Project Structure

```
pm-internship-recommender/
├── backend/                 # Flask API server
│   ├── app.py              # Main Flask application
│   ├── recommendation_engine.py  # Core recommendation logic
│   └── requirements.txt    # Python dependencies
├── frontend/               # Web interface
│   ├── index.html         # Main HTML page
│   ├── styles.css         # CSS styles (mobile-first)
│   └── script.js          # JavaScript functionality
├── data/                  # Data files and schemas
│   ├── candidate_schema.json     # Candidate profile schema
│   ├── internship_schema.json    # Internship data schema
│   └── sample_internships.json   # Sample internship data
├── static/               # Static assets (images, icons)
├── docs/                # Documentation
└── README.md           # Project overview
```

## Features

### For Candidates
- **Simple Form Interface**: Easy-to-use form with visual icons and clear labels
- **Mobile-First Design**: Optimized for smartphones and tablets
- **Intelligent Matching**: AI-powered recommendations based on skills, interests, and location
- **Clear Results**: Easy-to-understand internship cards with match explanations
- **Accessibility**: Keyboard navigation and screen reader support

### For Administrators
- **RESTful API**: Clean API endpoints for integration
- **Extensible Data**: JSON-based internship and candidate data
- **Configurable Algorithm**: Rule-based matching with adjustable weights
- **Multiple Data Sources**: Support for various data formats

## API Endpoints

### GET /
Health check endpoint

### POST /api/recommend
Get personalized recommendations
```json
{
  "education": "12th",
  "skills": ["computer", "communication"],
  "interests": ["technology", "education"],
  "location": "bangalore"
}
```

### GET /api/internships
Get all available internships

### GET /api/sectors
Get all available sectors

## Customization

### Adding New Internships
1. Edit `data/sample_internships.json`
2. Follow the schema defined in `data/internship_schema.json`
3. Restart the backend server

### Modifying the Algorithm
1. Edit `backend/recommendation_engine.py`
2. Adjust weights in the `calculate_match_score` method
3. Add new matching criteria as needed

### UI Customization
1. Modify `frontend/styles.css` for visual changes
2. Update `frontend/index.html` for structure changes
3. Edit `frontend/script.js` for functionality changes

## Deployment

### Local Development
Follow the installation steps above.

### Production Deployment
1. **Backend**: Deploy Flask app using Gunicorn, uWSGI, or similar
2. **Frontend**: Serve static files using Nginx, Apache, or CDN
3. **Database**: Replace JSON files with proper database (PostgreSQL, MongoDB)
4. **Security**: Add authentication, rate limiting, and HTTPS

### Integration with Existing Portal
The system is designed to be easily integrated:
- Use the API endpoints from existing applications
- Embed the frontend interface in iframes
- Customize the UI to match existing design systems

## Troubleshooting

### Backend Issues
- **Port 5000 in use**: Change port in `app.py`
- **Module not found**: Install dependencies with `pip install -r requirements.txt`
- **Data not loading**: Check file paths in `recommendation_engine.py`

### Frontend Issues
- **API not connecting**: Ensure backend is running on port 5000
- **CORS errors**: Flask-CORS is included to handle cross-origin requests
- **Mobile display issues**: Test on actual devices or use browser dev tools

### Performance Optimization
- **Large datasets**: Implement database storage and indexing
- **Slow recommendations**: Add caching layer (Redis)
- **High traffic**: Use load balancers and multiple server instances

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make changes following the existing code style
4. Test thoroughly on mobile devices
5. Submit a pull request

## License

MIT License - see LICENSE file for details.