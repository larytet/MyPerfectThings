## Video and Latency

* A vehicle moving at a speed of 130 km/h moves 3 cm/ms. The typical reaction time of a driver is 500ms-1s. Our target is 1-5% of the driver's reaction time (regulations will likely intervene if remote driving becomes popular). This equates to a **5-50ms round trip**. For slower vehicles like forklifts, network latency can be in the 100-500ms range. Under 5ms roundtrip latency is not realistic in modern, generally available IP networks (perhaps a proprietary **microwave relay** solution?).
* We need to deliver high-quality video only for the area where the driver is looking.
* We shall ensure under 5ms latency between recognizing a **saccade** and displaying a high-resolution image in the right place.
* The car can record a 360-degree view in high resolution, but send only a low-resolution stream for most areas.
* We aim to minimize network latency and the impact of network congestion. One method is ensuring 100% visibility for microwave transmitters.
* Semi-autonomous driving/safe stop features can help reduce downtime when the network is unavailable.
* We can organize convoys of semi-autonomous trucks controlled by a single driver in the lead truck, removing the network from the equation.
* We can establish control centers along busy interstates (every 200km or so) and switch remote control of the truck between centers. In this scheme, the vehicle is always within a one-hop connection from at least one control center and can communicate directly.

## Applications

Given that the network does not scale well, realistic applications include:

* Vehicle recovery
* SOS services
* DUI avoidance
* Military vehicles
* Autonomous vehicle support
* Automated parking
* Industrial applications, like forklifts

## Car Integration 

* The driving interface in vehicles is not standardized. Different vehicle types will require custom integration. Camera placement also varies. The software should accommodate hardware differences. Can we reduce the problem to 2 or 3 conversion kits?

## Driver's Environment 

* How do we provide **tactile feedback** to the driver? Gear switch vibrations, engine noise, vehicle inclination, turn signal clicking, and steering wheel feedback should all be collected and delivered.
* This isn't a computer game or training simulation. How do we keep the remote driver focused and motivated?

## Taxi

Operating taxis remotely is challenging - most city driving involves congested or unavailable networks, and high latency. The solution does not scale well. Even a small fleet of remotely controlled cars will quickly consume available bandwidth. Proprietary microwave relay is not ideal in cities due to regulated antenna deployment. However, a proprietary network could be useful in some scenarios, such as easier isolation and security. 

* Agreements with cellular providers could solve some QoS issues.
* Dedicated markings on roads and lanes could simplify work for semi-autonomous cars.

## Links

* [Human Eye Movement Speed - Quora](https://www.quora.com/How-fast-can-the-human-eye-move)
* [Eye Movement - Wikipedia](https://en.wikipedia.org/wiki/Eye_movement)
* Phantom Auto is shutting down [TechCrunch](https://techcrunch.com/2024/03/12/remote-driving-startup-phantom-auto-is-shutting-down)
* German Vay
* Estonian Elmo
