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

**Prior art / related:**
- Google Maps "bike + transit" mode exists but is limited and doesn't account for e-scooter speed or range preferences
- Citymapper does some multimodal routing but treats scooters as rentals, not owned vehicles
- Rome2rio handles long-distance multimodal but not micro-mobility
- Moovit, Transit app — solid transit, weak on personal micro-mobility integration
- OTP (OpenTripPlanner) open-source engine supports bike+transit; could be the backend

**Monetization:**
- Freemium with saved vehicle profiles
- Partnership with transit agencies to surface underused stops
- Integration with scooter/bike manufacturers as a bundled app feature
