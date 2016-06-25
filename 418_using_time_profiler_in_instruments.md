# 418 - Using Time Profiler in Instruments

> Profile early, profile often

## Why Profiling

- A better UX
- Longer Battery Life
- Smooth Scrolling / Responsive App

## Time Profiler Call tree

- Doesn't measure duration 
- Aggregates samples into usful summary
- Focuses on CPU usage (Doesn't capture everything)
- Columns:
    + Weight: Represents the percentage of samples for particular portiion
    + Time: Number of samples mutliplied by time between each sample
    + Self Time: Amount of time spent in the method itself (not calling other methods)
- New in Xcode 8: Smart Disclosure (Hold option key, click triangle) unfolds directly to the interessing part

## Responsiveness

- Focus on main thread
- Thread strategy view can be helpful / gives a good overview

## Best Practices

- Profile always release builds (Optimizations, Real-World)
- Profile always on device
- Run with old devices
- Use large data sets where it makes sense
