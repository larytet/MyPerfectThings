# Dedicated Microwave Network for Remotely Operated Robots

A private, line-of-sight microwave network built as the shared low-latency backbone for remote operation. The original idea was remote driving of cars/taxis/trucks. That market does not scale on public networks (see [Why not taxis](#why-not-taxis)), so the focus shifts to **more general robotic services**: delivery robots, robotic construction equipment, and interbank links as the revenue anchor that pays for the network.

## Core Concept

* One owned network (towers, relays, a few control centers) instead of renting cellular QoS.
* Operators connect to many robot types through one low-latency, high-reliability pipe.
* The network is the product; robots are tenants/customers.
* Every robot type has a different latency budget, so one network serves a mix of workloads (see table).

| Workload | Round-trip target | Notes |
|---|---|---|
| Interbank / trading links | microseconds to 1 ms | Pays the most per bit; needs the shortest path |
| Fast vehicles (130 km/h) | 5-50 ms | 3 cm/ms; driver reaction is 500 ms-1 s |
| Delivery robots (sidewalk, low speed) | 50-200 ms | Mostly supervised autonomy; humans handle edge cases |
| Construction equipment (excavators, cranes, dozers) | 20-100 ms | Slow, heavy, bounded work site |
| Forklifts / yard vehicles | 100-500 ms | Slow, confined area |

## Applications

### Robotic delivery services

* Sidewalk and last-mile robots with a remote operator on call for obstacles, crossings, and doors.
* One operator supervises many robots (1:10 to 1:50); intervene only when the robot asks for help. Bandwidth is bursty, not continuous.
* Dedicated network gives predictable QoS in dense areas where cellular is congested.
* Low speed means the latency budget is relaxed and a safe-stop is cheap.
* Micro-hubs on rooftops double as microwave relay points and robot depots.

### Robotic construction equipment

* Excavators, loaders, cranes, compactors, drilling rigs operated from a remote cabin: safer (dangerous sites, mines, demolition, disaster recovery) and lets a skilled operator serve several sites per day.
* Work sites are fixed and temporary: a **portable microwave node** (mast on a trailer) can bring up a site link in hours, solving the "no network at the site" problem.
* Lower speed and bounded workspace make 20-100 ms acceptable; haptic feedback (bucket resistance, vibration) improves precision.
* Fleet use: tele-operation for hard tasks, autonomous repetitive tasks (grading, trenching), operator takes over on exceptions.
* Sites in remote areas often have clear line-of-sight, which is the ideal case for microwave.

### Interbank links

* Dedicated microwave links are the established low-latency medium for finance (the Chicago-New Jersey type routes): lower latency than fiber because radio travels near the speed of light in air on a straighter path.
* Customers pay a large premium per bit. This can **subsidize the robot network** (shared towers, shared spectrum licenses, shared maintenance crews).
* Interbank traffic gets priority and its own channels; robot traffic uses separate channels on the same towers.
* Weather (rain fade) is the weak point: needs a fiber or lower-band fallback for finance, and a safe-stop for robots.
* To confirm: scope of "interbank" - low-latency trading links, or inter-bank settlement/wire traffic (which is not latency critical and probably not a fit).

### Other (from the original idea)

* Vehicle recovery, SOS services, DUI avoidance
* Autonomous vehicle support (remote assistance when the car is stuck)
* Automated parking
* Military vehicles
* Industrial forklifts and yard trucks

## Why not taxis

Operating taxis remotely is the hardest case - kept here as the reason for the pivot.

* Most city driving has congested or unavailable networks and high latency.
* Even a small fleet of remotely controlled cars quickly consumes available bandwidth (video from several cameras per car, continuously).
* Microwave relay is not ideal in cities due to regulated antenna deployment and line-of-sight blockage.
* A proprietary network still helps with isolation and security, and could serve **highway corridors**, where cars are in line of sight of the towers.
* Agreements with cellular providers could solve some QoS issues.
* Dedicated markings on roads and lanes could simplify work for semi-autonomous cars.
* Phantom Auto shut down in 2024 - remote driving as a stand-alone business struggled. Robots with lower speed and a shared network look more viable.

## Network Design

* Target **under 5 ms round trip** end to end where needed. This is not realistic on generally available IP networks; a proprietary microwave relay is the way to get it.
* Ensure 100% visibility (line of sight) for microwave transmitters; plan hops accordingly.
* Control centers along busy interstates every ~200 km, with the vehicle always one hop from at least one center and the ability to hand over control between centers.
* Urban: rooftop relays, short hops, mesh topology for rerouting around blocked paths; regulated antenna deployment is a licensing and permitting problem.
* Portable nodes for construction sites and events.
* Spectrum: licensed bands (e.g. 6/11/18/23 GHz) for reliability, E-band (70/80 GHz) for short high-capacity hops. Needs regulator research per country.
* Redundancy: second path (fiber, cellular, satellite) used for fallback and for non-critical data.
* Convoys of semi-autonomous trucks controlled by a single driver in the lead truck remove the network from the equation.

## Video and Latency

* A vehicle moving at 130 km/h moves 3 cm/ms. The typical driver reaction time is 500 ms-1 s. Target 1-5% of that: **5-50 ms round trip** (regulations will likely intervene if remote driving becomes popular).
* Deliver high-quality video only for the area where the operator is looking.
* Ensure under 5 ms between recognizing a **saccade** and displaying a high-resolution image in the right place.
* The robot can record a 360-degree view in high resolution, but sends only a low-resolution stream for most areas.
* Semi-autonomous driving / safe-stop features reduce downtime when the network is unavailable.
* Minimize the impact of network congestion: dedicated channels, priority queueing, and per-robot bandwidth budgets.

## Robot Integration

* Control interfaces are not standardized: vehicles, delivery robots, and construction machines all differ, and camera placement varies.
* Define a **common teleoperation gateway** (video, telemetry, control, safe-stop heartbeat) with a few adapter kits per robot class. Can we reduce the problem to 2 or 3 conversion kits?
* Retrofit kits for existing construction machines (actuators on levers/joysticks, cameras, GPS, safety stop) are a business on their own.
* Safety: heartbeat and watchdog on every link; loss of link triggers a safe stop appropriate to the machine.

## Operator Environment

* How do we provide **tactile feedback**? Gear switch vibrations, engine noise, vehicle inclination, turn signal clicking, steering wheel feedback, bucket/blade resistance should all be collected and delivered.
* This isn't a computer game or training simulation. How do we keep the remote operator focused and motivated? Rotate tasks, mix supervision and active control, measure fatigue.
* Operator pools can be shared across customers and time zones (follow-the-sun) for delivery and construction.

## Business Model Ideas

* Anchor tenant: interbank/trading links (high margin) fund tower build-out.
* Network-as-a-service for robot operators: per-robot or per-Mbps with latency SLA.
* Teleoperation-as-a-service: network + operators + retrofit kits for construction firms.
* Site-in-a-box: portable node + cameras + operator cabin rental for temporary construction sites.

## Open Questions

* Which one to start with: construction (clear sites, slow machines, high operator cost savings) looks like the best first market.
* Spectrum licensing and tower permitting costs per country.
* Insurance and liability for remote-operated machines.
* Competition: 5G private networks (campus/site networks) are the obvious alternative for construction; what does microwave offer beyond that (range, latency, ownership)?

## Links

* [Human Eye Movement Speed - Quora](https://www.quora.com/How-fast-can-the-human-eye-move)
* [Eye Movement - Wikipedia](https://en.wikipedia.org/wiki/Eye_movement)
* Phantom Auto is shutting down [TechCrunch](https://techcrunch.com/2024/03/12/remote-driving-startup-phantom-auto-is-shutting-down)
* German Vay
* Estonian Elmo
