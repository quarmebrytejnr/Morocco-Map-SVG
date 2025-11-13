## IMPLEMENTATION GUIDE

### Prerequisites
- A free Mapbox account (sign up at https://account.mapbox.com/auth/signup/)
- Your Mapbox access token
- The Morocco Style JSON (provided separately)

### Step-by-Step Setup

#### Step 1: Get Your Mapbox Access Token

1. Sign up for a free Mapbox account at https://account.mapbox.com/auth/signup/
2. Once logged in, go to your Account page
3. Scroll to "Access tokens" section
4. Copy your default public token (starts with `pk.`)
5. **Free tier includes:** 50,000 map loads/month, 100,000 tile requests/month

#### Step 2: Upload the Morocco Style to Mapbox Studio

**Method A: Using Mapbox Studio (Easiest)**

1. Go to https://studio.mapbox.com/
2. Click "New style"
3. Choose "Blank" or "Streets" as a starting point
4. Click on "Style" in the top menu
5. Click the three dots (⋮) next to your style name
6. Select "Replace style"
7. Paste the Morocco Style JSON
8. Click "Replace"
9. Your style will now have a unique Style URL (looks like: `mapbox://styles/yourusername/xxxxx`)

**Method B: Direct Upload via API**

```bash
# Replace YOUR_USERNAME and YOUR_TOKEN
curl -X POST "https://api.mapbox.com/styles/v1/YOUR_USERNAME?access_token=YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d @morocco-style.json
```

#### Step 3: Implementation Examples

**Option A: Web Application (Mapbox GL JS)**

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Morocco Map</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src='https://api.mapbox.com/mapbox-gl-js/v3.0.0/mapbox-gl.js'></script>
    <link href='https://api.mapbox.com/mapbox-gl-js/v3.0.0/mapbox-gl.css' rel='stylesheet' />
    <style>
        body { margin: 0; padding: 0; }
        #map { position: absolute; top: 0; bottom: 0; width: 100%; }
    </style>
</head>
<body>
    <div id='map'></div>
    <script>
        mapboxgl.accessToken = 'YOUR_MAPBOX_TOKEN';
        
        const map = new mapboxgl.Map({
            container: 'map',
            // Use your uploaded style URL
            style: 'mapbox://styles/yourusername/cm355hgyd009601pdef76716x',
            center: [-7.0926, 31.7917], // Morocco center
            zoom: 5
        });
        
        // Add navigation controls
        map.addControl(new mapboxgl.NavigationControl());
    </script>
</body>
</html>
```

**Option B: Power BI with Mapbox Visual**

1. In Power BI Desktop, go to "Get Data" → "Web"
2. Enter the Mapbox Static Tiles API URL:
```
https://api.mapbox.com/styles/v1/yourusername/STYLE_ID/tiles/256/{z}/{x}/{y}?access_token=YOUR_TOKEN
```

3. Or use the Azure Maps visual with custom tile layers:
   - Add Azure Maps visual to your report
   - In visual settings, go to "Map Settings"
   - Enable "Custom Map Style"
   - Paste your Mapbox style URL

**Option C: Python with Plotly**
