Trip planning today assumes you either walk, drive, or take transit — but it ignores a large middle option: people who own an electric scooter, e-bike, or bicycle and can cover several kilometers quickly under their own power.

The idea is a routing app that treats your personal micro-mobility vehicle as a first-class input. You tell it: "I have an electric scooter, I can ride up to 8 km comfortably." The planner then finds routes that mix your scooter leg with buses, metro, trains, and ferries — finding the fastest door-to-door trip rather than the one with the fewest transfers or least walking.

Examples of what this unlocks:
- Ride 3 km to a metro station that Google Maps ignores because it assumes a 20-minute walk, then take one direct train instead of two with a transfer.
- Skip a crowded bus leg by scooting a parallel route that's faster at that time of day.
- Park your scooter at a transit hub with secure parking and continue by rail.

**Key inputs the user provides once:**
- Vehicle type (kick scooter, e-scooter, e-bike, bicycle, rollerblades)
- Comfortable range per leg in km
- Speed estimate or just let the app default by vehicle type
- Whether the vehicle is foldable / can go on transit

**What makes this hard:**
- Real-time transit data + bike routing in a single graph search
- Scooter parking availability at stations
- Hills and terrain affecting realistic range
- Willingness to lock the bike at destination vs. bringing it on transit

**Existing apps and services:**

- **Citymapper** (Android/iOS) — closest to the idea. "Routing Powers" combines personal bike/scooter with public transit and supports personal cycling speed. Still doesn't expose range or vehicle type as explicit inputs. https://citymapper.com
- **Google Maps** (Android/iOS) — bike+transit mode exists but no per-user speed or range profile; treats everyone identically.
- **Moovit** (Android/iOS) — bike/walk + transit combos, AI routing. No owned-vehicle profile. https://moovit.com
- **Transit app** (Android/iOS) — scooter+metro in one trip, departure alarms. No owned-vehicle range/speed profile. https://transitapp.com
- **Trafi** (Android/iOS, limited cities) — most integrated: personal + shared scooters + public transit in one app. Coverage limited.
- **ATL RIDES** (Atlanta region only) — full multimodal including personal scooter/bike + transit, cost/calorie/carbon comparison. City-specific.
- **ScootRoute** (Android/iOS) — scooter/e-bike routing avoiding highways and hills, bike lanes. No transit integration.
- **Urban Rider** (Android/iOS) — 4 vehicle profiles (scooter, moped, motorcycle, bike) with speed selection (25/45 km/h). No transit integration. https://www.urbanrider.app
- **Naviki** (Android/iOS) — bicycle/e-bike routing, all terrain types. No transit integration. https://www.naviki.org
- **Komoot** (Android/iOS) — cycling routing with fitness/terrain profile. No transit integration.
- **Rome2rio** (Android/iOS) — long-distance multimodal (train+flight+ferry). No personal micro-mobility.
- **OpenTripPlanner** (open-source engine, not a consumer app) — powers many transit apps. Supports own bicycle + transit and bike park-and-ride. Could be the backend for this idea. https://github.com/opentripplanner/OpenTripPlanner

**Key gap:** No mainstream global app lets you say "I own an e-scooter, comfortable range X km, speed Y km/h" and get optimized mixed routes. Citymapper comes closest but still doesn't expose range/speed parameters for personal vehicles.

**Monetization:**
- Freemium with saved vehicle profiles
- Partnership with transit agencies to surface underused stops
- Integration with scooter/bike manufacturers as a bundled app feature
