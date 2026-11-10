# "Help to ride roller blades" - requirements and design spec (draft v0.1)

A retrofit kit for inline skates that gives the skater a gentle motor assist while skating (uphill help, slip prevention, downhill braking) and cues to improve technique. It builds on the idea in [smart-footwear-motorized-wheel.md](smart-footwear-motorized-wheel.md) (motorized wheel, sensors, gradual introduction mode, prior art) and shares the balance-assist loop with [teach-me-riding-a-bicycle.md](teach-me-riding-a-bicycle.md). I read "help to ride" as assisted skating for ordinary and beginner skaters. If you meant something narrower (beginners only, or uphill only), the requirements in section 4 split easily by mode.

All numbers marked "estimate" come from my own sizing or typical prices, not from quotes or measurements. Part numbers are candidates to check against datasheets and availability. I did not find any source on where competing products (Moonwalkers and others) put their batteries, so the battery comparison is engineering reasoning, not a market survey.

## 1. Summary of the decisions

*  **One skate module, two battery options.** Each skate has its own controller, a hub-motor wheel and sensors. The module accepts power from a pack built into the skate (Option A) or from a belt-worn pack through a cable (Option B). Both run on a 3S Li-ion system (9-12.6 V), so the same module serves both.
*  **Recommendation: Option B (belt pack) for v1, changed after your comment on foot weight.** Skaters lift and swing each leg every stride, so mass on the foot costs far more than the same mass at the waist. Option B keeps the pack off the foot and cuts the net added mass per skate from about 460 g to about 290 g. The price is a cable on each leg (section 7). Option A (battery in each skate) stays as a later variant for short rides with a small pack, and the skate module accepts either (section 6).
*  **Wiring for Option B:** one cable per leg, never between the legs, on the outer side of the leg in a sleeve with a slack loop at the knee and a magnetic breakaway connector at the skate. No adhesive on the skin and no pinning (section 7).
*  **A wrist remote with vibration.** A small wrist-worn remote (strap, over or on a wrist guard) sets the assist level, has a big stop button, and gives vibration cues. It also acts as a dead-man link: if the remote disconnects, the assist turns off (section 7b).
*  **The skater still does the work.** The motor adds torque during the push, never acts as a throttle, and the wheel freewheels when not assisting.

## 2. Users and use cases

| User | Need | Notes |
|---|---|---|
| Recreational adult skater | help on hills and at the end of a long ride | main target, 50-100 kg |
| Beginner | slip prevention, speed limit, gentle assist | beginner mode (section 4.3) |
| Commuter (later) | range, reliability, lights | needs Option B or a larger pack |

Use cases: (1) put the skates on and go, no setup, (2) climb a 3-8% slope with less effort, (3) brake with regeneration on a downhill, (4) learn: cues and a learning mode over the first 3-5 km, (5) charge and carry the skates indoors.

## 3. Sizing (estimates)

Assumptions: 80 kg skater, 18 km/h (5 m/s), skating rolling-resistance coefficient 0.012, drag area 0.275 m2.

*  Mechanical power: flat about 68 W. Climbing adds m g v slope: 3% about 118 W, 5% about 196 W, 8% about 314 W (climb only, on top of the flat figure).
*  Assist target: an average of 30-100 W of motor mechanical power across both skates. At 0.7 total efficiency and assist active 60% of the time (only during the push), the average electrical draw is 26-86 W.
*  Design point: 40 W average assist, about 34 W electrical. A 55 Wh total pack gives about 1.6 hours (regeneration gains ignored). At 40 W the assist covers about 20% of the 5% climb power, so the skater still does most of the work.
*  Peak per skate: 60 W electrical, 5.4 A at 11.1 V (6.7 A at a sagging 9 V). Inside the 8 A limit of the candidate motor driver.
*  Pack mass: about 150 Wh/kg at pack level (cells plus protection, estimate). 55 Wh needs about 0.37 kg of cells and protection, and about 0.45-0.5 kg with cases and holders.

## 4. Requirements

Priority: M = must, S = should, C = could.

### 4.1 Functional

