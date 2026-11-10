# "Teach me riding a bicycle" - requirements and design spec (draft v0.1)

A bolt-on kit for an ordinary bicycle that helps a learner (child or adult) to ride without falling, and then takes the help away as the rider improves. It shares its control loop and sensors with the balance-assist ideas in [smart-footwear-motorized-wheel.md](smart-footwear-motorized-wheel.md) (skates, fall-prevention shoes) and [self-balancing-shopping-cart.md](self-balancing-shopping-cart.md) (tandem balancing).

All numbers marked "estimate" come from my own sizing calculations or typical distributor prices, not from quotes or measurements. Part numbers are candidates, to be checked for availability and datasheet limits before a design is frozen.

## 1. Summary of the decision

Balancing the bicycle with a flywheel or gyro is not feasible for a loaded bicycle (section 3.1). The product therefore does not balance the bike. It is **adaptive training wheels**: two side wheels on motorized arms that

1. act as normal training wheels at a standstill and at walking pace,
2. limit how far the bike can lean, and open that limit step by step as the rider gets better (the "assist level"),
3. fold up completely once the rider no longer needs them,
4. and tell the rider what to do through handlebar vibration, LEDs and a phone app (steer into the lean, keep speed up, pedal steadily).

## 2. Prior art (checked, so this is not a clean field)

