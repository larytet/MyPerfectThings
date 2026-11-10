I use a small kick scooter for shopping. I hang the bags on the handlebar and push the scooter. Downhill I sometimes ride it with the bags still hanging on the handlebar. It works, but the load pulls the handlebar sideways, the scooter tips when I let go, and a heavy bag swings into the front wheel. See also [shopping-trolley.md](shopping-trolley.md), the earlier version of this idea.

## The idea

A self-balancing shopping cart with two wheels. It stays upright by itself, even when the bags are unevenly loaded, and it can be parked without a stand. Two ways to get it to the customer:

*  **Store carts.** The store keeps a fleet of them at the entrance, like regular carts. Fits stores that already have a coin or token lock (see [shopping-cart-coin.md](shopping-cart-coin.md)) and in-store positioning (see [gps-in-store.md](gps-in-store.md)).
*  **Personal carts.** The buyer owns the cart, folds it, carries it in the car or on the bus, and brings it into the store. This is the scooter-with-bags use case, and the one I actually need.

Possible features:

*  Balances under an uneven load (a heavy bag on one side). A gyro and a motor on the axle, like a Segway or hoverboard, do this well.
*  Hold mode: when I let go of the handle, the cart stays upright instead of falling.
*  Power assist uphill, and regenerative braking downhill so the load does not run into me.
*  Optional follow-me mode (see Gita below), so the cart can trail me through the store or along the sidewalk.
*  Folds flat. Hooks or a hanger for the standard bag types (IKEA bags, 50-60 lb loads).
*  Rideable by the owner on flat ground or downhill, which is what I do now with the scooter.

Open questions: stability on curbs and stairs, anti-theft in a store fleet, how it behaves when a child or a pet runs into it, regulation (a self-propelled cart in a shop is a liability issue), and the price against a $30 granny cart.

## Is there anything like this? Prior art

I searched the web and crowdfunding coverage. I did not find a self-balancing two-wheeled shopping cart on Kickstarter or Indiegogo, either for stores or for personal use. This is not a full search of the Kickstarter site itself. I only saw what the search engine returned, so it is worth searching Kickstarter directly for "self-balancing cart" before building. The closest products are below. Claims marked "(vendor)" come from the company's own material.

**Closest: self-balancing two-wheeled cargo robots**