| ID | Requirement | Pri |
|---|---|---|
| FR-1 | **Push assist:** adds motor torque during the skater's push (detected from IMU and frame load). It never drives the skate when the skater is gliding or standing, and is limited to a maximum boost of 10% speed. | M |
| FR-2 | **Hill assist:** assist level scales with the slope estimated on the skate (section 6.3). | M |
| FR-3 | **Regenerative brake:** on downhills above the set speed the motor gently brakes and returns energy to the battery. Braking torque ramped and capped. | S |
| FR-4 | **No lock-up:** the wheel freewheels whenever the assist is off or any fault is present. | M |
| FR-5 | **Speed cap:** no assist above 25 km/h (adjustable lower), and braking only below the cap. | M |
| FR-6 | **Anti-rollback:** if the skate starts rolling backward the motor brakes softly. | S |
| FR-7 | **Beginner mode:** lower assist, lower speed cap, anti-rollback, gentle ramps, and a graduated increase of the assist over the first 3-5 km. | M |
| FR-8 | **Cues:** LED cues on the skate and phone voice cues (push harder, glide longer, lean forward). The main cue channel is the wrist remote (FR-18). Rate-limited. | C |
| FR-9 | **Stop button:** an immediate assist-off by heel tap gesture, a button on the skate and an app button. | M |
| FR-10 | **Phone app:** assist level and mode, ride stats, battery state, firmware update. The skates work without the phone. | S |
| FR-11 | **Skate-to-skate coordination** over BLE (which foot is pushing). A lost link falls back to independent operation. | S |
| FR-12 | **Lights:** front and rear LED on each skate (visibility). | C |
| FR-13 | **Firmware update** over BLE with signed images. | M |
| FR-14 | **Wrist remote:** assist level up and down, mode, and a large stop button, with a vibration motor for cues. Works without the phone. | M |
| FR-15 | **Dead-man link:** with the remote enabled, losing the link to the remote for more than 0.5 s turns the assist off and the wheel freewheels. Required in beginner mode, optional (setting) otherwise. | M |
| FR-16 | **Stop button:** one press = assist off at once. Re-enabling needs a deliberate action (hold 2 s), so a bump cannot restart it. | M |
| FR-17 | **Secure pairing:** one remote bonded to one pair of skates over encrypted BLE. Others cannot command the skates. | M |
| FR-18 | **Remote cues:** vibration patterns for level change, push timing, speed cap, braking, link loss, low battery and fall (section 7b.3). Rate-limited to one cue per 2 s except safety alerts, with an adjustable intensity and an off switch. | S |
| FR-19 | **Shared state:** both skates always hold the same assist level, mode, speed cap and stop state. A change from the remote or the phone applies to both, and the skates cross-check each other. | M |
| FR-20 | **Matched assist:** left and right assist gains are equal within 10%, except for the push-driven part (each skate assists its own push). Assist is not applied while both skates are loaded and gliding, so the skater is not pulled sideways. | S |
| FR-21 | **Shared speed estimate:** each skate fuses its own wheel speed with the other's for the speed cap, regeneration and slope estimate, since the skates turn at different speeds in a curve. | S |
| FR-22 | **Time base:** the skates' clocks are aligned to within 5 ms, for stride phase analysis and for logs. | C |
| FR-23 | **Stance reference:** the skate that is on the ground (loaded, wheels rolling without slip) shares its state (ground speed, slope, gravity direction, heading rate) with the other skate. The other skate uses it while its own sensors are unreliable (in the air, swinging, or slipping during the push). | S |
| FR-24 | **Load calibration from single support:** when one skate is unloaded (recovery phase), the loaded skate's frame load equals the skater's full weight. The skates use this to correct the gain and offset of both load sensors continuously. | C |

### 4.2 Performance

| ID | Requirement |
|---|---|
| PR-1 | Assist response from the push detection to motor torque <= 50 ms. |
| PR-2 | Torque ripple and ramp such that the assist is felt as extra push, not a jerk. Torque slew limited (about 20 Nm/s at the wheel hub is a starting guess, to tune). |
| PR-3 | Pack energy >= 25 Wh per skate (Option A), 55 Wh for the belt pack (Option B). Range 1.5 hours at the design point. |
| PR-4 | Net added mass on each foot <= 300 g, with a stretch target of 250 g (section 5, weight levers). Option A with a 55 Wh total pack cannot meet this (about 460 g per skate). It would need a pack of about 15 Wh or less per skate. |
| PR-5 | Charge time <= 3 hours. |
| PR-6 | IP65 for the power pod, the motor wheel and the connectors. |
| PR-7 | Operating temperature -10 to 45 C. |
| PR-8 | Remote: button press to torque change <= 100 ms; stop button to assist off <= 100 ms (the skates also have a local stop). |
| PR-9 | Remote battery life >= 20 hours of use, charging <= 1.5 hours, mass <= 35 g. |
| PR-10 | Stance state is exchanged at about 100 Hz, as a summary of about 20 bytes (not raw IMU data), with a total delay of 60 ms or less, and timestamps aligned to 5 ms (FR-22). |

### 4.3 Beginner mode details

Speed cap 12 km/h (adjustable), assist capped at 50%, anti-rollback on, assist ramps up over 3-5 km of riding, and an automatic return to beginner level after a fall.

### 4.4 Safety

| ID | Requirement |
|---|---|
| SR-1 | The motor never produces torque unless the skater is loaded on that skate (frame load above a threshold) and a push is detected. |
| SR-2 | A fall or an impact (IMU shock above a threshold, or an abnormal attitude) cuts the torque in under 20 ms. |
| SR-3 | Loss of the sensors, the motor hall signals, the other skate's link (when needed) or the battery: assist off and freewheel. |
| SR-4 | No sudden braking: regen torque ramped, capped and cut at a full battery. Brake torque never locks the wheel. |
| SR-5 | Hardware watchdog; a motor driver with fault protection (over-current, over-temperature, short-circuit). |
| SR-6 | The battery has over-charge, over-discharge, over-current, short-circuit and temperature protection, and cell retention that survives a fall. |
| SR-7 | Option B: the cable has a breakaway connector at the skate, a current-limited output at the belt that stays dead until a skate is detected, and no cable between the legs. |
| SR-8 | The assist can always be switched off by the skater, and the skates behave as normal skates when off. |
| SR-9 | A first-use warning: helmet, wrist and knee protection. |
| SR-10 | Link loss from the remote (dead battery, range, body shadowing) always moves toward the safe state: the assist ramps to zero in about 200 ms and the wheel freewheels. The remote never commands torque by itself. It only sets limits and levels. |
| SR-11 | The remote is on a strap so that it cannot be dropped, and it is not held in the hand while skating (section 7b.1). |
| SR-12 | **Symmetric fallback:** if one skate faults, stops, falls, loses its sensors or loses its battery, the other skate turns its assist off within 100 ms (through the remote link or the skate-to-skate link). If both links are lost, each skate turns its own assist off after 0.5 s. One skate never keeps assisting alone, because a one-sided push would pull the skater sideways. |

### 4.5 Regulatory (applicability to be confirmed with a test lab)

*  Li-ion: IEC 62133-2 for cells and packs, UN 38.3 for transport.
*  Radio: FCC Part 15 (US), EU Radio Equipment Directive. A pre-certified BLE module reduces testing.
*  Skate safety: possibly EN 13843 (roller skates). Verify.
*  Rules for motorized personal devices on roads and sidewalks differ by country and city. Check before selling.

