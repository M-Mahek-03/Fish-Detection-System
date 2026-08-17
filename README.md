# 🐟 Fish Detection & Recommendation System

<div align="center">

![Fish Detection System](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Flask](https://img.shields.io/badge/Flask-3.0+-green.svg)
![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Status](https://img.shields.io/badge/status-active-success.svg)

**An intelligent fish detection and recommendation system with location-based features and navigation routing for fishermen.**

[Features](#-features) • [Installation](#-installation) • [Usage](#-usage) • [API Documentation](#-api-documentation) • [Contributing](#-contributing)

</div>

---

## 📋 Overview

The Fish Detection & Recommendation System is a comprehensive web-based platform designed to assist fishermen and marine enthusiasts in identifying fish species, getting location-based recommendations, and planning optimal water routes. The system combines geospatial analysis, real-time data processing, and an intuitive interface to provide actionable insights.

### 🎯 Key Highlights

- **Smart Fish Recommendations** - Get fish species suggestions based on your location and season
- **Distance-Based Search** - Find fish species nearest to your coordinates
- **Water Route Planning** - Navigate safely through water bodies avoiding hazards
- **Interactive Dashboard** - Visualize fishing data and trends
- **Fish Encyclopedia** - Comprehensive database with images and details
- **Cost Tracking** - Monitor fishing-related expenses

---

## ✨ Features

### 🔍 Fish Detection & Identification
- Real-time fish species identification
- Comprehensive fish database with 25+ species
- High-quality images for each species
- Detailed information on habitat and characteristics

### 📍 Location-Based Services
- GPS coordinate-based recommendations
- Haversine distance calculation for accuracy
- Season-specific fish availability
- Regional fishing patterns analysis

### 🗺️ Navigation System
- Water route optimization using NetworkX
- Hazard zone avoidance (circular and polygonal)
- OpenCage geocoding integration
- Interactive map visualization with Folium

### 📊 Analytics & Insights
- Fishing cost hub for expense tracking
- Dashboard with data visualizations
- Community features for sharing catches
- Historical data analysis

---

## 🛠️ Technology Stack

### Backend
- **Python 3.8+** - Core programming language
- **Flask 3.0+** - Web framework
- **Flask-CORS** - Cross-origin resource sharing

### Geospatial Libraries
- **GeoPandas** - Geographic data manipulation
- **NetworkX** - Graph-based route optimization
- **Shapely** - Geometric operations
- **Folium** - Interactive map creation
- **Geopy** - Geocoding and distance calculations

### Data & APIs
- **OpenCage Geocoder** - Location services
- **GeoDatasets** - Natural earth data
- **JSON** - Data storage and exchange

---

## 🚀 Installation

### Prerequisites

- Python 3.8 or higher
- pip package manager
- Virtual environment (recommended)

### Step 1: Clone the Repository

```bash
git clone https://github.com/M-Mahek-03/Fish-Detection-System.git
cd Fish-Detection-System
```

### Step 2: Create Virtual Environment

```bash
# Create virtual environment
python3 -m venv venv

# Activate virtual environment
# On macOS/Linux:
source venv/bin/activate
# On Windows:
venv\Scripts\activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Configure Environment Variables

Create a `.env` file in the root directory:

```env
OPENCAGE_API_KEY=your_opencage_api_key_here
FLASK_ENV=development
FLASK_DEBUG=True
```

### Step 5: Run the Application

#### Main Fish Recommendation System
```bash
python3 app.py
```
Access at: `http://localhost:5000`

#### Navigation & Route Planning System
```bash
python3 backend.py
```
Access at: `http://localhost:5000`

---

## 💻 Usage

### Fish Recommendation by Location

```bash
# Manual location and season
curl "http://localhost:5000/recommend?location=Kerala&season=Monsoon"

# Coordinate-based search
curl "http://localhost:5000/recommend?lat=9.9&lon=76.2"

# With season filter
curl "http://localhost:5000/recommend?lat=9.9&lon=76.2&season=Monsoon"
```

### Route Planning

```bash
# Get optimal water route
curl "http://localhost:5000/route?start=Mumbai&end=Goa"

# With straight line optimization
curl "http://localhost:5000/route?start=Mumbai&end=Goa&straight=true"

# Using coordinates
curl "http://localhost:5000/route?start=72.8,18.9&end=73.8,15.5"
```

### Hazard Management

```bash
# Add circular hazard zone
curl -X POST http://localhost:5000/hazards \
  -H "Content-Type: application/json" \
  -d '{"mode":"circle","type":"Storm","center":[73.0,19.0],"radius_km":50}'

# Clear all hazards
curl -X DELETE http://localhost:5000/hazards
```

---

## 📚 API Documentation

### Endpoints

#### `GET /recommend`
Get fish recommendations based on location or coordinates.

**Parameters:**
- `location` (string, optional) - Location name (e.g., "Kerala")
- `season` (string, optional) - Season name (e.g., "Monsoon")
- `lat` (float, optional) - Latitude coordinate
- `lon` (float, optional) - Longitude coordinate

**Response:**
```json
[
  {
    "species": "Kingfish",
    "location": "Kerala",
    "season": "Monsoon",
    "lat": 9.9312,
    "lon": 76.2673,
    "distance_km": 5.234
  }
]
```

#### `GET /route`
Calculate optimal water route between two points.

**Parameters:**
- `start` (string, required) - Starting location or coordinates
- `end` (string, required) - Ending location or coordinates
- `straight` (boolean, optional) - Enable path simplification

**Response:**
```json
{
  "map_html": "<html>...</html>",
  "start": "Mumbai",
  "end": "Goa",
  "waypoints": 127,
  "distance_km": 438.52,
  "hazards_active": 2
}
```

#### `GET /locations`
Get all fish species in the database.

**Response:**
```json
[
  {
    "species": "Barramundi",
    "location": "West Bengal",
    "season": "Summer",
    "lat": 22.5726,
    "lon": 88.3639
  }
]
```

---

## 🗂️ Project Structure

```
Fish-Detection-System/
│
├── app.py                      # Main Flask application
├── backend.py                  # Route planning backend
├── dataset.json                # Fish species database
├── requirements.txt            # Python dependencies
├── README.md                   # Documentation
│
├── Fish-Detection/             # Legacy detection module
│   ├── fishdetection.html
│   ├── fishdashboard.html
│   └── main.html
│
├── images/                     # Fish species images
│   ├── BarramundiI.png
│   ├── KingfishI.png
│   └── ...
│
├── public/                     # Public assets
│   ├── data/
│   │   ├── eez_india.geojson
│   │   └── pfz_sample.geojson
│   └── icons/
│
├── src/                        # Frontend source
│   ├── App.jsx
│   ├── main.jsx
│   └── styles.css
│
└── templates/                  # HTML templates
    ├── index.html
    ├── fishdetection.html
    ├── fishdashboard.html
    ├── fishencyclopedia.html
    ├── fishingscheme.html
    ├── water_route.html
    └── ...
```

---

## 🌊 Features in Detail

### 1. Fish Recommendation Engine

The recommendation system uses the **Haversine formula** to calculate great-circle distances between coordinates, providing accurate fish species recommendations based on proximity.

```python
def haversine_km(lat1, lon1, lat2, lon2):
    R = 6371.0  # Earth's radius in kilometers
    phi1 = math.radians(lat1)
    phi2 = math.radians(lat2)
    dphi = math.radians(lat2 - lat1)
    dlambda = math.radians(lon2 - lon1)
    
    a = math.sin(dphi/2.0)**2 + \
        math.cos(phi1) * math.cos(phi2) * math.sin(dlambda/2.0)**2
    
    return 2 * R * math.asin(math.sqrt(a))
```

### 2. Water Route Optimization

Routes are calculated using graph-based pathfinding with NetworkX, considering:
- Water body boundaries
- Hazard zones
- Distance optimization
- Adaptive grid resolution

### 3. Hazard Zone Detection

Supports two types of hazard zones:
- **Circular zones** - Defined by center point and radius
- **Polygonal zones** - Defined by boundary vertices

---

## 🎨 Screenshots

### Dashboard
*Real-time data visualization and analytics*

### Fish Encyclopedia
*Comprehensive species database with images*

### Route Planning
*Interactive water navigation system*

---

## 🤝 Contributing

We welcome contributions! Here's how you can help:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/AmazingFeature`)
3. **Commit** your changes (`git commit -m 'Add some AmazingFeature'`)
4. **Push** to the branch (`git push origin feature/AmazingFeature`)
5. **Open** a Pull Request

### Development Guidelines

- Follow PEP 8 style guide for Python code
- Write descriptive commit messages
- Add tests for new features
- Update documentation as needed

---

## 🐛 Known Issues & Limitations

- Route calculation may be slow for long distances
- Requires active internet connection for geocoding
- Limited to Indian fish species currently
- OpenCage API has rate limits on free tier

---

## 🔮 Future Enhancements

- [ ] Machine learning-based fish species identification from images
- [ ] Real-time weather integration
- [ ] Mobile application (iOS/Android)
- [ ] Multi-language support
- [ ] Offline mode with cached data
- [ ] Social features and community catches
- [ ] Advanced analytics and predictions
- [ ] Integration with fishing equipment marketplaces

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👥 Authors

**Mahek Mukadam** - [@M-Mahek-03](https://github.com/M-Mahek-03)

---

## 🙏 Acknowledgments

- OpenCage for geocoding services
- Natural Earth for geographic data
- Flask community for excellent documentation
- All contributors and testers

---

## 📞 Contact & Support

- **Email**: mnmukadam04@gmail.com
- **GitHub**: [@M-Mahek-03](https://github.com/M-Mahek-03)
- **Issues**: [Report a bug](https://github.com/M-Mahek-03/Fish-Detection-System/issues)

---

<div align="center">

**If you found this project helpful, please consider giving it a ⭐!**

Made with ❤️ for fishermen and marine enthusiasts

</div>
