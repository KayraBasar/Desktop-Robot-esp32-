# 🎵 Spotify → ESP32 Bridge (Flask Server) for desk buddy

---


A lightweight, multi-threaded Python Flask bridge server designed to fetch your real-time Spotify playback details and serve them as a compact JSON endpoint for IoT devices like **ESP32**. 

Optimized for open-frame cyberpunk desktop robots and smart displays, this script handles Spotify authentication, token refreshing, and background data fetching smoothly without blocking the main web server.

### 🚀 Features
* **Multi-threaded Architecture:** A background daemon thread fetches Spotify data every 3 seconds, ensuring the ESP32 receives instant, non-blocking HTTP responses.
* **Compact JSON Output:** Optimized endpoint structure providing `track`, `artist`, `album`, `progress`, `duration`, and `is_playing` states.
* **Persistent Authentication:** Automatically caches your OAuth credentials locally after the first browser confirmation.

### 🛠️ Prerequisites
* **Spotify Premium Account** (Required for Spotify Web API playback telemetry).
* Python 3.7+ installed.
* Dependencies: `flask`, `spotipy`, `requests`.

### ⚙️ Setup & Installation

#### 1. Spotify Developer Console Setup
1. Navigate to the [Spotify Developer Dashboard](https://developer.spotify.com/dashboard).
2. Click **Create an App**.
3. In the app settings, add the exact following URL to the **Redirect URIs** field:
   `http://127.0.0.1:8888/callback`
   *(Note: Use `127.0.0.1` instead of `localhost` to comply with Spotify's local security protocols).*

#### 2. Local Environment Setup
Clone the repository or download the script, then install the required libraries:
`
pip install flask spotipy
pip install --upgrade pip `


#### 3. Configuration
Open spotify_bridge.py and replace the placeholder credentials with your actual developer keys:
`CLIENT_ID     = "YOUR_SPOTIFY_CLIENT_ID_HERE"
CLIENT_SECRET = "YOUR_SPOTIFY_CLIENT_SECRET_HERE"`
####⚠️ Warning: Keep your Client Secret private. Never commit your raw API keys directly to public GitHub repositories!

💻 Running the Server
Execute the script using your terminal:
`python spotify_bridge.py`
First Run: A browser window will automatically pop up asking you to grant permissions.
Log in with your premium Spotify account and confirm. 
A hidden .spotify_cache file will be generated locally so you don't have to authenticate again.

🔌 API Endpoints
Once running, the bridge serves data locally at http://0.0.0.0:5000. Your ESP32 can poll the following endpoints:

GET /now-playing — Main data feed for the ESP32. Returns a compact JSON payload:
`{
  "album": "Album Name",
  "artist": "Artist Name",
  "duration": 210000,
  "is_playing": true,
  "progress": 45000,
  "track": "Track Title",
  "track_id": "4PTG3Z6ehGkBF2zI7Y9G7g"
}`
GET /health — 
Quick diagnostics check to ensure the server and bridge system are fully operational.