## 5. Option comparison: battery in each skate (A) vs. a belt or bag pack (B)

Same energy, 55 Wh in total, in both options.

| | A: battery in each skate | B: belt pack + cables |
|---|---|---|
| Packs | 2 x 27.8 Wh | 1 x 55 Wh |
| Mass on the feet (net, both skates) | about 915 g | about 585 g |
| Mass on the body | 0 | about 460 g (belt pack) + about 220 g (harness on the legs) |
| Total added mass | about 915 g | about 1,255 g |
| Wires on the body | none | one cable per leg, two connectors |
| Setup by the user | none | belt, two sleeves, two connectors |
| Cost, 1,000 units (estimate) | about $195 | about $234 |
| Charging | two skates, two ports | one USB-C port |
| Failure modes | a dead skate = one-sided assist | a cable breakaway = one-sided assist; snag hazard |
| Range upgrade | none (the pack is fixed in the skate) | swap in a larger belt pack |
| Regeneration | into the skate's own pack | into the belt pack, through the cable |

**Mass at the foot matters a lot, and I understated it first.** You pointed out that skaters lift their legs to move, and that a kilo on a leg is significant. I agree, and the first version of this paragraph wrongly assumed that gliding made the foot mass less important. In skating, the recovery leg is lifted and swung forward on every stride, so every gram on the foot is accelerated and lifted again.

*  Rough size (estimate): lifting the foot about 0.1 m and swinging it at about 2 m/s once per second per leg costs m x (g h + v squared / 2). For 457 g (Option A) that is about 1.4 J per stride per leg, about 2.7 W for both legs. For 292 g (Option B) it is about 0.9 J, about 1.7 W for both legs. At about 25% muscle efficiency the metabolic cost is about 4 times that: about 11 W for Option A and about 7 W for Option B. The assist is about 40 W of mechanical power, so the net is positive, but the foot mass takes back a sizeable part of it (assumed values, to measure).
*  Moment of inertia: the extra 165 g in Option A adds about 0.13 kg m2 to the leg's swing inertia (0.2 kg at about 0.8 m from the hip), roughly 10% of a leg's inertia about the hip (about 1.2 kg m2 assumed).
*  Evidence that this matters: for running shoes about 1% extra energy per 100 g on the foot is the commonly quoted figure (from memory, check), and the main complaint in reviews of Moonwalkers was weight (about 2 kg per shoe in one report, 4.2 lb per unit in another).
*  Conclusion: the foot mass budget is a primary design constraint, not a detail. Option B is recommended for that reason. Even Option B's 292 g per skate needs to come down.

**Weight levers on the foot (to reach 250 g per skate):**

*  Lighter pod: about 75 g to about 45 g (thin-wall shell, fewer fasteners).
*  Lighter motor wheel: a thinner rim, a smaller magnet set, and a motor sized for 40-50 W peak instead of 60 W.
*  Move the electronics off the skate. Only the motor driver needs to be near the motor, and the IMU and the load sensor must be on the skate. A belt-side controller would add a data cable, which I rejected in section 6.1, so this needs weighing.
*  Assist one wheel per skate, never two (already the design).
*  Do not add to the foot: no battery, no wireless charging coil, no big LEDs.

**Hybrid (Option C, later):** a small buffer pack in each skate (about 8 Wh) plus the belt pack through the cable. If the cable breaks away the skates keep working for a while, and the cable can be thin. It costs both options' parts, so it is not for v1.

## 6. System design

### 6.1 Architecture

```
 Option A                                        Option B
 +--------------------------+                    belt pack (3S2P, 55 Wh)
 | skate module             |                    BMS, 2 eFuse outputs, USB-C charger
 |  3S pack + BMS + charge  |                      |                      |
 |  controller board        |                  cable L                cable R   (outer leg, sleeve, loop at knee)
 |  motor wheel             |                      |                      |
 +--------------------------+                 magnetic breakaway     magnetic breakaway
                                                    |                      |
                                              +-----------+          +-----------+
                                              | skate L   |          | skate R   |
                                              | module    |          | module    |
                                              +-----------+          +-----------+
 Both options: each skate module = MCU + BLE, IMU, frame load sensor, 3-phase driver, hub motor wheel (hall sensors), LEDs, vibration motor.
 Skates talk to each other and to the phone over BLE. The cable (Option B) carries power only, two conductors.
```

The cable carries power only. The skates coordinate over BLE, so there is no data wire to break or pick up noise, and the cable is thinner and lighter. The skate-to-skate link is not safety critical because each skate acts independently on its own sensors (FR-11).

### 6.2 Mechanical outline (estimate)

*  Retrofit to standard inline frames (165 or 195 mm mounting, 80-90 mm wheels). One wheel (the middle or the rear) is replaced by an 85 mm gearless hub-motor wheel with hall sensors.
*  A sealed power pod bolted to the frame side holds the board and, in Option A, the pack. The pod sits low and close to the frame's centre line to keep the skate's balance.
*  Frame load sensor: strain gauges on the frame mounting plates, or force-sensing resistors under the mounts, to say how much of the skater's weight is on this skate. No wire goes into the boot. Which works better needs testing.
*  Option B: the pod has a DC input with a magnetic breakaway connector on the outer cuff side, clear of the wheels.

### 6.3 Control logic

