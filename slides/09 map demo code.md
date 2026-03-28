# Map Demo Code

```jsx
const [pin, setPin] = useState(null);
const [note, setNote] = useState("");

function handleMapPress(e) {
  const { latitude, longitude } = e.nativeEvent.coordinate;
  setPin({ latitude, longitude, note: "" });
  setNote("");
}

return (
  <>
    <MapView
      style={{ flex: 1 }}
      initialRegion={{
        latitude: 20, longitude: 0,
        latitudeDelta: 80, longitudeDelta: 80,
      }}
      onPress={handleMapPress}
    >
      {pin && (
        <Marker
          coordinate={pin}
          title="My Favorite Destination"
          description={pin.note}
        />
      )}
    </MapView>

    {pin && (
      <View>
        <Text>What do you love about this place?</Text>
        <TextInput
          value={note}
          onChangeText={setNote}
          placeholder="Beautiful beaches, amazing food..."
          multiline
        />
      </View>
    )}
  </>
);
```
