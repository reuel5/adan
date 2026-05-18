# adan

adanreuel

## Phone sensor as per GPS

This project can use a phone's GPS as the primary location sensor for collecting position-aware data. The GPS reading should be treated as the source of truth for latitude, longitude, altitude, speed, heading, accuracy, and timestamp when location data is required.

### Recommended sensor flow

1. Request location permission from the user before starting GPS collection.
2. Enable high-accuracy GPS mode when precise movement or route tracking is needed.
3. Capture each GPS sample with:
   - latitude and longitude
   - horizontal accuracy
   - altitude, when available
   - speed and heading, when available
   - timestamp
4. Ignore or flag samples where GPS accuracy is outside the acceptable range for the feature.
5. Fall back to network or fused location only when GPS is unavailable, and mark the sample source accordingly.

### Example GPS sample format

```json
{
  "source": "gps",
  "latitude": 14.5995,
  "longitude": 120.9842,
  "accuracy_meters": 8.5,
  "altitude_meters": 12.0,
  "speed_mps": 1.4,
  "heading_degrees": 87.0,
  "timestamp": "2026-05-18T00:00:00Z"
}
```

### Implementation notes

- Use GPS readings only after the device reports a valid fix.
- Store timestamps in UTC so samples from different devices can be compared consistently.
- Keep battery usage in mind by reducing the sampling rate when the user is stationary.
- Clearly disclose location collection to users and avoid collecting GPS data when it is not needed.
