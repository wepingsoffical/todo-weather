# India Weather & Travel Companion — Wireframe & Roadmap

## Screen-by-Screen Wireframe

### 1. Home (Weather) — ✅ Phase 1 (built in this drop)
- App bar: "India Weather & Travel"
- Location badge (shows "Approximate" when using IP fallback, per UX rule)
- Big temperature, condition text, wind speed
- Rain/thunderstorm alert banner (color-coded)
- Pull-to-refresh

### 2. Radar — Phase 3
- Full-screen `flutter_map` with OpenStreetMap tiles
- RainViewer color overlay
- Tap/long-press on map → plays rain/thunder sound for that point's color band
- Push notification trigger for severe cells near user

### 3. Route Planner — Phase 4
- Two text fields: "From" / "To" (Nominatim autocomplete)
- "Plan Route" button → OSRM route + waypoint weather strip
- Map with polyline, color-coded by weather severity at each waypoint
- Advisory text banner (e.g. "Rain at Villupuram — delay 45 min")

### 4. Districts (Explore India) — Phase 2
- State list → District grid (from local JSON)
- District detail: live weather (Open-Meteo) + Wikipedia summary card + RSS news card

### 5. Timeline (My Travels) — Phase 5
- Map with red polyline of tracked route
- Below: chronological stop log (time, place, weather at that time)
- Export button (PDF/GPX — future "more options" item)

### 6. Settings — Phase 6 & 7
- Language picker (23 languages, easy_localization)
- Theme (Light/Dark/AMOLED)
- Backup Now / Restore button (Google Drive, AES-256)
- Auto-backup toggle (nightly, Wi-Fi + charging only)

---

## Phase Plan & Status

| Phase | Scope | Status |
|---|---|---|
| 1 | Location Engine (GPS+IP) + Weather Home screen | ✅ Code in this drop |
| 2 | District Selector + Wikipedia integration | Next |
| 3 | Rain Radar + Sound Alerts | Planned |
| 4 | Route Weather Planner (OSRM) | Planned |
| 5 | Travel Timeline (foreground tracking first) | Planned |
| 6 | 23-language localization | Planned |
| 7 | Google Drive Backup + AES-256 encryption | Planned |

## Phase 1 — What's included in this code drop
- `lib/core/services/location_service.dart` — GPS primary, ip-api.com fallback (swap for GeoLite2 before production), 5s GPS timeout, always resolves (never blocks UI).
- `lib/core/network/open_meteo_client.dart` — dedicated Open-Meteo client class.
- `lib/features/weather/domain/weather.dart` — weather model + alert-level logic (rain/thunderstorm codes from the sound-alert plan).
- `lib/features/weather/data/weather_repository.dart` — combines location + weather into one snapshot.
- `lib/features/weather/presentation/home_screen.dart` — UI with approximate-location badge and alert banner.
- `lib/main.dart` — app entry point.

## Next steps to run this
1. `flutter pub get`
2. Add Android/iOS location permissions (`ACCESS_FINE_LOCATION`, `NSLocationWhenInUseUsageDescription`).
3. `flutter run`
