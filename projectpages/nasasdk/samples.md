# Sample Scenes

The NASA APIs for Unity SDK includes several sample scenes to help you get started. These scenes demonstrate how to use different NASA APIs and integrate them into your Unity projects.

## Importing Samples

To import the sample scenes:

1. Open the Unity Package Manager (**Window > Package Manager**)
2. Select the **NASA APIs for Unity** package
3. In the package details, find the **Samples** section
4. Click the **Import** button next to each sample you want to use

## Sample Descriptions

### APOD Gallery

![APOD Gallery](../images/apod_gallery_preview.gif)

**Description**: Displays the Astronomy Picture of the Day with navigation controls to view previous days.

**Features**:
- Fetches and displays APOD images
- Navigation between different dates
- Displays title and explanation text
- Handles different media types (image/video)

**Key Scripts**:
- `ApodGalleryController.cs`: Main controller for the APOD gallery

**NASA APIs Used**:
- Astronomy Picture of the Day (APOD)

**How to Use**:
1. Import the sample
2. Open the `ApodGallery.unity` scene
3. Set your `NasaConfig` asset in the inspector
4. Press Play
5. Use the Next/Previous buttons to navigate between dates

### Mars Rover Explorer

![Mars Rover Explorer](../images/mars_rover_explorer_preview.gif)

**Description**: Simulates exploring Mars by fetching photos from NASA's Mars rovers.

**Features**:
- Fetches and displays Mars Rover photos
- Selects photos by rover, camera, and sol (Martian day)
- Displays photo metadata

**Key Scripts**:
- `MarsRoverController.cs`: Main controller for the Mars rover explorer

**NASA APIs Used**:
- Mars Rover Photos API

**How to Use**:
1. Import the sample
2. Open the `MarsRoverExplorer.unity` scene
3. Set your `NasaConfig` asset in the inspector
4. Press Play
5. Click the Capture button to fetch a photo for the current settings
6. Adjust the rover, sol, and camera settings as needed

### Real-Time Asteroid Radar

![Asteroid Radar](../images/asteroid_radar_preview.gif)

**Description**: Visualizes near-Earth asteroids based on NASA's NeoWs feed.

**Features**:
- Fetches current near-Earth objects (NEOs)
- Visualizes asteroids with scale based on their size
- Displays asteroid information on hover/selection
- Shows potentially hazardous asteroids

**Key Scripts**:
- `AsteroidRadarController.cs`: Main controller for the asteroid radar
- `AsteroidInfo.cs`: Component attached to asteroid GameObjects

**NASA APIs Used**:
- Near Earth Object Web Service (NeoWs)

**How to Use**:
1. Import the sample
2. Open the `RealTimeAsteroidRadar.unity` scene
3. Set your `NasaConfig` asset in the inspector
4. Press Play
5. Asteroids will be fetched and displayed automatically
6. Click on asteroids to view more information

### Earth Orbit Viewer

![Earth Orbit Viewer](../images/earth_orbit_viewer_preview.gif)

**Description**: Displays stunning EPIC (Earth Polychromatic Imaging Camera) images of Earth.

**Features**:
- Fetches EPIC images from DSCOVR satellite
- Applies images to a 3D Earth model
- Navigation between multiple images from the same day
- Displays image capture information

**Key Scripts**:
- `EarthOrbitController.cs`: Main controller for the Earth orbit viewer

**NASA APIs Used**:
- EPIC (Earth Polychromatic Imaging Camera)

**How to Use**:
1. Import the sample
2. Open the `EarthOrbitViewer.unity` scene
3. Set your `NasaConfig` asset in the inspector
4. Press Play
5. EPIC images will be fetched and the first one displayed on the Earth sphere
6. Use the Next/Previous buttons to cycle through available images

## Extending the Samples

These samples are designed to be starting points for your own projects. Here are some ideas for extending them:

### APOD Gallery
- Create a gallery view to display multiple days at once
- Save favorite images to a collection
- Share images to social media

### Mars Rover Explorer
- Create a VR experience where users can explore Mars
- Add a map interface to select locations
- Create a Mars terrain based on real topographical data

### Real-Time Asteroid Radar
- Add animations for asteroid orbits
- Create a game where players must defend Earth from asteroids
- Visualize asteroid approaches over time

### Earth Orbit Viewer
- Add cloud and atmosphere effects
- Create a time-lapse animation of Earth from EPIC images
- Add interactive markers for geographical features or events