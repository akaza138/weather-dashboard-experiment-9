# Experiment No. 9: Weather Dashboard with Current and Historical Data Visualization Using React and Chart.js

## Overview
This repository contains the complete implementation for **Experiment No. 9: Weather Dashboard with Current and Historical Data Visualization Using React and Chart.js** from the **22CS506 Full Stack Development Laboratory** curriculum.

> **Implementation Note:** In accordance with the course lab practical manual, the application implements a rich, interactive front-end client architecture utilizing HTML5, CSS3, Bootstrap 5, JavaScript (ES6+), Moment.js, FontAwesome, and **Chart.js** for 5-day temperature and humidity data visualization, integrating with the OpenWeatherMap REST API with local storage persistence.

---

## Aim
To develop a web application that fetches and displays current and 5-day weather forecast information for cities, using the OpenWeatherMap API, with search history saved in local storage, graphical trend representation using Chart.js, and dynamically updates the UI with weather data and icons.

---

## Algorithm
1. **Initialize Saved Search Data**:
   - Retrieve previously searched cities from browser `localStorage` (`savedSearchArray`), or initialize with default cities (`Columbus`, `Bend`, `Los Angeles`, `San Francisco`, `Savannah`, `New York`, `Nashville`).
2. **Set Date Elements Using Moment.js**:
   - Compute and display the current time and current date.
   - Format and project the subsequent 5 daily dates (`date_1` to `date_5`).
3. **Get User Input for City Search**:
   - Listen for form submission or click events on the search button.
   - Sanitize and pass the query city to `getCurrent()`.
4. **Fetch Current Weather Data**:
   - Query the OpenWeatherMap Current Weather API (`/data/2.5/weather?q={city}`).
   - Dynamically update the UI with the city name, current temperature, weather icon, description, humidity, and wind speed.
5. **Fetch 5-Day Weather Forecast & Historical Trend**:
   - Extract latitude and longitude coordinates from the current weather response.
   - Retrieve daily forecast metrics including temperatures, weather icons, conditions, and humidity for the next 5 days.
   - Display UV Index for current day conditions.
6. **Data Visualization with Chart.js**:
   - Plot a dual-axis interactive line chart visualizing 5-day forecasted temperatures (°F) alongside humidity trends (%).
7. **Manage Search History**:
   - Render recent search queries into the interactive dropdown history menu.
   - Attach click listeners to historical entries allowing quick reloading of previously searched cities.
8. **Persist Search History**:
   - Save updated query lists into `localStorage` under `savedSearchArray`.

---

## Project Structure
```text
weather-dashboard-experiment-9/
├── assets/
│   ├── css/
│   │   ├── reset.css           # Modern CSS reset
│   │   ├── style.css           # Clean minimal styling matching practical lab manual output
│   │   └── responsive.css      # Mobile, tablet, and desktop breakpoints
│   ├── js/
│   │   └── config.example.js   # OpenWeatherMap API key configuration template
│   └── script.js               # Core application logic, API fetching, & Chart.js
├── .gitignore                  # Git ignore rules (excludes keys, node_modules, OS files)
├── index.html                  # Main application dashboard entry point
├── Whether.html                # Practical lab manual entry point alias
└── README.md                   # Complete documentation, aim, algorithm, and instructions
```

---

## Required Tools & Dependencies
- **Modern Web Browser**: Google Chrome, Mozilla Firefox, Microsoft Edge, or Safari.
- **CDN Libraries**:
  - [Bootstrap 5.0.2](https://getbootstrap.com/) (Layout and responsive dropdowns)
  - [FontAwesome 5.8.1](https://fontawesome.com/) (Weather and UI icons)
  - [Moment.js 2.24.0](https://momentjs.com/) (Date and time formatting)
  - [Chart.js 4.x](https://www.chartjs.org/) (Data visualization and trends)
  - [jQuery 3.2.1](https://jquery.com/)
- **Optional Local Server**: Python (`http.server`), Node.js (`http-server` or `serve`), or VS Code Live Server.

---

## OpenWeatherMap API Setup Instructions
To enable live weather data:

1. Visit [OpenWeatherMap](https://openweathermap.org/) and create a free account.
2. Navigate to your [API Keys page](https://home.openweathermap.org/api_keys) and copy your generated key.
3. You can configure your key using either of the following methods:
   - **Method A (Interactive in UI)**: Click the **"Set API Key"** button on the banner in the dashboard and paste your key. It will be safely saved in your browser's `localStorage`.
   - **Method B (Local Configuration File)**:
     1. Copy `assets/js/config.example.js` to `assets/js/config.js`:
        ```bash
        cp assets/js/config.example.js assets/js/config.js
        ```
     2. Open `assets/js/config.js` and set your key:
        ```javascript
        const CONFIG = {
          OPENWEATHER_API_KEY: 'your_actual_api_key_here'
        };
        ```
     *(Note: `assets/js/config.js` is automatically excluded by `.gitignore` to prevent credential exposure).*

---

## Instructions to Run the Application

### Option 1: Direct Browser Launch
Simply double-click `index.html` or `Whether.html` to open it directly in any web browser.

### Option 2: Using Python HTTP Server
```bash
# Start a local static file server
python -m http.server 8000

# Open in browser
# http://localhost:8000/index.html
```

### Option 3: Using Node.js
```bash
npx serve .
# Or: npx http-server .
```

---

## Expected Output
- **Header**: Navigation bar containing the title and dropdown menu for search and history.
- **Current Conditions**: City name, real-time clock and date, large temperature readout, animated weather icon, condition description, humidity percentage, wind speed, and UV index.
- **5-Day Forecast Grid**: 5 individual cards displaying projected day names, high temperatures, weather icons, and humidity.
- **Data Visualization Chart**: Smooth dual-axis line graph powered by Chart.js displaying temperature curves and humidity percentages across the 5-day forecast.
- **Search History**: Persistent list of past searches that re-fetches city data upon click.

---

## Common Troubleshooting Steps
1. **API Key 401 Unauthorized**:
   - OpenWeatherMap keys typically take 10 to 30 minutes to activate after initial account creation.
   - The application automatically falls back to clean demonstration data so UI and charting functionality can still be evaluated without interruption.
2. **City Not Found (404)**:
   - Check the spelling of the city name in the search input box.
3. **CORS or Local File Restrictions**:
   - If icons or external fonts fail to load over `file://` protocol due to browser security settings, run a local development server using `python -m http.server 8000`.
