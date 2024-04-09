
## video and latency

*  Vehicle moving at the speed of 130 km/h moves 3cm/ms Typical reaction time of a driver is 500ms-1s. We want to target 1-5% of the driver reaction time (regulaton will say it's word for sure if the remote driving gets popular). This is **5-50ms round trip**. For slower moving vehicles like forklifts the network latency can in the 100-500ms range? Under 5ms roundtrip latency is not realistic in the modern generally available IP networks (proprietary **microwave relay** here?).
*  We need to deliver high quality video only for the area where the driver has his eyes on. 
*  We shall ensure under 5ms latency between recognition of a **saccade** and displaying a high resolution image in the right place. 
*  The car can record 360 degrees view in high resolution, but send only low resolution stream for all or most areas.
*  We want to minimize the network latency and impact of the network congestion. One of the ways to do this is to require 100% visibility for the microwave transmitters. 
*  Semi-autonomous driving/safe stop will help to reduce "down time" when the network is not available.
*  We can organize trains of semi-autonomous trucks controlled by a single driver sitting in the leading truck. This approach removes network from the equation.
*  We can employ control centers along the busy interstates - every 200km or so - and switch the remote control over the truck between the centers. In this deployment scheme the vehicle is always one hop connection from at least one control center and can communicate directly.

## Applications

Becasue the network is not scaling well realistic possibilities are:

* Vehicle recovery
* SOS services
* DUI avoidance
* military vehicles
* autonomous vehicle support
* automatic parking 
* industrial applications, like forklift

## Car integration 

* The driving interface in vehicles is not standart. Different types of vehicles will reuqire custom integration. Placement for the camera set is different as well. The software should accommodate differences in the hardware. Is it possible to reduce the problem to 2 or 3 conversion kits?

## Drivers environment 

* How to provide **tactile feedback** to the driver? For example, gear switch related vibration (the transmission is not ideally smooth), the engine noise, the vehicle inclination, turn signal clicking, the steering wheel feedback - all should be collected and delivered.
* This is not a computer game or training. How to keep the remote driver focused and motivated?

## Taxi

Taxi is tricky - most of the driving happens in the city. Network is congested or unavailable, network latency is high. The solution is nor scaling well. Even a small fleet of remotely controlled cars will easily consume the available bandwidth. 
Proprietary microwave relay is not a great solution for the city as well: deployment of antennas is regulated. In some cities there are already deployed microwave relays. Proprietary network can make sense in some circumstances. For example, such network is easier to isolate, secure. 

*  Agreeements with the cellular providers can resolve some of the QoS problems. 
*  Dedicated marking on roads, dedicated lanes which simplify the work for semi-autonomous cars.


## Links

*  https://www.quora.com/How-fast-can-the-human-eye-move
*  https://en.wikipedia.org/wiki/Eye_movement
*  phantom.auto is shutting down https://techcrunch.com/2024/03/12/remote-driving-startup-phantom-auto-is-shutting-down
