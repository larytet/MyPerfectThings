# VR team

Products that could leverage a shared, multi-user VR space. Started from a VR arena idea (team-vs-team shooter, 4+ players, low-cost standalone headsets, two hand controllers) and widened to where the money actually is: enterprise and institutional training.

Status: research notes, November 2026. Figures come from web searches. Many are vendor claims or paid market-research estimates and are marked as such. Nothing here is verified by a primary source unless stated.

## 1. Core idea

One technology stack, several buyers:

- Shared physical space tracked in one coordinate system (inside-out tracking plus shared spatial anchors).
- 4+ players, standalone headsets, no cable, streamed or on-device rendering.
- A game master / instructor console, session timing, leaderboards, debrief and replay.
- Content is the product. The same engine serves a game for venues and a drill for a training customer.

The arena game is the cheapest to prove and the lowest paying. Enterprise training pays more per seat and per contract, but sales cycles are longer.

## 2. Where the money is

| Segment | Buyer | Why it pays | Evidence quality |
|---|---|---|---|
| Industrial and construction safety | Contractors, plant operators, insurers | Injuries and downtime are expensive; compliance is mandatory | Small studies, vendor claims |
| Frontline onboarding | Retail, logistics, food service | Large headcount and high turnover; training time cut from hours to minutes | Vendor case studies |
| Driver and operator training | Fleets, emergency services, driving schools | Simulator hours replace costly vehicle hours and crashes | Vendor claims, trade press |
| Healthcare and surgical training | Hospitals, device makers | Practice without patients; device companies pay for training content | RCTs, but small and vendor-funded |
| First responders and tactical | Police, fire, military | Multi-person team drills are hard and costly in real life | Vendor claims |
| Education | Schools, universities | Large budgets, but price-sensitive and hardware-led | Weak outcome evidence |
| Venue entertainment (the original idea) | Arenas, FECs, laser tag | Per-session revenue of roughly $27–50 per player | Operator price lists, one chain owner's account, see section 6 |

## 3. Market size (treat as rough)

Estimates disagree because the scope differs (enterprise-only, VR-only or AR+VR, hardware included or not).

- VR corporate training: USD 14.0B (2025), 16.6B (2026), 41.1B (2031), per Mordor via Research and Markets. Another publisher gives USD 8.6B (2025). A third gives USD 7.6B (2025) rising to over 33B early next decade.
- AR/VR training overall: about USD 25.3B (2025) per Market.us, with the enterprise XR sub-segment at about 4.6B.
- Dataintelo: corporate training held the largest share (32.4%) in 2025.
- VR in education: USD 6.2B (2025) per IMARC, versus about 24B (2026) per Fortune Business Insights. Hardware is about 61% of it.
- No source gave dollar figures for construction or safety alone.

