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