*  **US 7,556,277 "Bicycle training aid with dynamically deployable balancing features"** - remote-controlled deployable training wheels. A speed sensor retracts the wheels automatically at a set speed such as 5 mph, and an optional gyro redeploys them if the child starts tipping (greater than 15 degrees per 50 ms). A related continuation, **US 9,771,029 "Bicycle training aid with intelligent controller"**, covers an intelligent controller. [US7556277B2](https://patents.google.com/patent/US7556277), [US9771029 PDF](https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/9771029). Auto-retract on speed and redeploy on tipping is therefore already claimed. A freedom-to-operate check is needed before building. I did not read the claims in detail.
*  **"Real-time retractable training wheels" patent family** - a mechanical lift operated by a grip, lever or switch, not automatic. [US9284002](https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/9284002), [US11001322](https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/11001322).
*  **Gyrobike / Jyrobike** - a freewheeling mass in the front wheel (motor-driven to about 2,000 rpm in the battery version) that adds gyroscopic stability. The UK version was reported at £229 for ages 3-6. Jyrobike ran a 2014 Kickstarter with a $100,000 goal. Developer claims of learning in under 30 days are not independent results. A Cambridge engineering page argues gyroscopic effects matter little for bicycle stability and that trail matters more. [Cambridge page](https://www3.eng.cam.ac.uk/~hemh1/gyrobike), [BikeRadar](https://www.bikeradar.com/news/gyroscopic-technology-to-revolutionise-way-kids-learn-to-ride), [New Atlas](https://newatlas.com/jyrobike-balancing-bicycle/32558), [Wikipedia](https://www.wikipedia.com/wiki/Jyrobike)
*  **EZ Training Wheels** - an adjustable spring-based design on Kickstarter, no electronics. Kicktraq lists 365 backers and $19,416 against a $1,000 goal. [Kicktraq](https://www.kicktraq.com/projects/eztrainingwheels/ez-training-wheels/)
*  **Motorcycle auto-deploy outriggers (LegUp)** - deploy below about 6 mph (10 km/h) and retract above. Same idea on a motorcycle. [Mike Shouts](https://mikeshouts.com/?p=253168)

What I did not find: a product that **adapts the lean limit to the rider's measured skill**, uses the sensors to **coach** the rider, and works as a **retrofit kit for adults too**. That, not the retracting wheels, is what this spec proposes as the new part.

## 3. Feasibility analysis (why training wheels and not a balancing bike)

Setup: child + small bike 28 kg, centre of mass 0.9 m high; adult + bike 90 kg, 1.0 m high.

### 3.1 Flywheel and gyro balancing: rejected

*  The gravity torque on a leaning bike is m g h sin(lean). Child: 21.5 Nm at 5 degrees, 64 Nm at 15 degrees. Adult: 77 Nm at 5 degrees, 229 Nm at 15 degrees.
*  A reaction wheel stores angular momentum and can only deliver a torque until it saturates. A 1 kg, 70 mm radius disc at 3,000 rpm holds about 0.77 Nms. At the child's 5-degree lean torque it saturates in about 0.04 s. That is why the reaction-wheel balancers I found (Murata Boy, hobby builds) are small robots.
*  A control moment gyro (gimbaled flywheel) of the same size gives about 7.7 Nm at a 10 rad/s gimbal rate, still well below the child's 15-degree load. Lit Motors' C-1 quotes about 800 Nm for a full-size vehicle. Weight, power draw and cost are far too high for a bicycle kit.
*  Steering-based balancing (Honda Riding Assist-e) needs a steering actuator that fights the rider's hands, and it is a concept with no production commitment. Rejected for v1. It is a possible v2 for the adult variant (a small steering nudge).

### 3.1b Gyro in place of the rear wheel: rejected

The question: could a gyro replace the rear wheel? I found no one who has done it.

*  A bicycle wheel is already a gyro, but a weak one: about 2.7 Nms at 20 km/h (estimate: 1.5 kg effective rim mass, 0.33 m radius). A purpose-built flywheel (3 kg, 150 mm radius, 5,000 rpm) holds about 18 Nms, still far below the child's 15-degree lean torque of about 64 Nm.
*  The rear wheel gives the second ground contact, traction and drive. Without it the vehicle is a one-wheeler: a gyro could handle roll, but pitch would need a motor-driven balance loop like a Onewheel or unicycle.
*  A gyro stabilizes through a gimbal, which saturates under a sustained lean load. It damps wobble well but cannot hold a steady lean.
*  A learner needs a real bicycle, so removing a wheel does not suit this product. A gyro module on the frame would be the alternative, with the weight and cost problems from section 3.1.

Prior work and related designs:

*  **Gyrobike Gyrowheel** - motor-driven spinning disc inside the front wheel of a kids' bike. The closest commercial product, but the front wheel, not the rear. A Cambridge engineering page doubts the gyro does much of the stabilizing. [BikeRadar](https://www.bikeradar.com/news/gyroscopic-technology-to-revolutionise-way-kids-learn-to-ride), [Cambridge](https://www3.eng.cam.ac.uk/~hemh1/gyrobike)
*  **Halfbakery concept** - an unbuilt idea that drops the front wheel, moves the seat back over the rear wheel and adds two gimbaled gyros. The inverse of this question. [Halfbakery](https://www.halfbakery.com/idea/Unicycle_20with_20gimballed_20gyroscopes)
*  **Brennan gyro monorail (1900s-1910s)** - two counter-rotating gyros, carried passengers at 40 km/h. [Wikipedia](https://en.wikipedia.org/wiki/Gyro_monorail), [Science Museum](https://collection.sciencemuseumgroup.org.uk/objects/co27065/brennans-gyroscopic-mono-rail-car)
*  **Shilovsky gyrocar** - two wheels in tandem and a single gyro, reported unstable in sharp left turns. A University of Michigan paper says a two-wheeled gyro car was built in 1913. [Michigan paper](https://public.websites.umich.edu/~arclab/max/media/gyrovehicle.pdf)
*  **Gyro-X (Alex Tremulis)** - a concept for a streamlined two-wheeled gyro car. I found no detail on whether it was built.
*  **Gyro-balanced bicycle research** - an Auburn paper uses a vertical-axis control gyro to balance a bicycle at zero speed. A Stanford paper (ACC 2014) covers control moment gyro stabilization of two-wheelers. [Auburn](https://www.eng.auburn.edu/~jhung/bicycle_paper.doc), [Stanford](https://web.stanford.edu/~kalouche/docs/ACC_2014.pdf)
*  **Gyrocycle (Thrustcycle Enterprises)** - a self-stabilizing bike; I only saw the headline, so check it. [InsideHook](https://www.insidehook.com/autos/thrustcycle-enterprises-gyrocycle-motorcycle)
*  **Lit Motors C-1** - two gyros in a two-wheeled enclosed vehicle (see [self-balancing-shopping-cart.md](self-balancing-shopping-cart.md)).

### 3.2 Adaptive outriggers: chosen

*  A passive stop is strong and needs no fast actuation. The motor only moves the stop position slowly, so power draw stays low (about 1 W average, section 8).
*  Geometry: outrigger wheel at lateral offset b from the bike's centre plane. Ground clearance at the wheel is about b sin(lean angle), so an outrigger set at clearance c allows a lean of asin(c / b). With b = 0.30 m: 3 degrees = 16 mm, 8 degrees = 42 mm, 15 degrees = 78 mm. With b = 0.35 m (adult): 18, 49, 91 mm.
*  Load on one outrigger when the bike leans onto it: F is about m g (h / b) tan(lean). Child: 43 N at 3 degrees, 116 N at 8 degrees, 221 N at 15 degrees. Adult: 132 N, 355 N, 676 N. Design load: 1.5 kN lateral at the wheel (about 2x the adult 15-degree value, for impacts and a rider falling onto it).
*  A self-locking worm gear holds the arm without power. A slip clutch or shear pin protects the gearbox.

## 4. Users and use cases

| User | Weight limit (rider + bike) | Bike | Notes |
|---|---|---|---|
| Child 4-10 | 45 kg | 14"-20" wheels | Parent buys. Parent sees progress in the app. |
| Adult learner | 120 kg | 26"-28" wheels | Embarrassment matters: should look discreet, fold away fast. |
| Rehab / older rider (later) | 120 kg | any | Overlaps with fall-prevention shoes, would need a medical-device assessment. |

Use cases: (1) first ride, (2) practice sessions with progress, (3) stopping and starting, (4) transport and storage (the kit folds up against the frame), (5) parent or coach watching in the app.

## 5. Requirements

Priority: M = must, S = should, C = could.

### 5.1 Functional

| ID | Requirement | Pri |
|---|---|---|
| FR-1 | The outriggers hold the bike upright at a standstill (lean limit <= 3 degrees) when speed < 3 km/h. | M |
| FR-2 | While riding, the outriggers limit lean to the current assist level's limit (levels L0-L5, from 3 to 15 degrees; L6 = folded up). | M |
| FR-3 | The assist level can be set manually (app or button) and, in auto mode, advances or steps back from measured skill metrics (section 7.3). | M |
| FR-4 | The outriggers fold up fully (L6) and the kit then does nothing but log data and give cues. | M |
| FR-5 | The rider can fold or deploy the outriggers by hand (button on the handlebar) at any time. A parent or coach can do it from the app. | M |
| FR-6 | Handlebar cues: left and right grip vibration, an LED bar showing lean, optional buzzer. Cues are rate-limited (no more than 1 per 2 s). | S |
| FR-7 | Phone app: live lean, speed and assist level, session history, parent view, voice cues. The kit works without the phone (levels and cues run on the board). | S |
| FR-8 | Per-session metrics: time within the lean limit, number and size of outrigger touches, speed stability, steering-into-lean response, session length. | S |
| FR-9 | Firmware update over BLE (secure DFU). | M |
| FR-10 | Fits a standard bicycle by clamping to the seat tube, seat stays and rear axle area, with no frame modification. | M |
| FR-11 | Anything that fails (sensor, motor, low battery) leaves the arms where they are and the bike rideable, and tells the rider. | M |

### 5.2 Performance

| ID | Requirement |
|---|---|
| PR-1 | Lean (roll) angle estimate error <= 1 degree RMS in a steady turn, using a centripetal correction. Update rate 200 Hz. |
| PR-2 | Arm moving from deployed to fully folded in <= 3 s, and back in <= 3 s. |
| PR-3 | Lean limit setpoint accuracy +/- 1 degree (position feedback on each arm). |
| PR-4 | Battery life >= 10 hours of riding per charge; charge time <= 3 hours via USB-C. |
| PR-5 | Total kit mass <= 1.3 kg (child), <= 1.8 kg (adult). |
| PR-6 | BLE range >= 10 m. Phone latency does not matter for safety functions. |

### 5.3 Safety and mechanical

| ID | Requirement |
|---|---|
| SR-1 | The outrigger structure withstands 1.5 kN lateral at the wheel (child kit sized to 1 kN) with no permanent deformation. To be verified by test. |
| SR-2 | Deployment and folding can never trap fingers. Pinch points guarded, motor current limited. Folding is blocked while the rider is leaning on an outrigger (load detected). |
| SR-3 | The board must not move an arm while braking is suspected (rapid deceleration) unless it is a deploy. |
| SR-4 | A power loss or a crashed processor leaves the arms mechanically locked in their last position. A hardware watchdog restarts the MCU. |
| SR-5 | The kit never touches brakes, gears or steering. |
| SR-6 | The arms cannot fold up by themselves from vibration or a bump. Self-locking drive plus a detent. |
| SR-7 | The default auto level never moves to a wider limit when speed or lean data is invalid. |
| SR-8 | Cells have protection against over-charge, over-discharge, short-circuit and over-temperature. Battery enclosure rated IP54 and crash-tested for the cell retention. |
| SR-9 | Auto-advance to wider limits needs an explicit one-time parental confirmation for child kits. |

### 5.4 Environmental and regulatory (check with a test lab, applicability not confirmed)

*  IP54 minimum (rain, splash, dust). Operating -10 to 45 C.
*  Cycle safety: ISO 4210 (bicycles), ISO 8098 (bicycles for young children). The kit is an accessory, so applicability needs confirming.
*  Li-ion cells: IEC 62133-2, shipping UN 38.3.
*  Radio: FCC Part 15 (US), EU Radio Equipment Directive (RED). Using a pre-certified BLE module reduces testing.
*  Children's products: CPSIA (US), EN 71 (EU toys) if sold as a children's product. General product safety regulation in the EU.
*  Privacy: child data (ride logs) stays on the phone by default, no account needed. Applies to children's privacy laws (COPPA, GDPR-K).

## 6. System design

### 6.1 Architecture

```
           +--------------------------- handlebar module ---------------------------+
           |  haptic L/R (ERM)   LED bar (8 px)   button (fold/deploy)  buzzer      |
           +------------------------------------+-----------------------------------+
                                                | 6-wire harness (power, data, GND)
 +---------------------- main enclosure (seat tube) ------------------------------+
 |  2S Li-ion (2x18650)  --> charger/protection --> 3.3 V buck                     |
 |         |                                                                       |
 |         +--> motor drivers (2x) ---> arm gearmotors L/R (worm, encoder + clutch)|
 |  nRF52840 BLE MCU <-- IMU (roll/yaw rate/accel)                                 |
 |         ^---------- steering angle sensor (magnet on headset)                   |
 |         ^---------- wheel speed hall (magnet on spoke)                          |
 |         ^---------- cadence hall (optional, magnet on crank)                    |
 |         +--> BLE --> phone app (coach, parent view)                             |
 +---------------------------------------------------------------------------------+
        |                                               |
   left outrigger arm + wheel                      right outrigger arm + wheel
```

### 6.2 Mechanical outline (estimate)

*  Main enclosure on the seat tube (battery, board, IMU). The IMU is rigid and close to the bike's centre line.
*  Each arm: aluminium arm about 300 mm (child) or 350 mm (adult) with a 75 mm wheel, pivoting on a bracket at the rear axle / seat stay. Worm gearmotor at the pivot, an absolute angle sensor on the arm, a slip clutch between the gearbox and the arm.
*  Arm motion: swings from "down" (deployed) up through the stop settings to "up" (folded against the stay). The mapping from arm angle to lean limit is a calibrated table in firmware.
*  Handlebar module on the stem with a short cable. Grips with a vibration motor on each side are a later, optional accessory.

### 6.3 Control logic

States: OFF, STANDSTILL, RIDING, FOLDED, FAULT.

*  Roll angle: gyro integration with a slow accelerometer correction. In a turn, the accelerometer's gravity direction is biased by centripetal acceleration (about v times yaw rate), so subtract it using wheel speed and the yaw-rate gyro axis.
*  Speed < 3 km/h -> STANDSTILL: both arms to the level L0 stop (about 3 degrees) so the bike stands.
*  Speed >= 3 km/h -> RIDING: arms to the stop for the current level (L0-L5), moved slowly and never while an arm carries load.
*  Level L6 (folded) is only reachable from L5 and the rider can always override it with the button.
*  Safety interlocks: no arm movement while an arm's motor current shows load (rider leaning on it), no widening if a sensor is invalid.

### 6.4 Assist levels (starting values, to tune with real riders)

| Level | Lean limit | Condition to advance (auto) |
|---|---|---|
| L0 | 3 degrees (fixed, training-wheel mode) | 3 sessions with <= 20% of ride time touching an outrigger |
| L1 | 5 degrees | same, plus speed held within +/- 2 km/h for 30 s |
| L2 | 8 degrees | same, plus a successful start from standstill |
| L3 | 11 degrees | same, plus 5 steer-into-lean responses within 0.5 s |
| L4 | 15 degrees | 3 sessions with <= 5% touching |
| L5 | outriggers hover about 100 mm over the ground (about 20 degrees) | 3 sessions with no touches |
| L6 | folded | rider and parent confirm |

Step-back rule: if touches exceed 40% of ride time for two sessions, go back one level. The aim is to allow small errors and stop only the big ones, so the rider still learns to balance.

## 7. Sensing and feedback

### 7.1 Sensors

| Sensor | Purpose | Candidate part |
|---|---|---|
| 6-axis IMU | roll angle, roll rate, yaw rate, vibration | ICM-42688-P or BMI270 |
| Steering angle (magnetic encoder, 12 bit) | detects steering into the lean | AS5600 + 6x2 mm diametric magnet |
| Wheel speed (hall switch + magnet) | speed, standstill detection | DRV5032 class low-power hall |
| Cadence (hall, optional) | pedalling steadiness | same part |
| Arm angle (magnetic encoder or potentiometer) | stop position feedback | AS5600 or a gearmotor with a built-in pot |
| Motor current (driver current-sense output) | detects an outrigger carrying load (touch) | built into the driver |
| Battery voltage and temperature | protection and range estimate | MCU ADC + NTC on the pack |

The motor current is a useful learning metric by itself: it says how much the rider is leaning on the outriggers, without extra sensors.

### 7.2 Cues to the rider

*  Vibration in the left or right grip: "steer left" or "steer right" (the rider leans left, so steer left).
*  LED bar on the handlebar: a green centre pixel for upright, moving to the side with the lean, red at the limit.
*  Buzzer: a short beep when the speed falls below the minimum for the level ("pedal").
*  App voice: spoken coaching, "look ahead", "keep pedalling", "good, no touches in the last minute". Delivered in the phone, not required for safety.

### 7.3 Skill metrics

Time inside the lean limit, touch count and size (motor current), speed variance, response time between lean and steering, number of successful starts from standstill. All computed on the board, summarised per session, stored in flash (about 30 sessions) and synced to the app.

## 8. Rough electronics board

### 8.1 Target

One board 60 x 40 mm, 4 layers, 1.0 mm thick, in the main enclosure. Handlebar module is a separate small flex or rigid board with the LEDs, buzzer, button and haptic drivers.

### 8.2 Block list and candidate parts

| Block | Part (candidate) | Notes |
|---|---|---|
| MCU + BLE | nRF52840 certified module (Raytac MDBT50Q or Fanstel BT840 class) | Cortex-M4F with FPU, 1 MB flash, BLE 5, built-in antenna in the module, FCC/CE modular approval |
| IMU | ICM-42688-P or BMI270 | SPI, 1.6 kHz output rate with the low-pass filter set to about 100 Hz |
| Motor drivers | 2x DRV8874 class (H-bridge, PWM interface, current-sense output, 4.5-37 V) | Verify the 2S voltage range (6-8.4 V) and the stall current limit in the datasheet |
| Motor current sense | the driver's current-sense output into 2 MCU ADC pins | no extra shunt amplifier |
| Charger | 2S Li-ion charger with USB-C input (BQ25887 class) | Check balancing, charge current <= 1 A and temperature input |
| Pack protection | 2S protection IC + back-to-back MOSFETs | over-charge, over-discharge, short-circuit, cell balance |
| 3.3 V supply | low-Iq buck (TPS62840 class) | the board draws about 15 mA awake, so quiescent current matters |
| Steering encoder | AS5600 (I2C) | 12 bit, on the seat tube side of a short flex to the head tube magnet |
| Arm encoders | 2x AS5600 or potentiometers on the gearmotors | |
| Hall inputs | 2x DRV5032 class hall switches (wheel, cadence) | on short cables with a connector |
| Haptic | 2x ERM motor, each driven by a logic-level N-MOSFET with a flyback diode, PWM from the MCU | simpler than LRA drivers with an I2C mux. LRA upgrade later |
| LED bar | 8x tiny addressable LEDs (SK6805-EC15 class) | on the handlebar board |
| Buzzer | piezo, driven by the MCU PWM | |
| Connectors | 2x motor + encoder (JST-GH 6 pin), 1x handlebar (JST-GH 6 pin), 2x hall (JST-SH 3 pin), battery, USB-C | all keyed, sealed in the enclosure with grommets |
| Protection | reverse-polarity MOSFET, PTC resettable fuse on the motor rail, TVS on external connectors, ESD on USB | |

### 8.3 Power tree

```
USB-C 5 V --> 2S charger --> 2S Li-ion pack (6.0-8.4 V) --+--> motor rail (via PTC, 6.0-8.4 V) --> 2x motor driver
                                                           +--> buck 3.3 V --> MCU module, IMU, encoders, halls, LEDs, haptic FETs
```

Power budget (estimate, average over riding): MCU and sensors about 0.05 W, haptic bursts about 0.02 W, LED bar about 0.03 W, arm moves (about 4 s per minute at about 1 A, 7.4 V, both arms) about 0.9 W. Average about 1.1 W. A 2 x 18650 pack of about 23 Wh usable gives about 20 hours of riding, so the 10-hour target has margin and one cell pack could even be smaller. If the arms mostly stay put (outriggers off), average drops below 0.2 W.

Peak current: two motors stalled at 2 A each is 4 A at 7 V (28 W). The PTC and the driver current limit stop a stall from overloading the pack.

### 8.4 MCU pin plan (nRF52840, rough)

| Function | Interface | Pins |
|---|---|---|
| IMU | SPI + INT1 | 4 + 1 |
| Steering and arm encoders | I2C bus (3x AS5600 share an address, so use one I2C bus per encoder or an I2C mux, or use analog potentiometers for the arms) | 2 (+ mux, or 2 extra pins) |
| Motor driver L and R | PWM + direction + current-sense ADC | 3 + 3 |
| Hall wheel and cadence | GPIO with interrupt | 2 |
| Haptic L/R | PWM to MOSFET gate | 2 |
| LED data | GPIO (bit-banged or I2S) | 1 |
| Buzzer | PWM | 1 |
| Button | GPIO with wake | 1 |
| Charger status and temperature | GPIO + ADC | 2 + 1 |
| Battery voltage | ADC | 1 |
| Debug | SWD | 2 |
| Spare | | 4 |

About 30 pins used, so the module (48 GPIO) has margin. The AS5600 has a fixed I2C address, so in practice use a single I2C bus plus a small I2C mux, or one encoder on I2C and potentiometers on the arms.

### 8.5 Layout notes

*  Keep the BLE module's antenna end at the board edge with the manufacturer's copper keep-out, away from the motor wires and the aluminium arm brackets.
*  Put the IMU near the centre of the board, away from the motor drivers and the buck inductor, and mount the board rigidly (no soft pads) so the roll estimate does not see enclosure motion. Isolate vibration with the filter, not with foam.
*  Motor drivers, PTC and the motor connectors on one side with a wide ground area. Route the motor current away from the analog and IMU area.
*  Ground plane on layer 2, power plane on layer 3. Test points on every rail and every bus.
*  Conformal coating, or a sealed enclosure with a gasket. USB-C port behind a rubber plug.

### 8.6 Firmware outline

Zephyr or nRF Connect SDK. Tasks: sensor sampling at 200 Hz, state estimator, level controller and arm position control (slow loop at 50 Hz), motor current monitoring (1 kHz), cue generator, BLE GATT (live data, settings, session log), DFU bootloader, flash logging with wear levelling, hardware watchdog. Phone app: iOS and Android, or a web page using Web Bluetooth for the first prototype.

## 9. Bill of materials and weight (estimate)

Volume assumption 1,000 units, child kit. Prices are typical distributor or Asian OEM prices, not quotes, and the error is about +/- 30%.

| Group | Item | Qty | Cost (USD) | Mass (g) |
|---|---|---|---|---|
| Electronics | nRF52840 module | 1 | 8.0 | 2 |
| | IMU | 1 | 3.5 | 0.1 |
| | 2 x motor drivers | 2 | 5.0 | 0.1 |
| | Charger IC + 2S protection IC + MOSFETs | 1 set | 5.0 | 1 |
| | Buck 3.3 V + inductor | 1 | 1.2 | 1 |
| | Steering encoder + magnet | 1 | 2.5 | 1 |
| | Hall sensors and magnets (wheel, cadence) | 2 | 1.4 | 5 |
| | USB-C connector + ESD | 1 | 1.2 | 1 |
| | Haptic motors + MOSFETs | 2 | 2.0 | 4 |
| | LED bar + buzzer + button (handlebar board) | 1 set | 3.0 | 6 |
| | Connectors, passives, protection parts | 1 set | 6.0 | 4 |
| | PCB (4 layer, 60x40) + assembly | 1 | 7.0 | 10 |
| | Electronics subtotal | | **45** | **~35** |
| Power | 2 x 18650 cells (3000 mAh class) | 2 | 5.0 | 92 |
| | Cell holder / tabs / harness to board | 1 | 1.5 | 15 |
| Actuators | Worm gearmotor with built-in angle sensor | 2 | 30.0 | 220 |
| | Slip clutch / shear pin set | 2 | 3.0 | 15 |
| Mechanics | Aluminium arms, 300 mm | 2 | 12.0 | 280 |
| | Outrigger wheels, 75 mm with bearings | 2 | 6.0 | 140 |
| | Frame clamps and pivot brackets | 1 set | 10.0 | 180 |
| | Fasteners, detent, covers | 1 set | 4.0 | 40 |
| Enclosure and cabling | Main enclosure (IP54, 2 parts) + gasket | 1 | 6.0 | 45 |
| | Handlebar module housing + mount | 1 | 3.0 | 20 |
| | Harness (motors, handlebar, halls) | 1 | 6.0 | 50 |
| Packaging | Box, manual, USB-C cable | 1 | 4.0 | n/a |
| | **Total** | | **~145** | **~1,130** |

*  **BOM about $145 (range $110-190).** If the retail price is 2.2-2.5 times the BOM, that gives about $320-360 for a child kit (the Gyrobike's UK price of £229 is a loose reference, not a target).
*  **Weight about 1.1 kg (range 0.9-1.4 kg)**, within the 1.3 kg child target. Over 95% of the weight is mechanics, battery and actuators, not electronics (electronics are about 35 g plus 92 g cells). Cutting weight means shorter arms, a single-cell pack and lighter gearmotors, not board changes.
*  **Adult kit estimate:** heavier arms and clamps, larger wheels and gearmotors, about 1.5-1.8 kg and a BOM of about $180-230.
*  Not in the BOM: tooling (injection molds, about $30-80k for the enclosures and parts, estimate), certification (cycle, radio, battery, children's product tests), app development, and the patent clearance.

## 10. Risks and open questions

1. **Patents.** US 7,556,277 and its continuation cover auto-retract and tipping redeploy. Check the claims and the expiry before building. The adaptive level logic and the coaching are the possible differentiators.
2. **Does it teach?** Training wheels are known to teach balance poorly, because the bike stays upright without leaning. The lean-limit approach is meant to fix that, but it is untested. Needs a pilot with real learners and a control group.
3. **Liability.** Children's product, a fall with a powered mechanism, arm failures. Insurance and certification costs are likely high.
4. **Mechanical load.** 1.5 kN design load needs real testing, and the arm needs a clutch so the gears survive a fall onto it.
5. **Roll estimate.** The centripetal correction is untested on a wobbling learner. Prototype with a logged IMU on a normal bicycle first.
6. **Fit across bikes.** Seat stays, racks, fenders and disc brakes vary. A universal clamp is hard.
7. **Price.** $320-360 against a pair of ordinary training wheels, and against a balance bike (which teaches without any electronics).

## 11. Next steps

*  Log a week of IMU, speed and steering data from learners on a normal bicycle (phone or a dev board) to check the roll estimate and the skill metrics before building arms.
*  Build a manual-lever prototype of the arm with adjustable stops and measure the loads.
*  Build the board as a breadboard stack: nRF52840 dev kit + IMU breakout + two driver breakouts + AS5600 breakouts.
*  Read the claims of US 7,556,277 and US 9,771,029.
*  Reuse the same board for the skates (replace the arm motors with the wheel motor) and test the shared balance-assist loop there.