*  **Push detection:** the load on the skate rising while the skate accelerates forward and the IMU shows the push phase (lateral push, yaw, roll pattern). Assist torque follows the push signal and fades out when the load drops.
*  **Slope estimate** (uses the stance skate's data when the skate is not the grounded one, section 6.5): the forward axis accelerometer measures g sin(slope) plus the true acceleration. Subtract the acceleration from the motor hall speed (its derivative) to get the slope, then low-pass it over a few strides.
*  **Assist torque:** torque = gain(mode, level) x push signal x slope factor, capped by the speed limit, the battery state and the temperature. Slew-rate limited.
*  **Regeneration:** above the set speed on a downhill, a ramped braking torque, limited by battery state of charge (zero regen when the pack is above 4.1 V per cell) so that the DC bus voltage cannot spike.
*  **Safety interlock:** any fault, a fall, a missing load or a lost sensor -> torque off, freewheel.
*  **Learning mode:** the assist gain starts at 30% and climbs over the first 3-5 km of riding.

### 6.4 Two-leg coordination

The two motors do not need to be synchronized like the wheels of a car: each skate is on its own foot, pushes at its own time and moves at its own speed in a turn. What does need coordination is shared state and safety.

*  **Independent torque, shared limits.** Each skate decides its own torque from its own push signal, its own load and its own IMU (6.3). The limits (level, mode, speed cap, stop) are shared (FR-19).
*  **Stop and fault propagate to both skates** (SR-12). The remote link reaches both skates directly (7b.4), and the skate-to-skate BLE link is a second path. The stop on either path is enough.
*  **Speed and slope.** The skates exchange speed and acceleration at 20-50 Hz and use the average of the two wheel speeds, weighted by load, for the speed cap and slope estimate (FR-21). In a turn the inner and outer wheels differ in speed, and a shared estimate prevents one skate from braking while the other pushes.
*  **No two-foot assist.** When both skates are loaded and the skater is gliding or standing, the assist is off on both. This also covers the case where one skate's push detection misfires (FR-20).
*  **Link timing.** BLE connection intervals of 15-30 ms give a 30-60 ms worst-case delay between the skates. That is fine for shared state and speed averaging, and not fast enough for torque coordination in the same millisecond, which the design does not need. Clock alignment to 5 ms comes from the remote's or the link's timestamps (FR-22).
*  **Mismatch checks.** The skates compare level, mode and software version at connection and refuse to assist if they differ (for example, after a firmware update that reached only one).
*  **Not covered yet:** a wired link between the skates is rejected (cable between the legs, section 7.1). If BLE latency or dropouts turn out too poor in tests, a short-range alternative (optical or capacitive coupling through the body) would need a study.

### 6.5 Stance-skate reference (cross-sensing)

The idea (yours): while one skate is on the ground its sensors give clean data that the other skate cannot get for itself. A skate in the air or swinging forward has an IMU full of leg motion and a wheel that is not rolling at ground speed. The grounded skate is a reference for the pair.

What the stance skate can supply to the other one:

*  **Ground speed.** Its wheel rolls without slip, so its hall-sensor speed is the true speed. The other skate's wheel speed is wrong while it is in the air or slipping at push-off, which matters for the speed cap and for the push detection.
*  **Slope and gravity direction.** With the wheels on the road, the accelerometer minus the wheel-speed derivative (6.3) gives a clean slope estimate. The swinging skate cannot do this. It can use the stance skate's slope and the known gravity direction to orient its own IMU.
*  **Push phase.** One skate loaded and the other unloaded identifies the single-support phase and which foot is the stance foot. The loaded skate's yaw and roll rate then tell the other skate when its push begins.
*  **Relative leg motion.** The difference between the two IMU orientations gives the angle between the feet while one is grounded, a cue for stride width and push angle (for the technique cues, section 7b.3).
*  **Load calibration.** During single support the loaded skate carries the skater's whole weight, a known reference for correcting the other load sensor's gain and drift (FR-24). Strain gauges drift with temperature, so continuous calibration is useful.
*  **Fault cross-check.** If the stance skate reports speed 0 while the other reports fast motion (or the opposite), one of them has a sensor fault, and the assist goes off (SR-12).

Limits and cautions:

*  **Skate orientation is not body orientation.** In a V-shaped push the skates point in different directions, so heading and lean from one skate are not the skater's. Share quantities that do not depend on the foot angle (speed, slope, weight) and be careful with heading and roll.
*  **Delay.** The stance data arrives 30-60 ms late over BLE. For a push of 300-500 ms that is acceptable for speed, slope and calibration, and too slow for fast torque decisions, which stay local (6.4).
*  **Two-foot glide:** both skates are references, and the pair averages them (FR-21).
*  **Which skate is the stance skate** is decided by the load: each skate shares its load fraction, and the one carrying more than about 70% of the weight is the reference. This needs the calibration above, so a first-use calibration standing on both feet is part of setup.
*  **Data volume is small.** About 20 bytes at 100 Hz is 2 kB/s, well within BLE (PR-10).

### 6.6 Motor wheel options: one big wheel, or two or three small ones

Question: instead of one 85 mm motor wheel, use two or three small motor wheels, or adapt a large skate wheel? Findings from the web search and my own scaling. Listing figures come from sellers and mix rated and peak power, so treat them as indicative.

**What the market gives**

*  **Skateboard hub motors exist at 70-90 mm but are far too heavy and powerful.** OrangeRed 5230SD 83 mm: 350 W rated, 4.2 Nm max, 815 g. OrangeRed 4230SD 70 mm: 150 W, 575 g. An MP 83 mm hub: listed 8 Nm, 0.9 kg, 1.5 kW rated. Maytech 90 x 55 mm: 1,000 W max, 1,000 g, 24-36 V. [OrangeRed (Hobbywing)](https://www.hobbywing.com/en/products/orangered-skateboard-motor156), [MP 83 mm](https://reach.dog/shop/dongguan-freerchobby-coltd/products/mp-83mm-hub-motor-8nm-torque-for-electric-skateboard), [Maytech 90 mm](https://reach.dog/shop/michobbycom/products/mto9055rh-60-ha-maytech-90mm-60kv-hub-motor-1000w)
*  **Skate wheels are narrow.** A skateboard hub motor is about 55 mm wide (Maytech), while an inline skate wheel is about 24-30 mm wide (my knowledge, to verify), so a skate hub motor has about half the active length, and torque scales roughly with diameter squared times length.
*  **I found no 80-100 mm gearless hub motor at 12-24 V with a published torque and mass.** The closest listings were a 5.5 inch (larger) 24 V hub at 3.2 Nm and 2.0 kg, a geared 24 V AMR wheel module, and the CubeMars R80 outrunner (87 mm, 4 Nm, 354 g, but 48 V). A custom motor wheel is still needed. [CubeMars R80](https://store.cubemars.com/products/r80)
*  **Atmos Gear (the closest product) uses one motor, in the middle wheel, with a 110 mm wheel.** Rated 18 mph and 16 miles. The battery is a separate pack worn in a bag, because the company says an earlier prototype with the battery inside the skates weighed far too much (it cites about 7 kg at the feet). Their stated added weight is about 700 g (1.5 lb) over conventional skates. The page is ambiguous whether that is per pair or per frame. [Atmos Gear store](https://www.atmosgear.com/store/p/rollers)

Atmos Gear's choice of a belt-style pack matches the Option B recommendation from your weight argument. If the 700 g is per pair (about 350 g per skate), it is close to my estimate of about 290 g per skate, with a different design. If it is per frame, their skates are much heavier than mine.

**Required torque is small (estimate).** At 5 m/s, 20-30 W of mechanical assist per skate is about 4-6 N at the road. At the wheel that is 0.17-0.26 Nm for an 85 mm wheel and 0.22-0.33 Nm for 110 mm. Hill and start peaks of 2-3 times that, so about 0.5-1 Nm peak. The skateboard motors' 4-8 Nm is several times too much. Their mass is the problem, because they are built for 150-1,000 W.

**Mass scaling (estimate).** The listed motors give 0.26 W/g (150 W, 575 g), 0.43 W/g (350 W, 815 g) and 1 W/g (1,000 W, 1,000 g). At 60 W per skate that gives 60-230 g of motor depending on how hard it is driven, so my 260 g motor wheel assumption (including the wheel and bearings) is plausible, and not conservative if heat is a problem.

**Options compared**

| Option | Torque (relative to one 85 mm wheel) | For | Against |
|---|---|---|---|
| One 85 mm motor wheel (current spec) | 1.0 | simple, one driver per skate | torque limited by the narrow width, custom motor |
| **One 110 mm motor wheel** (Atmos Gear approach) | about 1.7 (diameter squared) | validated by a product, bigger wheel rolls better, more rotor volume, 3x110 and 4x110 frames common | wheel and frame heavier, 195 mm frames only for the longer sets |
| One 125 mm motor wheel | about 2.2 | most torque and rollover, 3x125 frames take 165 and 195 mm mounts | heaviest wheel, large wheel changes the feel and turning |
| Two 85 mm motor wheels per skate | about 2.0 | torque shared, more heat surface, each motor half the mass, a redundancy, weight spread along the frame | two drivers, two sets of halls, 2x the motor parts and cost, more cables |
| Three small motor wheels per skate | about 3.0 | most torque, each motor very light | most cost and complexity, little benefit if one 110 mm wheel is enough |

*  **Two or three small motor wheels help where torque is the limit.** They add motor length (the skate wheel is narrow), spread the heat and let each motor be small. They do not reduce the total motor mass for the same total torque, and they add bearings, axles, halls and driver channels. The electronics cost is small (a driver chip is about $3), the mechanical cost is not.
*  **Sharing one driver between two wheels** is possible in principle, since both wheels on one frame turn at the same speed, but the rotor positions are not locked, so I would use one driver per motor.
*  **Recommendation:** v1 = one 110 mm motor wheel in the middle of a 3x110 frame (the Atmos Gear layout), because the diameter squared gives about 1.7 times the torque of 85 mm for no extra parts. Keep two motor wheels per skate as the fallback if the thin motor lacks torque or overheats in tests.

**Large wheels and frames I could adapt**

*  Freeskate frames usually take 80-110 mm wheels, longer frames take 100-125 mm. [SkatePro frames](https://skatepro.com/c142.htm)
*  195 mm mounting came with 100-110 mm wheels because the longer base lowers the centre of gravity. [Powerslide on 195 mounting](https://powerslide.com/blogs/technologies/195-mounting), 165 mm is still used, for example the Powerslide Megacruiser 125 range. [Rollerenligne on 165 mm](https://www.rollerenligne.com/en/materiel/is-2015-the-comeback-year-of-165-mm-mounting/)
*  Frames to look at: Powerslide Core X-perience 11.8 inch, 3x125 mm, 165/195 mm. Powerslide racing 195 frames in 3x110 and 4x110. Bont 110 mm x 3 frame. Endless 110/125 frames. [Powerslide Core X-perience](https://powerslide.com/products/core-x-perience-11-8-3x125-195-165), [Powerslide racing 195](https://b2b.powerslide.com/collections/powerslide-racing-195-frames), [Bont 3x110](https://korea.bont.com/products/110mm-x-3-wheel-inline-skate-frame), [Endless 110/125](https://locoskates.com/products/endless-110-125-frames-silver), [Powerslide frames](https://powerslide.com/collections/inline-skate-frames?page=9)
*  The boot and frame must match the mounting spacing (165 or 195 mm), and each frame lists its maximum wheel size. Axle and bearing standard (I believe 608 bearings and an 8 mm axle, to verify on the chosen frame).
*  Wheel speed at 5 m/s: about 1,120 rpm for 85 mm, about 870 rpm for 110 mm, about 760 rpm for 125 mm, so a bigger wheel also means a slower, easier motor to drive.

## 7. Wiring for Option B (battery on a belt or in a bag)

You asked how the wiring works if the battery is not in the skate, and whether to pin the wire to a leg with strips. Short answer: no pins and no adhesive strips. Use a sleeve or straps, and design the cable so that it can let go safely.

### 7.1 Routing

*  One cable per skate. Each cable stays on its own leg: belt (hip), outer side of the thigh, outer side of the knee, outer side of the shin, ankle, skate port on the outer cuff.
*  **Never run a cable between the legs or from one skate to the other.** Skaters cross their feet in turns, and a cable between the ankles is a trip hazard.
*  The knee joint axis runs roughly side to side, so a cable on the outer side near that axis changes length the least when the knee bends. Add a coiled slack loop of about 5 cm at the knee for the rest.
*  Cable length from hip to ankle about 1.2 m including slack for an adult (estimate; measure for a size range).

### 7.2 Attachment

*  A thin elastic leg sleeve per leg (compression-sock style) with a sewn channel for the cable, or three hook-and-loop straps (above the knee, below the knee, at the ankle). The cable is held loosely in loops, not clamped, so it can slide.
*  Not adhesive tape or strips on the skin or on clothing (they pull on hair and skin, they peel in sweat, and you cannot remove them quickly), and not pins.
*  The sleeve also keeps the cable away from the wheels, at least 15 cm of clearance.

### 7.3 Connectors and protection

*  A magnetic breakaway connector at the skate, with a pull-off force chosen to hold in normal use and release before the cable is dragged or tripped over (start at 15-30 N and test). The belt end is a locking connector.
*  Each belt output has an eFuse with a current limit. It stays off until a skate is detected by a small pilot current, so a pulled-out connector is not live.
*  A bulk capacitor (100-220 uF, low ESR) and a TVS diode at each skate input to absorb regen spikes and cable inductance.
*  Strain relief at both ends. Silicone cable with 20 AWG conductors.

### 7.4 Electrical numbers (estimate)

20 AWG copper is 33 mOhm/m, and a 1.3 m cable pair has about 87 mOhm of loop resistance.

| Condition | Current | Voltage drop | Loss |
|---|---|---|---|
| 60 W per skate at 11.1 V | 5.4 A | 0.47 V (4%) | 2.5 W |
| 60 W per skate at a sagging 9 V | 6.7 A | 0.58 V | 3.9 W |

At 12 V and 100 W the loss would be about 5.5 W (20 AWG), so the design keeps the per-skate peak at 60 W. A 6S belt pack (24 V) would halve the loss but needs a different motor, so I kept 3S to reuse the same skate module.

### 7.5 A bag instead of a belt

A backpack puts the pack higher, so the cable must reach the hip anyway, adding 0.3-0.4 m. It only works well if the bag has a hip belt that carries the cables to the hip, which makes it a belt pack. A loose bag swings and pulls on the cables. Recommendation: belt pouch, not a bag.

## 7b. Wrist remote with vibration cues

### 7b.1 Form factor

You suggested a remote held in the hand. I recommend a wrist-worn remote instead, for these reasons (engineering reasoning, to confirm in a trial):

| Form | For | Against |
|---|---|---|
| Hand-held fob | easy to press | arms swing and balance a skater, a held object is dropped or lands in a fall, and wrist guards do not protect a held hard object |
| **Wrist band (recommended)** | cannot be dropped, no hand is used, works with a wrist guard (strap or clip on the guard), a vibration motor on the wrist is easy to feel | buttons must be big enough to press with a glove, from the other hand |
| Ring or glove button | very discreet | tiny battery, weak vibration, hard to charge |
| Smartwatch + phone app | no new hardware, a fast prototype | extra latency, depends on the phone, a watch is not a dead-man link |

The cue channel is also better on the wrist than in the skate: the wheels shake the frame and the boot constantly on rough pavement, which would mask vibration cues there (reasoning, not measured).

### 7b.2 Controls

*  Two rocker buttons: assist level up and down.
*  One mode button: normal, beginner, and the like.
*  One large stop button, pressed with the palm or the thumb, with a raised rim so it is not hit by accident. A press cuts the assist, and holding it for 2 seconds re-enables it.
*  A status LED (colour: connected, assist on, stopped, low battery).
*  No grip sensor is needed on a wrist band. The dead-man function comes from the link (FR-15) and from the remote's accelerometer, which also detects a fall.

### 7b.3 Vibration cues (starting set, to tune with skaters)

| Cue | Pattern |
|---|---|
| Level change confirmed | N short pulses for level N (up to 5) |
| Assist stopped (stop button) | one long pulse |
| Push timing (learning mode) | one soft tick at the start of the ideal push, only when the stride is slow |
| Speed cap reached | two short pulses |
| Regenerative braking active | a short low buzz at the start |
| Link lost / assist off | three long pulses (sent by the remote when it detects the loss itself, and by the skates when they can) |
| Skate battery low | two long pulses |
| Fall / impact, assist cut | one strong 1-second buzz |

### 7b.4 Link design

*  The remote keeps a BLE link to **both** skates (it is the central and the skates are peripherals), so one skate failing does not cut the control of the other. The skates also keep their own link to each other for coordination (FR-11).
*  Connection interval 15-30 ms, 1M PHY (longer range than 2M), supervision timeout 500 ms, transmit power set high enough for the wrist-to-ankle path. A body absorbs 2.4 GHz, so test for dropouts when an arm is behind the torso.
*  The remote sends a heartbeat. The skates treat a missing heartbeat as link loss (SR-10). Link loss ramps the assist down, so a single dropped packet does not jerk the skate.
*  Remote messages only set the level, the mode and the stop. They are authenticated (bonded, encrypted link) and a replayed command is rejected.
*  Remote battery dead: the skates go to assist off. This is the safe direction, but it will annoy a skater halfway through a ride, so the remote warns at 20% and 10%, and the phone app can take over level control without the dead-man function as a fallback if the skater turns that setting on.

## 8. Rough electronics board (skate module)

### 8.1 Target

One board per skate, about 50 x 28 mm, 4 layers, in the sealed pod. Option B adds a separate belt board, about 60 x 35 mm.

### 8.2 Block list and candidate parts, skate module

| Block | Candidate | Notes |
|---|---|---|
| MCU + BLE | STM32WB5MMG module class (Cortex-M4 + BLE radio, certified module) | one chip for motor control timers and BLE. A separate BLE module plus a motor MCU is the alternative |
| IMU | ICM-42688-P or BMI270 | SPI |
| Frame load sensing | 24-bit bridge ADC (NAU7802 class), 2 strain gauges or FSRs | I2C |
| Motor driver | DRV8316 class (3-phase, integrated MOSFETs, current sense, 8 A peak, up to about 35 V) | check supply range and current at the pack's minimum voltage |
| Motor feedback | 3 hall sensors in the hub motor | commutation at low speed |
| 3.3 V supply | low-Iq buck (TPS62840 class) | |
| Input protection | reverse-polarity MOSFET, TVS, bulk capacitor | |
| Option A only: BMS and charger | 3S protection IC + charge controller, charge connector (magnetic pogo or sealed USB-C) | regen needs the charge path to accept up to 3 A |
| Cue outputs | LED strip (2-4 LEDs), vibration motor + MOSFET | |
| Misc | NTC for the motor and the pack, push button, battery voltage divider | |

### 8.3 Belt board (Option B only)

| Block | Candidate |
|---|---|
| Pack | 3S2P 18650 cells, protection IC, balancing |
| Outputs | 2 x eFuse / load switch with current limit and a pilot-current skate detection (TPS25947 class) |
| Charger | 3S charger with USB-C input (BQ25798 class, to check) |
| MCU | small BLE MCU for handshake, status LED and pack state (nRF52832 class) |
| Connector | 2 x locking output connector to the cables |

### 8.4 Power tree

```
Option A:  3S pack (9-12.6 V) -> BMS -> reverse protect/TVS/bulk cap -> motor rail -> DRV8316
                                                                    -> buck 3.3 V -> MCU, IMU, ADC, LEDs
Option B:  belt pack -> eFuse -> cable -> breakaway -> reverse protect/TVS/bulk cap -> (same as above)
```

### 8.5 MCU pin plan, skate module (rough)

| Function | Pins |
|---|---|
| Driver PWM (3 phases) + enable + fault | 5 |
| Driver SPI configuration | 4 |
| Driver current-sense outputs (3 ADC) | 3 |
| Hall inputs | 3 |
| IMU SPI + interrupt | 5 |
| Load ADC I2C + data-ready | 3 |
| LEDs, vibration, button | 3 |
| Pack voltage, NTC x2 ADC | 3 |
| Charger status / BMS I2C (Option A) | 3 |
| Debug SWD | 2 |
| Spare | 4 |

About 38 pins, within the 48 GPIO of the candidate module family.

### 8.6 Layout notes

*  The BLE antenna end at the board edge with the module's keep-out, away from the motor wires and the aluminium frame. A plastic pod cover helps.
*  IMU near the centre of the board, away from the driver and the buck inductor, rigidly mounted. The road vibration is large, so filter in firmware.
*  The driver, bulk capacitor and motor connector together with short, wide traces and a solid ground area. Motor phase wires away from the hall and ADC lines.
*  Conformal coating plus a gasketed pod. Test points on all rails.

### 8.7 Firmware outline

Motor control (sensored trapezoidal first, field-oriented control later), push and slope estimators, the assist and regen controller, safety supervisor, BLE (skate-to-skate and phone), cue generator, logging and signed firmware update. 1 kHz control loop for the torque, 100-200 Hz for the estimators.

### 8.8 Remote board (wrist remote)

One small board, about 35 x 20 mm, 2 to 4 layers, in a sealed housing on a strap.

| Block | Candidate | Notes |
|---|---|---|
| MCU + BLE | nRF52832 or nRF52840 certified module (MDBT42Q class) | two connections (both skates) at 15-30 ms |
| Haptic | LRA (8 mm coin type) + DRV2605L class driver | I2C, built-in waveform library, so the patterns in 7b.3 are easy to build. An ERM motor + MOSFET is cheaper but less precise |
| Accelerometer | LIS2DW12 class, low power | wake on motion, fall and impact detection, gesture |
| Buttons | 4 domes with a rubber overlay, one large stop button | large, glove-friendly |
| Status LED | one RGB LED | |
| Battery and charging | 120 mAh LiPo + charger IC (MCP73831 class) + protection | USB-C or a magnetic pogo connector with a seal |
| 3.3 V | low-Iq LDO or buck | |

Power budget (estimate): BLE with two connections at about 20 ms, about 0.3 mA average; sleep and accelerometer about 0.02 mA; haptic bursts at about 70 mA for about 2% of the time, about 1.4 mA. Total about 1.7 mA, so about 70 hours on 120 mAh and about 50 hours with a 30% derating, well above the 20-hour target.

## 9. Bill of materials and weight (estimate)

Volume 1,000 kits (two skates). Prices are typical distributor or Asian OEM prices, not quotes, and the error is about +/- 30%. Masses are gross unless marked net.

### 9.1 Per skate, common to both options

| Item | Cost (USD) | Mass (g) |
|---|---|---|
| 85 mm gearless hub-motor wheel with halls (replaces a 75 g wheel) | 25.0 | 260 |
| MCU module (STM32WB class) | 12.0 | 2 |
| IMU | 3.5 | 0.1 |
| Load ADC + strain gauges | 4.5 | 3 |
| Motor driver | 3.0 | 0.1 |
| Buck, input protection, bulk cap | 3.5 | 3 |
| LEDs, vibration motor, button | 3.0 | 6 |
| Connectors, passives | 6.0 | 4 |
| PCB, 4 layer, assembled | 8.0 | 4 |
| Sealed pod + gasket + mounting hardware | 10.0 | 75 |
| **Subtotal per skate** | **~78** | **~357 gross, ~282 net of the replaced wheel** |

### 9.2 Option A additions (per skate)

| Item | Cost (USD) | Mass (g) |
|---|---|---|
| 3 x 18650 cells (about 2.5 Ah) | 7.5 | 138 |
| 3S BMS + charge controller | 4.0 | 4 |
| Cell holder, tabs, case share | 3.0 | 25 |
| Charge connector with seal | 3.0 | 8 |
| **Subtotal** | **~17.5** | **~175** |

Total Option A: 2 x (78 + 17.5) = about $191, plus packaging and manual about $5, **about $195**. Mass net on the feet: 2 x (282 + 175) = **about 915 g**.

### 9.3 Option B additions

| Item | Cost (USD) | Mass (g) |
|---|---|---|
| Skate-side breakaway connector (2) | 6.0 | 20 |
| Belt pack: 6 cells (3S2P) | 15.0 | 276 |
| Belt board: protection, 2 eFuses, charger, MCU | 20.0 | 35 |
| Belt case and belt | 12.0 | 150 |
| Cables, 2 x 1.3 m, silicone 20 AWG, with connectors | 10.0 | 70 |
| Leg sleeves, 2 | 10.0 | 140 |
| **Subtotal** | **~73** | **~690** |

Total Option B: 2 x 78 + 73 = about $229, plus packaging and manual about $5, **about $234**. Mass: skates net 2 x 282 + 20 = about 585 g, body-worn about 670 g, total about 1,255 g.

### 9.4 Wrist remote (add to either option)

| Item | Cost (USD) | Mass (g) |
|---|---|---|
| nRF52 module | 4.5 | 1 |
| LRA + haptic driver | 3.0 | 2 |
| Accelerometer | 1.0 | 0.1 |
| Buttons, rubber overlay | 2.0 | 3 |
| RGB LED, passives | 1.8 | 1 |
| 120 mAh LiPo + charger + protection | 2.9 | 4 |
| Charge connector (USB-C or magnetic) | 1.0 | 2 |
| PCB, assembled | 2.5 | 2 |
| Sealed housing | 3.0 | 10 |
| Wrist strap | 1.5 | 10 |
| Packaging | 1.0 | n/a |
| **Total** | **~24** | **~35** |

With the remote: Option A about $219, Option B about $258. The remote adds about 35 g (on the wrist, so no swing-inertia problem at the foot). At 2.2-2.5 times the BOM the retail guess rises by about $55-60.

*  **Retail guess:** at 2.2-2.5 times the BOM, about $430-490 for Option A and $515-585 for Option B.
*  **Foot mass versus the old idea.** The earlier text in the skates file assumed about 300 g added per boot. Option B meets that (about 290 g per skate net). Option A does not (about 460 g per skate net) and would need a pack of about 15 Wh per skate or less.
*  Mass is dominated by the cells and the motor wheel, not by the electronics (about 20 g of board per skate).
*  Not in the BOM: tooling, certification (battery, radio, skate safety), app development, and a custom hub-motor wheel (the 85 mm, 60 W gearless motor probably needs a custom design, which is a large one-time cost and a supply risk).

## 10. Risks and open questions

1. **Motor wheel.** A gearless hub motor at 85-125 mm and 12-24 V in a skate-wheel width, with enough torque at 60 W, probably does not exist off the shelf (section 6.6). A geared motor is heavier and noisier. This is the biggest technical risk. A 110 mm wheel (the Atmos Gear layout) or two motor wheels per skate are the ways to relieve it.
2. **Weight on the foot.** About 290 g net per skate in Option B and about 460 g in Option A. Skaters lift and swing the leg every stride, so even Option B is significant and needs a trial with skaters. Target 250 g.
3. **Cogging and drag.** A hub motor drags when unpowered (cogging and iron loss), so the skates may be slower than normal skates with the assist off. Needs measuring.
4. **Push detection.** Distinguishing a push from a glide or a bump with an IMU and a frame load sensor is untested.
5. **Frame load sensor** on the skate frame: strain gauges on a mounting plate, or force-sensing resistors, are unproven for durability.
6. **Falls and liability.** Motors on skates, children and beginners. Insurance and certification costs are likely high.
7. **Waterproofing and shock.** Cells and connectors in a pod that gets hit by rain, puddles and impacts.
8. **Option B wiring** needs usability tests (donning time, snagging, breakaway force).
9. **Remote link.** The 2.4 GHz link between the wrist and the ankles is blocked by the body, so dropouts are likely when an arm is behind the torso. Too many dropouts will turn the dead-man feature into a nuisance. Needs measuring on real skaters.
10. **Cue effectiveness.** Whether a wrist vibration cue is noticed and understood at speed, and whether it improves technique, is untested. Pattern design needs a trial.
11. **Competition.** Moonwalkers already adapt power to gait. The room for differentiation is the learning mode, the cues and the price.

## 11. Next steps

*  Log IMU, load and speed data on normal skates on hills to test push detection and the slope estimate.
*  Build a prototype on a standard frame with an off-the-shelf BLDC hub motor and a dev board (STM32 nucleo with a driver board, IMU breakout) to check the control loop and the feel.
*  Measure the foot-mass penalty with dummy weights (160, 330 and 460 g) on skaters.
*  Bench-test the belt cable: voltage drop, breakaway force, routing in a sleeve while skating.
*  Source or design the 85 mm hub-motor wheel.
*  Prototype the remote first as a smartwatch or phone app with haptics, then as the wrist board, and measure link dropouts and cue recognition on skaters.
*  Reuse the controller board for the bicycle kit and the fall-prevention shoes.
