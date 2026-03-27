# What We're Building Today

- Set up a React Native project from scratch with Expo
- Add a map with live geolocation
- Tap into device sensors (accelerometer, gyroscope)
- Understand how React Native works under the hood

---

# What is React Native?

- Build native mobile apps using JavaScript & React
- Not a webview — renders real native components
- One codebase for iOS and Android
- Huge ecosystem: same npm packages you already know

---

# What is Expo?

- A framework and platform built on top of React Native
- Handles the hard stuff: builds, native config, OTA updates
- No Xcode or Android Studio needed to get started
- `npx create-expo-app` and you're off

---

# Setting Up

```bash
# Install and create a new project
npx create-expo-app@latest MyApp
cd MyApp

# Start the dev server
npx expo start
```

- Scan the QR code with Expo Go on your phone
- Or press `i` for iOS simulator / `a` for Android emulator

---

# Hello World

```jsx
import { Text, View, StyleSheet } from "react-native";

export default function App() {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>Hello, CPOSC!</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: "center", alignItems: "center" },
  title: { fontSize: 32, fontWeight: "bold" },
});
```

---

# Hot Reloading

- Save a file and changes appear instantly on your device
- No recompilation, no restart
- Preserves component state while updating code

**DEMO: Change text, colors, layout — watch it update live**

---

# Adding a Map with Geolocation

```bash
npx expo install react-native-maps expo-location
```

```jsx
import MapView, { Marker } from "react-native-maps";
import * as Location from "expo-location";
```

- Request location permissions
- Get current coordinates
- Drop a marker on the map at your position

---

# Map Demo Code

```jsx
const [location, setLocation] = useState(null);

useEffect(() => {
  (async () => {
    let { status } = await Location.requestForegroundPermissionsAsync();
    if (status !== "granted") return;

    let loc = await Location.getCurrentPositionAsync({});
    setLocation(loc.coords);
  })();
}, []);

return (
  <MapView
    style={{ flex: 1 }}
    initialRegion={{
      latitude: location?.latitude ?? 40.2732,
      longitude: location?.longitude ?? -76.8867,
      latitudeDelta: 0.01,
      longitudeDelta: 0.01,
    }}
  >
    {location && <Marker coordinate={location} title="You are here" />}
  </MapView>
);
```

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

- Accelerometer, gyroscope, barometer, pedometer
- All accessible with a few lines of code

---

# How React Native Works

```
  JavaScript          Bridge / JSI         Native
 ┌───────────┐      ┌────────────┐      ┌──────────┐
 │ Your React │ ──► │  Hermes +   │ ──► │ UIKit /   │
 │ Components │ ◄── │  Fabric     │ ◄── │ Android   │
 └───────────┘      └────────────┘      └──────────┘
```

- **Hermes**: Optimized JS engine for React Native
- **Fabric**: New rendering system — synchronous, concurrent
- **JSI**: Direct JS-to-native calls, no more JSON bridge bottleneck

---

# Key Takeaways

- React Native + Expo = fastest path from zero to mobile app
- Write JavaScript, get real native performance
- Access device APIs (GPS, sensors, camera) with minimal code
- Hot reload makes the dev experience feel instant
- One codebase, multiple platforms
