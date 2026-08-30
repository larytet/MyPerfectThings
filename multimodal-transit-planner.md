Trip planning today assumes you either walk, drive, or take transit — but it ignores a large middle option: people who own an electric scooter, e-bike, or bicycle and can cover several kilometers quickly under their own power.

The idea is a routing app that treats your personal micro-mobility vehicle as a first-class input. You tell it: "I have an electric scooter, I can ride up to 8 km comfortably." The planner then finds routes that mix your scooter leg with buses, metro, trains, and ferries — finding the fastest door-to-door trip rather than the one with the fewest transfers or least walking.

Examples of what this unlocks:
- Ride 3 km to a metro station that Google Maps ignores because it assumes a 20-minute walk, then take one direct train instead of two with a transfer.
- Skip a crowded bus leg by scooting a parallel route that's faster at that time of day.
- Bring your bicycle on the train and ride the last 5 km — no parking needed at either end.

**Bringing your vehicle on transit — a key multiplier:**

Many transit systems allow passengers to bring personal micro-mobility vehicles on board, which changes the routing math significantly — the vehicle doesn't need to be locked at a station, and both legs of the trip can be covered door-to-door:

- **Trains** — many rail systems allow full-size bicycles during off-peak hours (e.g., Israel Railways allows bicycles in designated cars at non-rush hours). Foldable scooters and foldable bicycles are typically allowed at any hour without restrictions.
- **Buses** — many intercity and regional buses have luggage bays underneath where a scooter or folded bicycle fits. This makes the scooter usable on both the first and last mile without leaving it behind.
- **Metro/light rail** — rules vary by city; foldable vehicles are almost universally permitted.

The app needs to know: is your vehicle foldable? Then it can route you through train legs and bus legs where the vehicle travels with you, not just to/from a parking spot.

**Key inputs the user provides once:**
- Vehicle type (kick scooter, e-scooter, e-bike, bicycle, rollerblades)
- Whether it is foldable
- Comfortable range per leg in km
- Speed estimate or just let the app default by vehicle type

**What makes this hard:**
- Real-time transit data + bike routing in a single graph search
- Per-operator, per-line, time-of-day rules for bringing vehicles on board — this data is rarely machine-readable
- Scooter parking availability at stations (for non-foldable vehicles)
- Hills and terrain affecting realistic range

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

**Updates and additional apps (researched August 2026):**

- **Citymapper** — Acquired by Via Transportation (2023), still active. In 2026 launched AI-powered journey planning ("Citymapper CLUB") with personalized recommendations based on historical preferences and AI-generated trade-off summaries (speed/cost/walking/reliability). Closer to personalization but still addresses preferences, not vehicle physics. The core gap remains.
- **Transit App** — Added elevation-sensitive routing (avoids uphill legs unexpectedly) — directly relevant to e-scooter range on hills. In-app unlock and payment for shared scooters/bikes in ~10 cities (Chicago, Toronto, Montreal, Detroit, Minneapolis). Still no owned-vehicle range/speed profile.
- **Trafi** — Now primarily a B2B white-label MaaS platform (acquired by Enghouse, April 2025); not a standalone consumer app. City-branded deployments (e.g., Jelbi for Berlin) show real-time availability + battery range for *shared* scooters (Voi, Lime, Bolt) but not personally-owned vehicles. Effectively inaccessible as a global consumer product.
- **Metropia** (not previously listed) — MaaS intermodal planner with first/last mile integration; personalization based on walking/biking speed preferences. B2B city-contract platform, not a standalone consumer app. Relevant as a benchmark for what cities are deploying.
- **Magic Earth** (not previously listed) — OpenStreetMap-based, privacy-first (no account, no tracking), offline maps. Has vehicle profiles for car/bike/walk but no transit integration and no e-scooter mode. Niche: privacy-focused users; doesn't solve the multimodal problem.

**Monetization:**
- Freemium with saved vehicle profiles
- Partnership with transit agencies to surface underused stops
- Integration with scooter/bike manufacturers as a bundled app feature
