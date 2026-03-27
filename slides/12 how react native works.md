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