Links:
- [Mordor / Research and Markets: VR corporate training](https://www.researchandmarkets.com/reports/6247201/virtual-reality-vr-corporate-training-market)
- [Market.us: AR and VR training](https://market.us/report/ar-and-vr-training-market)
- [Dataintelo: XR training](https://dataintelo.com/report/extended-reality-training-market)
- [Customer Times: enterprise VR training](https://www.customertimes.com/enterprise-vr-training-industrial-metaverse)
- [IMARC: VR in education](https://www.imarcgroup.com/report/en/virtual-reality-in-education-market)
- [vr.org: enterprise VR training ROI](https://vr.org/articles/enterprise-vr-training-219-percent-roi) (the 219% figure traces to a Forrester study commissioned by Meta, per another vendor blog; treat as marketing)

## 4. Product list

### 4.1 Games and venue entertainment
- Team-vs-team 4v4 objective shooter for free-roam arenas. Reference: Zero Latency Sol Raiders (details below).
- Kids and non-gun variants (sci-fi, sports, capture-the-orb). Teleports and spatial distortion make a small room feel large.
- Corporate team-building and birthday packages sold through venues.
- Customers: independent free-roam arenas, family entertainment centers, laser tag operators. Zero Latency (about 150 venues) and Sandbox VR (about 90) run their own content and are not customers.
- Channel: turnkey platforms that may accept third-party games, see section 6.

### 4.2 Industrial onboarding and job training
- Plant and site induction, lock-out/tag-out, hazard walk-throughs, machine and process familiarization.
- Procedures practiced before the first shift. Team versions: shift handover, emergency shutdown, multi-person tasks.
- Soft-skills variants: customer service, difficult conversations, supervisors.

### 4.3 Construction safety
- Hazard recognition on a virtual site (electrical cables, edges, falls, heavy machinery, excavation).
- Team scenarios: crane and signaller communication, evacuation drills, near-miss replay.
- Evidence: see section 5.

### 4.4 Driving courses
- Commercial and fleet driver training: braking distance, emergency lane change, stability, skid recovery, adverse weather.
- Emergency vehicles: police interceptor and fire pumper scenarios.
- Distracted-driving awareness for learner drivers and fleet compliance.

### 4.5 Extreme driving courses
- Skid control, evasive and pursuit driving, off-road and winter handling, track-day preparation.
- I found no dedicated "extreme driving" VR product. The closest are the fleet road-course and braking scenarios above, so this looks like a gap, possibly because motion cues are hard to fake without a motion platform.

### 4.6 Healthcare
- Surgical and orthopaedic procedure practice (Osso VR).
- Nursing simulation (UbiSim), emergency team drills, patient handover, de-escalation, mental-health and phobia therapy, rehabilitation games.
- Device-maker training modules paid for by manufacturers.

### 4.7 Education
- Science labs, STEM, history, vocational training (Prisms VR, Transfr, Labster, ClassVR, VictoryXR).
- Price-sensitive and slow to buy. Better as a vocational and technical-training play than as K-12 classroom headsets.

### 4.8 First responders, security and military (strongest fit for the multi-user idea)
- Team drills for police, fire and security with full-body avatars, voice comms and an instructor console. Free-roam, up to about 12 users claimed by one vendor.
- De-escalation and use-of-force decisions, building entry, active-incident and evacuation drills.

### 4.9 Other ideas (not researched yet)
- Mining, oil and gas, utilities and lineman work, hazmat, confined-space entry.
- Forklift and warehouse operations, crane and excavator operation.
- Aviation and maintenance procedures, assembly and quality inspection.
- Public-venue evacuation and crowd-safety planning, event staff training.
- Sports and tactical team training, fitness games.
- Architecture and design review with several people in one shared model.

## 5. Evidence and briefs

### Construction safety
- A 2022 ICCEPM study found a statistically significant knowledge gain in hazard recognition for VR over conventional training. A 2022 *Buildings* study on heavy-machinery operators found headsets improved identification of critical hazards such as electric cables. An AERA 2026 poster reports a Bayesian meta-analysis with 10–18% improvement in hazard recognition and safety behaviour (abstract only, method unverified).
- I found no study showing measured injury reduction or cost savings. Vendor claims (for example "30% more safety awareness in a 200-worker study") were not verified against the papers.
- Links: [Buildings 2022 (DOAJ)](https://doaj.org/article/fa6f8d2118ef4ebdb74a5f7542d05422), [ASCE: VR safety training for construction](https://ascelibrary.com/doi/10.1061/9780784485231.009), [Warp VR: VR safety training (vendor)](https://www.warpvr.com/blog/vr-safety-training-workplace-incidents), [US DOT repository report](https://rosap.ntl.bts.gov/view/dot/61777/dot_61777_DS1.pdf)

### Frontline onboarding (Strivr and Walmart)
- Strivr claims Walmart cut Pickup Tower training from 8 hours to 15 minutes, rolled out to over 2.2 million associates in 4,700 locations. A Strivr blog also claims VR-trained staff performed "16x" better in A/B tests. Both are vendor claims with no independent source. Another Strivr case says Sprouts cut onboarding from 4 hours to 45 minutes.
- Walmart reportedly bought 17,000 Oculus Go headsets in 2018. Strivr has raised roughly $87.5M in total per one profile, and has shifted focus towards AI-driven frontline guidance.
- Links: [ARtillery case study (July 2026)](https://arinsider.co/2026/07/28/case-study-walmart-streamlines-training-with-vr/), [Strivr: Walmart](https://www.strivr.com/customers/walmart), [TechTarget: Walmart, FedEx make the case for VR training](https://www.techtarget.com/enterprise-software/news/252472139/Walmart-FedEx-make-case-for-VR-training), [Josh Bersin analysis](https://joshbersin.com/2022/04/virtual-reality-has-now-gone-mainstream-for-corporate-training/), [VentureBeat: Strivr $35M](https://venturebeat.com/2022/04/19/enterprise-vr-training-company-strivr-raises-35m-to-help-reskill-the-workforce/)

### Driving
- VR Motion RealDrive: truck, box truck, police SUV and fire pumper, car control, road course, braking challenge. Datasheet lists $16,000 one-time or $2,000 per month with a 6-month minimum (check if current).
- ITI VR Driver Safety Simulator: braking distance, emergency lane change, vehicle stability, sedan to 53 ft tractor-trailer combinations.
- Trade press: one simulator hour can replace about four behind-the-wheel hours (one fleet trainer's experience).
- Links: [VR Motion RealDrive datasheet](https://vrmotioncorp.com/wp-content/uploads/RealDrive_Product-Datasheet.pdf), [VR Motion solutions](https://vrmotioncorp.com/solutions), [ITI VR Driver Safety Simulator](https://www.iti.com/en/help/vr-driver-safety-simulator), [FleetOwner: navigating the virtual road](https://www.fleetowner.com/technology/article/21683887/navigating-the-virtual-road), [Trucking Technology: driver training](https://ttnews.com/articles/driver-training-technology-creates-virtual-reality)

### Healthcare
- UCLA randomized trial (20 participants, tibial nailing): VR-trained group finished faster and completed more steps correctly. Reported effect sizes vary by source (230% by the CEO, 130% in another source), and the study was funded by Osso VR.
- University of Illinois Chicago randomized, blinded study (published in *Clinical Orthopaedics and Related Research*): VR training increased procedural accuracy and completion in medical students.
- Osso VR said (2019) more than 20 teaching hospitals and 8 device companies in 11 countries use it. Device partnerships include MicroPort modules.
- Links: [MDDI: Osso VR study results](https://www.mddionline.com/augmented-virtual-reality/osso-vr-expands-its-reach-shares-study-results), [MDDI: does VR training improve surgical proficiency](https://www.mddionline.com/augmented-virtual-reality/does-vr-training-really-improve-surgical-proficiency-), [Osso VR clinical compendium](https://essentialhospitals.org/wp-content/uploads/2025/10/OSSOVR-25_Clinical-Compendium.pdf)

### Education
- ClassVR claims 2 million+ students in 250,000 classrooms across 90 countries (company-reported, 2025). Labster has 300+ simulations, mostly browser-based, plus UbiSim for nursing.
- I found no independent learning-outcome evidence and no clean K-12 versus higher-ed split.
- Links: [ClassVR: VR for STEM](https://www.classvr.com/us/vr-for-stem/), [ClassVR headsets](https://www.classvr.com/vr-headsets/), [Reality Atlas: VR in education guide](https://www.reality-atlas.com/blog/vr-in-education-guide), [Reality Atlas: best K-12 VR companies 2026](https://www.reality-atlas.com/de/blog/beste-vr-unternehmen-k12-bildung-2026)

### First responders and tactical multi-user training
- V-Armed: free-roam, multi-person, full-body tracking, lethal and non-lethal force options for law enforcement, military and first responders. OptiTrack case study says each participant has their own headset and PC.
- Sentinel (OP-2): permanent installs at bases and academies, up to 12 simultaneous free-roam users (vendor claim).
- InVeris SVR 3.0: multi-user scenarios for military police and security forces. Wrap Reality: public-safety de-escalation and use-of-force simulator.
- Academic note (Braun et al., 2022, firefighter training): standard SDK applications lack the combination of multi-user team training and full-body avatars for all participants.
- Links: [OptiTrack: V-Armed case study](https://optitrack.com/news/how-optitrack-enables-v-armeds-large-scale-immersive-simulations), [Sentinel OP-2](https://lynx-panda-765p.squarespace.com/op-2-heavy), [InVeris SVR 3.0 datasheet](https://wehrtechnik.info/wp-content/uploads/2023/02/InVeris-SVR-3.0-Datasheet-Militaer.pdf), [Multi-user firefighter training paper (CAS catalogue)](https://katalog.lib.cas.cz/KNAV/EdsRecord/edsdoj,edsdoj.923e23e0db03409d9f0289b2d72ee0cf), [Law-enforcement VR patent](https://patents.justia.com/patent/11887507), [EPO patent application on free-roaming law-enforcement VR](https://data.epo.org/publication-server/rest/v1.2/patents/EP3984611NWA2/document.html)

## 6. Venue entertainment research (original idea)

### Market
- Location-based VR overall: about USD 1.9B globally in 2025 per Mordor, with other publishers up to 4.8B. One report gives a US figure of about 950M for all location-based VR. In JLL's 2026 tenant study, only 83 of 4,746 location-based entertainment sites were VR venues. No reliable US free-roam total.
- Adjacent: family entertainment centers about USD 29–38B globally (Technavio and others). Laser tag figures conflict.
- Links: [Mordor: location-based VR](https://www.mordorintelligence.com/industry-reports/location-based-virtual-reality-vr-market), [Market Research Future](https://www.marketresearchfuture.com/reports/location-based-vr-market-23403), [Blooloop: Zero Latency 2026 report](https://blooloop.com/zero-latency-vr-2026-report/), [Technavio: FEC market](https://www.technavio.com/report/family-entertainment-center-market-industry-analysis), [Market Intelo: laser tag](https://marketintelo.com/report/laser-tag-center-market)

### Operators
- Sandbox VR: about 90 venues, 20 opened in 2026, plans about 200 franchises by end of 2027, over USD 300M lifetime sales (March 2026), about USD 75M revenue in 2024, ticket about USD 50–53. Rooms of 6 players, party packages for 6, 12 or 18 (about $450–800 per group). No sports or team-vs-team product found.
- Zero Latency: about 150 venues in 30 countries, over 35 in the US. Sol Raiders is its team-vs-team title.
- Links: [Sandbox VR (Wikipedia)](https://en.wikipedia.org/wiki/Sandbox_VR), [VR.org: Sandbox VR 100th location](https://vr.org/articles/sandbox-vr-times-square-100th-location-deadwood-zombie-tickets-2026), [ARtillery: Sandbox scales](https://arinsider.co/2026/03/11/sandbox-scales-signaling-location-based-vrs-turnaround/), [Sandbox funding announcement](https://thesun.my/business-news/media-outreach/new-funding-to-accelerate-sandbox-vr-s-global-franchise-program-set-for-explosive-growth-with-200-projected-stores-in-2027-DB13560021), [Sandbox Chicago events](https://sandboxvr.com/chicago/private-events), [Sandbox Sacramento events](https://sandboxvr.com/sacramento/private-events?lang=zh)

### Reference game: Sol Raiders (Zero Latency)
- Objective-based 4v4 PvP, 4–8 players, 13+, 30–50 minutes. Three maps: push a Soul Orb into the enemy side, a dark "Data Banks" hunt, and a lift plus sniper-tower map. One multi-purpose gun with an overheating laser and a charged spread shot.
- Collision avoidance: oversized avatars, dead players walk back through a "rift" showing every real player, spatial distortion (gondolas, elevators), kill-on-wall rules, chaperone, instructor.
- Hardware history: backpack PCs with overhead tracking, then HP Windows Mixed Reality, now Vive Focus 3 streamed over Wi-Fi 6E from on-site PCs. A listing says Pico 4 and Quest are also supported.
- Reviews: positive on teamwork and fun with friends, negative on chaos and onboarding.
- Links: [Zero Latency Houston: Sol Raiders](https://zerolatencyhouston.com/games/sol-raiders), [Road to VR design write-up, page 1](https://www.roadtovr.com/zero-latency-sol-raiders-tackling-challenges-vr-location-based-pvp/), [page 2 (rift and spatial distortion)](https://roadtovr.com/zero-latency-sol-raiders-tackling-challenges-vr-location-based-pvp/2), [page 3](https://roadtovr.com/zero-latency-sol-raiders-tackling-challenges-vr-location-based-pvp/3), [AggroGamer hands-on](https://aggrogamer.com/article/7135/HandsOn--Sol-Raiders), [Tech Buzz Ireland review](https://techbuzzireland.com/2019/10/04/review-zero-latency-player-vs-player-solraiders-gaming-vr-solraiders), [Road to VR: Vive Focus 3 switch](https://roadtovr.com/vr-attraction-zero-latency-ditches-backpack-pcs-in-favor-of-vive-focus-3-wireless-rendering/), [Shacknews: second-gen hardware](https://www.shacknews.com/article/110667/zero-latency-unveils-second-generation-free-roam-vr-hardware), [Tripadvisor: Montreal](https://www.tripadvisor.com/ShowUserReviews-g155032-d19070787-r714596747-Zero_Latency-Montreal_Quebec.html), [Tripadvisor: Hannover](https://www.tripadvisor.com/Attraction_Review-g187351-d24983950-Reviews-Zero_Latency_Hannover-Hannover_Lower_Saxony.html)

### Outside the US
- Israel: YesVR (Holon) runs wireless VR laser tag for 2–10 players at 100–140 NIS per person, falling with group size. Dubai: VR Point at about AED 136 per player. Germany: Zero Latency announced two new venues in May 2026.
- Links: [YesVR Holon](https://www.escaperoom.co.il/en/holon-yesvr), [VR Point Dubai (KidzApp)](https://kidzapp.com/kids-activities/dubai/fun-play/vr-point-dubai-4d-free-roam-vr-arena-122785), [Games Market: Zero Latency Germany](https://www.gamesmarket.global/two-zero-latency-vr-locations-are-opening-in-germany/)

### Russian arena chain (video, owner's account)
- Arena capex about 3.2M RUB (about 60% build-out, 16% headsets and PCs). Margin about 38% in a normal mall (rent 28%, staff 16%, ads 5%, tax 7%), about 70% in a cheap short-term lease. Payback about 10 months, or under 2 months in the cheap lease.
- Game budget: estimated 1M RUB, actually about 10M, then about 600k RUB per month for a 4-person team plus a freelancer. The game is now licensed to arenas in other cities. Revenue figures not disclosed.

### Selling games to venues (channel)
- Hero Zone: sells a platform and "Arena Max" (Pico 4 Ultra, 6×6 m for 6 players or 6×9 m for 8). Licensing per game, monthly or annual. A January 2026 post says it opened its platform to third-party productions.
- DIVR Labs InstaVR Arena: Pico 4, RFID tracking, 5×5 m play space, 1–4 players, 10-minute sessions, six original games, third-party integration claimed.
- SpringboardVR (2024): the market has not settled on a commercial game-licensing structure.
- Links: [Hero Zone: opening platform to third parties](https://herozonevr.com/post/hero-zone-ups-the-location-based-vr), [Hero Zone profile (VR Collective)](https://thevrcollective.com/hero-zone-profile/), [Hero Zone Arena Max](https://herozonevr.com/arena-max), [InstaVR Arena (VR Collective)](https://thevrcollective.com/product/instavr-arena/), [Blooloop: DIVR Labs InstaVR Arena](https://blooloop.com/play/news/divr-labs-instavr-arena/), [SpringboardVR: commercial licensing in VR arcades](https://springboardvr.com/blog/commercial-licensing-landscape-in-vr-arcades), [VR Collective: free-roam operator guide 2026](https://thevrcollective.com/free-roam-storytelling/)

## 7. Hardware and channel risks

- Meta stopped selling commercial Quest headsets and the paid Horizon Managed Services subscription on 20 February 2026 and shut Horizon Workrooms. Existing customers keep free managed-services access (Quest 3 and 3S until 4 January 2030). Businesses and schools can buy consumer headsets and enrol them in third-party device management (ArborXR, ManageXR, Intune, Ivanti, Omnissa). Pico is the common headset in the venue turnkey systems I found.
- Plan for Pico 4 (Ultra Enterprise) and Quest 3/3S as consumer hardware under third-party MDM. A phone-in-helmet design is not competitive: a Quest 3S is about $300 with tracking and controllers.
- Links: [SiliconANGLE: Meta stops selling Quest to businesses](https://siliconangle.com/2026/01/16/meta-stop-selling-quest-headsets-businesses-discontinue-multiple-vr-features/), [The Register: Horizon Workrooms](https://www.theregister.com/2026/01/16/meta_quest_horizon_workrooms/), [ArborXR: Meta HMS changes](https://arborxr.com/blog/a-practical-guide-to-the-meta-hms-changes-for-xr-teams), [Xpert.Digital: Meta leaves the B2B VR market](https://xpert.digital/metas-abschied-vom-b2b-vr-markt/?amp=1), [Unbound XR: Meta business offer ends](https://unboundxr.eu/blogs/meta-terminates-the-business-offer-as-of-20-february)

## 8. Initial ranking (my judgement, to be tested)

1. First responders and tactical team training. Direct fit for the multi-user free-roam engine, existing vendors prove willingness to pay, and a real gap exists for low-cost standalone systems.
2. Industrial and construction safety. Large mandatory budgets, but evidence of reduced incidents is thin and sales are via safety managers and insurers.
3. Driver and operator training. Proven simulator-hours substitution, though an "extreme driving" product has an open motion-cue problem.
4. Venue games. Fastest to prototype and test, lowest revenue per customer, and a distribution channel exists via Hero Zone and DIVR Labs.
5. Healthcare. Best evidence base, but regulated and device-maker-led.
6. Education. Largest nominal numbers, weakest willingness to pay.

## 9. Open questions and next steps

- Which segment gives the fastest first paid pilot? Candidates: an independent arena in Israel for the game, a fire or security training unit for the team-drill product.
- Ask Hero Zone and DIVR Labs: do you accept third-party games, what is the revenue split, how does onboarding work?
- Count independent free-roam venues and test price points with five operators.
- Verify the vendor claims above against primary studies (the Scientific Reports and Frontiers papers cited by safety vendors, Forrester's ROI study, Walmart's own numbers).
- Research the unresearched segments in 4.9 (mining, utilities, forklift, aviation, evacuation drills).
- Decide the common technical core: headset (Pico 4 versus Quest 3/3S), shared-space tracking method, instructor console, content pipeline.
