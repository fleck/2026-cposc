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
