# UberBags - Scavenger Hunt App

A real-time scavenger hunt app styled like the Uber driver app. Perfect for bachelor parties and city adventures!

## Features

- 🗺️ **Real-time GPS tracking** - Driver's location updates live
- 📍 **Dynamic destinations** - Organizer sends destinations on the fly
- 💬 **Hints system** - Add clues for each location
- 📱 **Mobile optimized** - Works great on phones
- 🚗 **Uber-style UI** - Familiar driver app interface
- 🔄 **Real-time sync** - Powered by Firebase

## Setup Instructions

### 1. Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Add project" and follow the steps
3. Once created, click "Web" (</> icon) to add a web app
4. Register your app (name it "UberBags")
5. Copy the Firebase configuration object

### 2. Create Firestore Database

1. In Firebase Console, go to "Firestore Database"
2. Click "Create database"
3. Start in **test mode** (we'll secure it later)
4. Choose a location close to your city
5. Once created, click "Start collection"
6. Collection ID: `game`
7. Document ID: `current`
8. Add these fields:
   - `currentDestination` (map/null) - leave as null
   - `driverLocation` (map/null) - leave as null
   - `lastUpdate` (string) - leave empty
   - `status` (string) - value: `"active"`
   - `queue` (array) - leave as empty array `[]`

### 3. Configure Your App

1. Open `index.html` in a text editor
2. Find this section (around line 170):
```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```
3. Replace with your Firebase config from step 1
4. Do the same in `organizer.html` (around line 217)

### 4. Deploy to GitHub Pages

1. Create a new GitHub repository
2. Upload `index.html` and `organizer.html`
3. Go to repository Settings → Pages
4. Source: Deploy from branch `main`
5. Save and wait a few minutes
6. Your app will be live at `https://yourusername.github.io/uberbags/`

### 5. Secure Your Firebase (Important!)

After testing, secure your Firestore with these rules:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /game/current {
      allow read: if true;
      allow write: if true;
    }
  }
}
```

For production, add authentication or restrict to specific domains in Firebase Console → Authentication → Settings.

## How to Use

### For the Driver:
1. Open `https://yourusername.github.io/uberbags/` on your phone
2. Allow location permissions
3. Wait for the first destination
4. Follow the map and hints!
5. Tap "Start Navigation" to open Google Maps

### For the Organizer:
1. Open `https://yourusername.github.io/uberbags/organizer.html`
2. See the driver's live location on the map
3. Click the map to select a destination OR enter an address
4. Add a hint (optional)
5. Tap "Send Destination"
6. Driver receives it instantly!

## Tips

- **Test first**: Try it out a day before the party
- **Bookmarks**: Save both URLs as home screen bookmarks
- **Battery**: Driver should have a charger - GPS drains battery
- **Network**: Works on any cellular/wifi connection
- **Privacy**: Only you and the driver have access (no one else knows the URL)

## Troubleshooting

**Driver not seeing destinations?**
- Check if location permissions are enabled
- Make sure Firebase config matches in both files
- Check browser console for errors

**Map not loading?**
- Check internet connection
- OpenStreetMap might be slow - refresh the page

**Location not updating?**
- Enable high-accuracy GPS on phone
- Works best outdoors with clear sky view

## Customization Ideas

- Change the color scheme in CSS
- Add sound effects when new destination arrives
- Track completed destinations
- Add a timer/scoring system
- Custom map markers (upload images)

## Cost

- **Firebase**: Free tier includes 50K reads/20K writes per day (more than enough)
- **GitHub Pages**: Free
- **Maps**: OpenStreetMap is free

Total cost: **$0** 🎉

## Privacy & Security

- URLs are private - only people with the link can access
- Firebase test mode is open - don't store sensitive data
- Driver's location is only visible to organizer
- No data is permanently stored

Have fun and drive safe! 🚗💨
