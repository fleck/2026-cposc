---
marp: true
theme: default
---

```
                        *
                       /|\
                      / | \
                     /  |  \
                    / ZERO  \
                   /   TO    \
                  / MOBILE APP\
                 /  IN 30 MIN! \
                '-------+-------'
                   |  REACT  |
                   | NATIVE  |
                   |    +    |
                   |  EXPO   |
                   |_________|
                   |  |   |  |
                   |  |   |  |
                  /|__|___|__|\
                 / /_________\ \
                '==============='
                   )  ) | (  (
                  (  (  |  )  )
                   ) )  |  ( (
                  (   ( | )   )
                   )   )|(   (
                    (  )|(  )
                     ) )|( (
                      ()|()
                       )|(
                        ~
```

## By Jonathan Fleckenstein

---

# Download Expo Go

While we get started, grab **Expo Go** on your phone:

**iPhone** - Search "Expo Go" in the App Store

**Android** - Search "Expo Go" in the Google Play Store

You'll use this to run the app we build today directly on your device!

---

# What We're Building Today

Set up a React Native project from scratch with Expo

Add a map with live geolocation

Tap into device sensors (accelerometer, gyroscope)

Understand how React Native works under the hood

---

# What is React Native?

Build native mobile apps using JavaScript & React

Not a webview — renders real native components

One codebase for iOS and Android

Huge ecosystem: same JavaScript you already know

---

# What is Expo?

A framework and platform built on top of React Native

Handles the hard stuff: builds, native config, OTA updates (bypass app store review for small changes), routing, web, api routes ane much more!

---

# Setting Up

```bash
# Create the project in the current directory (from an empty folder)
# default@sdk-54 pins Expo SDK 54 (latest without this uses SDK 55)
# --yes accepts all defaults
pnpm create expo-app@latest CPOSC --template default@sdk-54 --yes

# Install the maps library before starting the server
cd CPOSC
pnpm dlx expo install react-native-maps

# Enable API routes (default template uses "static")
sed -i '' 's/"output": "static"/"output": "server"/' app.json

# Start the dev server
pnpm start
```

Show expo-dev-qr for remote connections.

If nobody can connect run `pnpm run ios` and show simulator.

---

# Hello CPOSC

Let's make an edit to our home screen CPOSC/app/(tabs)/index.tsx and see what happens.

If you device doesn't update automatically press and hold with 3 fingers and tap reload.

---

# Hot Reloading

Save a file and changes appear instantly on your device

No recompilation, no restart

Preserves component state while updating code

---

# Map Demo Code

Add a tab to CPOSC/app/(tabs)/\_layout.tsx

```jsx
<Tabs.Screen
  name="map"
  options={{
    title: "Map",
    tabBarIcon: ({ color }) => (
      <IconSymbol size={28} name="map.fill" color={color} />
    ),
  }}
/>
```

add map (apply MAP stash)

---

# Saving & Loading Pins with API Routes

Expo Router supports server-side API routes with the `+api.ts` convention

```
app/api/pins+api.ts   →   /api/pins
```

**POST** `/api/pins` — save a pin with coordinates and note

**GET** `/api/pins` — load all saved pins from every user

Add a **Save** button to persist your pin to the server

Add a **Refresh** button to fetch the latest pins and comments from everyone

---

# Device Sensors

```bash
npx expo install expo-sensors
```

```jsx
import { Accelerometer } from "expo-sensors";

const [data, setData] = useState({ x: 0, y: 0, z: 0 });

useEffect(() => {
  const sub = Accelerometer.addListener(setData);
  Accelerometer.setUpdateInterval(100);
  return () => sub.remove();
}, []);
```

Accelerometer, gyroscope, barometer, pedometer — all accessible with a few lines of code

---

# How React Native Works

```
  JavaScript          Bridge / JSI         Native
 ┌───────────┐      ┌────────────┐      ┌──────────┐
 │ Your React │ ──► │  Hermes +   │ ──► │ UIKit /   │
 │ Components │ ◄── │  Fabric     │ ◄── │ Android   │
 └───────────┘      └────────────┘      └──────────┘
```

**Hermes** — Optimized JS engine for React Native

**Fabric** — New rendering system, synchronous and concurrent

**JSI** — Direct JS-to-native calls, no more JSON bridge bottleneck

---

# Key Takeaways

React Native + Expo = fastest path from zero to mobile app

Write JavaScript, get real native performance

Access device APIs (GPS, sensors, camera) with minimal code

Hot reload makes the dev experience feel instant

One codebase, multiple platforms
