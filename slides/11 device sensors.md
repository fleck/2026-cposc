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
