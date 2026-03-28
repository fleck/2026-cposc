# Saving & Loading Pins with API Routes

Expo Router supports server-side API routes with the `+api.ts` convention

```
app/api/pins+api.ts   →   /api/pins
```

**POST** `/api/pins` — save a pin with coordinates and note

**GET** `/api/pins` — load all saved pins from every user

Add a **Save** button to persist your pin to the server

Add a **Refresh** button to fetch the latest pins and comments from everyone
