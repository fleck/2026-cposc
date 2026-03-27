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