*  **Piaggio Fast Forward Gita / gitamini** - a self-balancing two-wheeled robot that follows its owner and carries about 40 lb (18 kg) of groceries or other goods in a lidded bin. A camera belt worn by the owner and its own point-cloud map let it keep up around corners. Launched 2017, went on sale in November 2019 at $3,250. Aimed at personal mobility, not at stores. This is the closest prior art for the personal cart. The weak points are the price and that it does not fold, and I could not confirm the current price or availability; check the company site. [TechCrunch](https://techcrunch.com/2017/01/31/why-piaggio-built-gita-a-cargo-carrying-robot-to-follow-in-your-footsteps), [Dezeen](https://www.dezeen.com/2017/01/30/piaggio-fast-forward-gita-personal-cargo-robot-autonomous-follows-you-around-transport-news/), [New Atlas](https://newatlas.com/piaggio-gita/47646), [IEEE Spectrum](https://spectrum.ieee.org/automaton/robotics/home-robots/piaggio-cargo-robot), [MIT Technology Review](https://www.technologyreview.com/s/603558/this-robot-will-carry-your-stuff-and-follow-you-around/), [gitamini physical overview](https://knowledge.mygita.com/gitamini-physical-overview), [gita shop](https://knowledge.mygita.com/gita-shop), [Fortune review of gitamini](https://www.fortune.com/2022/12/10/gitamini-service-robot-review-walk-short-car-trips)
*  **Ascento Pro** - a self-balancing two-wheeled autonomous robot (legged wheels) that climbs stairs. A research and security robot, not a cart, but it shows that a two-wheeled balancing platform can handle stairs. [Laughing Squid](https://laughingsquid.com/ascento-pro-two-wheeled-robot/)
*  **Segway Loomo (2018)** - a two-wheeled self-balancing rideable that turns into a follow-me robot. The pitch included carrying bags home. [Electronics Specifier](https://electronicspecifier.com/news/analysis/the-new-segway-can-also-be-a-cute-robot-companion), [TechXplore](https://techxplore.com/news/2018-03-two-wheel-smart-sidekick.html)

**Self-balancing rideables (same balancing technology, not carts)**

*  **Solowheel Iota** (Inventist) - two small wheels instead of one for a stabler ride. Kickstarter 2017, $219,569 from 457 backers. Shows that a self-balancing two-wheeler can be funded on Kickstarter. [Digital Trends](https://digitaltrends.com/cool-tech/solowheel-iota-kickstarter), [New Atlas](https://newatlas.com/inventist-solowheel-iota/47563/), [Indiegogo](https://indiegogo.com/projects/solowheel-iota-a-mini-personal-e-vehicle--3)
*  **Puppy 1 (90Fun)** - a follow-me suitcase that uses self-balancing technology from a Segway partnership. Mentioned in the roundup below; I did not find a dedicated review. [Roundup](https://reviewed.com/news/cowa-robot-suitcase-follows-you-around-like-lost-puppy)

**Follow-me luggage and carts (follow, but do not balance)**

*  **Ovis (ForwardX)** - follow-me suitcase that recognizes its owner; reported at about $800. [Tom's Guide](https://www.tomsguide.com/us/ovis-smart-suitcase-hands-off-testing,news-27285.html), [New Atlas](https://newatlas.com/ovis-suitcase/55063)
*  **Travelmate** - autonomous suitcase with a Follow Me feature. [CNBC](https://www.cnbc.com/2017/04/24/travelmate-an-autonomous-suitcase.html), [The Manual](https://themanual.com/travel/travelmate-robotics-suitcase-autonomously-follows-owner)
*  **Naucrates** - follows the owner; the reviewer found it jerky and only trusted it in uncrowded areas. [9to5Mac](https://9to5mac.com/2019/10/14/naucrates-review/)
*  **Cowarobot R1** - follows a bracelet worn by the owner. [Digital Trends](https://digitaltrends.com/cool-tech/cowarobot-r1-robotic-suitcase-news)
*  **Cart robot with auto-follow function** - a 2019 Korean patent for a store cart that follows the shopper. This is the store-fleet side of the idea. [USPTO PDF](https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/11585934)
*  **University of Illinois follow-me cart** - a student project (camera, ultrasonic sensors, Raspberry Pi) that follows the user and avoids collisions. [Course project (ECE 445)](https://courses.physics.illinois.edu/ece445/getfile.asp?id=25289)

**Powered carts and wagons (carry the load, do not balance)**

*  **Litefar Orion** - remote-controlled motorized wagon, up to 180 lb, four wheels. Went to Kickstarter to fund production (early bird $399 reported). [Kowatek blog](https://blog.kowatek.com/?p=75130), [Notebookcheck](https://www.notebookcheck.net/Experience-a-piece-of-Death-Stranding-with-this-affordable-motorised-AI-handcart-with-camera.1077152.0.html)
*  **UpCart City** - folding stair-climbing dolly. The first UpCart campaign on Kickstarter in 2014 reached only $27,387 of $100,000, but the product later sold. A useful warning about how hard crowdfunding a cart can be. [New Atlas](https://newatlas.com/upcart-city-loads-folds-flat/54493)
*  **Buddy Lift Plasmoid** - commercial motorized stair-climbing hand truck. [DirectIndustry](https://www.directindustry.com/prod/zonzini/product-181355-2493829.html)
*  **Granny carts / Shoppa Cart** - unpowered, the thing the personal cart would replace. [Core77](https://core77.com/posts/116918)

**Kick scooters with baskets (my current workaround, made official)**

*  **Razor EcoSmart Cargo** - electric scooter with a basket that fits a bag of groceries; Tom's Guide suggests bungee cords. [Tom's Guide](https://www.tomsguide.com/reviews/razor-ecosmart-cargo), [Inverse](https://www.inverse.com/input/tech/razor-ecosmart-electric-scooter)
*  **Hammacher Schlemmer Electric Sit/Stand Cargo Scooter** - folding model with a large rear basket. [Hammacher](https://hammacher.com/product/electric-sit-stand-cargo-scooter)
*  **Gyroor scooter with a large middle basket** - up to 300 lb load, 30 miles range (vendor). [Cool Hunting](https://coolhunting.com/buy/silk-lantern/)
*  **Sharper Image sit-down scooter with basket** and **HOVSCO Porto Max** - retail listings, marketing copy only. [Sharper Image](https://sharperimage.com/products/sit-down-electric-scooter-with-basket), [HOVSCO](https://hovsco.com/products/porto-max-electric-scooter)

## Tandem layouts (front and rear wheel, like a kick scooter)

Most of the products above have the wheels on the sides. A tandem layout can balance too. There are three methods; only the first two work at a standstill. I found no commercial or crowdfunded tandem balancing cart or scooter in this search.

**Steering-based (no gyro, low weight)**

*  **Honda Riding Assist-e (2017 concept)** - a motorcycle that balances by small computer-driven steering corrections, with an adjustable headstock rake to amplify them. No gyroscopes, to save weight. It can balance stationary and roll at walking pace without a rider. The balance algorithms are said to come from Honda's Uni-Cub and ASIMO work. Concept only, no production commitment. The best reference for a tandem layout without a gyro. [Electrek](https://electrek.co/2017/09/29/honda-introduces-riding-assist-e-self-balancing-electric-motorcycle/), [Cycle World](https://www.cycleworld.com/honda-self-balancing-motorcycle-rider-assist-technology), [Visordown](https://www.visordown.com/motorcycle-news-new-bikes/honda-riding-assist-e), [Visordown on the patent](https://www.visordown.com/news/new-bikes/honda-riding-assist-e-even-madder-patent), [Fox News](https://www.foxnews.com/auto/hondas-self-balancing-bike-stands-alone), [Motorcycle News](https://motorcyclenews.com/news/new-tech/honda-auto-steering)
*  **Research: bicycle robot at zero forward speed** - a paper that regulates the frame's tilt by rotating the front wheel, with no mechanical regulator. [SAGE journals](https://journals.sagepub.com/doi/10.5772/56701)

**Reaction wheel (flywheel) at a standstill**

*  **Murata Boy** - a bicycle robot with a flywheel. An academic paper calls it the most striking flywheel bicycle robot: it stands still, tracks a curve and climbs a slope. I did not get a direct source for the robot itself, only the paper's description. [Pink Tentacle](https://pinktentacle.com/?p=766), [Seiko unicycle robot for comparison (Gizmodo)](https://gizmodo.com/little-seiko-unicycling-robot-caught-on-video-unicycli-5056143)
*  **Aoki2001 self-balancer** - a hobby bicycle-style robot with a reaction wheel that balances at a complete standstill. [Hackaday](https://hackaday.com/2012/06/29/self-balancer-does-it-differently-than-were-used-to-seeing)
*  **Self-stabilizing autonomous bicycle (2012 diploma thesis)** - a driverless bicycle with a reaction wheel and an IMU. The reviewer noted the ground clearance is poor. [Hackaday](https://hackaday.com/2012/03/25/self-stabilizing-autonomous-bicycle)
*  **Reaction-wheel bicycle thesis (UMT Lahore, 2023)** - balances at several tilt angles, with lower power than other methods. [UMT eScholar](https://escholar.umt.edu.pk/items/c8fb2028-6c6b-4f74-b921-72d899c8c716)

**Gyroscope (control moment gyroscope, CMG)**

*  **Lit Motors C-1** - an enclosed two-wheeled vehicle that balances with gyroscopes (about 800 Nm of torque quoted for the C-1), at a standstill too. Orders opened in 2023. The best-documented production-oriented tandem balancer, but a vehicle, not a cart. [Wikipedia](https://en.wikipedia.org/wiki/Lit_Motors), [PopSci](https://www.popsci.com/self-balancing-two-wheeled-car/), [Electrify News](https://electrifynews.com/news/moto/meet-the-new-self-balancing-fully-enclosed-electric-motorcycle), [Scooter.uk.com 2023 orders](https://scooter.uk.com/news/lit-motors/lit-motors-starts-accepting-orders-2023/)
*  **Lit Motors Kubo** - a two-wheeled electric cargo scooter that went to Kickstarter in 2013. Lit Motors calls it self-balancing, and one database (Bikez) says it uses two gyroscopes to stay upright when stopped. The 2013 launch coverage does not mention gyroscopes, so treat the balancing claim as unconfirmed. A cargo scooter, so the closest tandem relative to this idea. [Lit Motors Kubo page](https://www.litmotors.com/kubo-scooter), [New Atlas](https://newatlas.com/lit-motors-kubo-electric-cargo-scooter/29858), [ETA](https://www.eta.co.uk/news/kubo-an-electric-cargo-scooter-for-the-city), [Autoblog](https://www.autoblog.com/2013/11/20/lit-motors-kubo-electric-cargo-scooter-video/), [Bikez](https://bikez.com/models/lit_motors_kubo.php)
*  **Gyroscope bicycle (student project)** - a gyroscope with a PID controller on a two-wheeler. [Google Slides](https://docs.google.com/presentation/d/1V8crsmxO86pbZ3eGFERCfk2_boE84A-y0Xr6Vgp7CIU/htmlpresent)
*  CMGs cost more and use more energy than reaction wheels (from a Turkish-language paper listing the balancing methods). [DergiPark](https://dergipark.org.tr/en/download/article-file/822540)

**Self-stable (no actuator, only while moving)**

*  **Northeastern self-stable bicycle** - a bicycle built to cancel the gyroscope effect with counter-rotating discs and minimal trail. It cruises riderless, but only while moving, so it does not solve the standstill problem. [Northeastern](https://coe.northeastern.edu/news/self-stable-bicycles)

Takeaway: steering-only balancing (Honda) is the lightest, and reaction wheels (Murata, hobby builds) are the cheapest standstill option. A gyro (Lit Motors) works but is heavy. Honda's approach is only shown at the concept stage. The Kubo is the one tandem cargo product that went to Kickstarter.

## Gap

The follow-me robots (Gita) balance on two wheels but cost thousands of dollars and are not carts. The cheap powered carts and scooters with baskets are cheap but do not balance, so a heavy side load still tips them. Self-balancing rideables (Solowheel, Segway) prove the balancing is cheap and fundable, but nobody has put a fold-flat, hang-bags-on-the-handle, balancing cart under $500 on the market, as far as I could find. Nor did I find a store fleet of such carts. The scooter-with-bags use case (push on flat ground, coast downhill, uneven bag loads) seems untouched.

## Next steps

*  Search Kickstarter and Indiegogo directly for "self-balancing cart", "balancing trolley", "hoverboard cart" and "follow me cart".
*  Look at hoverboard-based DIY carts (a hoverboard motor pair and gyro board is a cheap prototype base).
*  Check Gita's current price and whether it is still sold; that sets the price ceiling.
*  Check patents (the Korean follow cart patent above is a start) for self-balancing trolleys.
