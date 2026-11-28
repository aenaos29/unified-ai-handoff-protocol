# Veridian Plaza Handoff Example

This is a real-world example of an AI-generated technical handoff produced through iterative game development. It demonstrates context preservation, knowledge transfer, technical specification reuse, and potential cross-project reproducibility.

**Reproducibility status:** not independently validated. The handoff records supplied requirements and design decisions; it does not establish that the described implementation has been completed or reproduced.

---

## Original Playground handoff

Create a single-player 3D futuristic exploration prototype called "Veridian Plaza" in 16:9 landscape orientation using Three.js, React Three Fiber, Drei, Postprocessing, and Rapier physics (fixed 1/60s 60 Hz timestep). Prioritize cinematic visual fidelity, architectural detail, and smooth traversal over gameplay complexity—do NOT include storylines, combat, scoring loops, investigation mechanics, timers, or building interiors.

### 1. Visual Architecture (Aenaos Visual Engine v0.1)
Organize rendering, procedural PBR materials, lighting, water, spatial corridor validation, architecture, and vegetation into clean modular files:
- **Rendering & Adaptive Mobile Performance**: Configure ACES Filmic tone mapping (exposure ~0.88–0.90), PCFSoftShadowMap, and adaptive mobile/desktop profiles (scaling DPR `[1, 1.35]` mobile / `[1, 1.75]` desktop, shadow map size `1024` mobile / `2048` desktop, shadow frustum tight around the visible camera focus, and environment/contact-shadow resolutions).
- **Procedural PBR Materials**: Generate and cache procedural diffuse, Sobel tangent-space normal, bump, and roughness maps for composite titanium-terrazzo plaza tiles, conductive basalt-carbon walkways, emerald bio-turf, pearl aero-ceramic, carbon-titanium armor, emerald-slate ceramic panels, anodized bronze-graphite cladding, brushed white-silver aluminum, copper-carbon acoustic slats, tree bark, botanical foliage, and striped solar-weave awning canvas.
- **Balanced Daylight & Post-Processing**: Balanced directional solar key light following the camera focus, cool-sky ambient and hemisphere fill, procedural sky dome and lightformer IBL reflections, atmospheric fog with a distant horizon haze cylinder, baked architectural contact shadows plus grounded character shadow discs, subtle bloom (`luminanceThreshold: 1.18`, `intensity: 0.22`), light vignette, and mobile-optimized `N8AO` ambient occlusion (half-resolution and reduced samples on mobile) for subtle architectural crevice depth without darkening the scene.
- **Fresnel Fountain Water**: At the plaza center, build a Hydro-Quantum Fountain featuring a rotating gyro-ring core, animated water droplets, and a custom GLSL water shader with Schlick Fresnel grazing reflections, dual-wave animated ripples, rim foam, and solar specular highlights.

### 2. Futuristic Pedestrian Plaza & Seven Typed Buildings
Arrange **seven distinct futuristic buildings** around a circular central pedestrian square, all facing inward and connected by continuous radial walkways and an outer promenade ring. **No vehicle roads and no cars.** Every surface must be flush and walkable at `Y = 0` with zero gaps, steps, or invisible snags.
1. **Courthouse (Civic Arbitration Tribunal)**: Pearl-ceramic facade, fluted titanium columns with bases/capitals, extruded triangular pediment with a rotating golden holographic seal, solar-glass cupola dome, bronze/gold torchère pylons, and arched recessed entrance.
2. **Police Station (Autonomous Security Precinct)**: Carbon-titanium armored hull with angled corner buttresses, rotating rooftop radar dish, cobalt security beacons, energy bollards, holo-flagpole, and arched airlock entrance.
3. **Research Laboratory (Quantum & Bio-Tech Institute)**: Brushed aluminum cantilevered wings, vertical solar-louver fins, rooftop biosphere dome, double-height glass atrium housing a spinning tri-axis kinetic containment sculpture, and airlock entrance.
4. **Office Building (Meridian Orbital Exchange)**: Bronze-graphite stepped tower base with diagonal exoskeleton struts, curtain-wall glazing bays, glowing horizontal floor bands, rooftop penthouse spire, and cantilevered lobby marquee.
5. **Lounge (Neon-Amber Synth Conservatory)**: Anodized copper-walnut pavilion with vertical acoustic louvers, warm amber-coral panoramic glazing, cantilevered halo canopy with recessed downlights, brass stanchions with amber ribbons, and illuminated planters.
6. **School (Veridian Cybernetics Academy)**: Emerald-slate ceramic collegiate facade with pitched solar-slate roof, glowing atomic chronometer clock tower, arched observatory windows, courtyard lantern pillars, and arched entrance.
7. **UNION Café (Automated Roastery & Bistro)**: Pearl-ceramic and deep-teal titanium storefront with solar-weave striped awning, holographic menu stand, illuminated signboard, and outdoor chrome-marble terrace tables with espresso pods, chairs, and striped parasols.

Use multilayered facades with extruded curved arches and keystones, dentil cornice moldings, 3D recessed window bays (with jambs, sills, and mullions), and street-level recessed functional entrances.

### 3. Spatial Corridor Validation & Street Details
Before placing any prop or tree, enforce protected pedestrian corridors (`~4.9m` clear width along all 7 radial paths), entrance clearance zones (`~4.25m` radius), central square/promenade lanes, spawn clearance, and exact rotated building footprint OBBs. Validate every prop's full physical footprint against those zones and add matching Rapier colliders for:
- Multi-limbed bark-textured broadleaf trees with stone tree-pit curbs, layered cypresses, terracotta flower urns, cantilevered composite benches, solar-ring lamps, recycling pods, courier data-drop terminals, a titanium garden pergola, a holo-wayfinding plinth, animated mechanical songbirds, sunlight dust motes, and a distant neo-arcology skyline.

### 4. Articulated Android Characters & Bypassers
Avoid blocky/voxel/low-poly characters:
- **Playable Android Explorer**: Realistic-proportioned articulated explorer with pearl-ceramic chest carapace, carbon-fiber joints, glowing cyan wraparound optical visor, sternum reactor core, dorsal spine telemetry LEDs, shoulder pauldrons, crossbody data-pack satchel, tech scarf collar, multi-jointed knee/elbow walk/jog/idle animation, and boot soles grounded at `Y = 0`.
- **Six Conversational Android Bypassers**: Units EL-7 (Elena), MK-4 (Marcus), NR-9 (Noor), JL-2 (Julian), CL-5 (Claire), and MT-3 (Mateo) with distinct chassis colors, LED hues, cranial crests (halo, antennae, fin, visor cap), and props (holopad, thermal coffee pod, briefcase, data-tote). Strolling units patrol walkable corridors, pause politely and turn toward the player when approached, and cycle through 3 sci-fi dialogue lines when spoken to.

### 5. Third-Person Camera, Controls & Minimal UI
- **Camera Behavior**: Automatic third-person rear over-the-shoulder follow camera (`~50°` FOV, `~5.4m` distance) with ray-vs-OBB building-wall pull-in so it never clips into facades. Include **30° left/right slack** before the camera smoothly turns behind the explorer's perspective, and latch the movement reference heading during backward/sideways movement so walking backward or turning around never causes U-turn spinning while the camera swings smoothly behind the player's back. Support optional mouse-drag orbit and scroll-wheel zoom on desktop.
- **Controls**: `WASD` / Arrow keys to walk, `Shift` to jog, `E` / `Space` to speak with bypassers or inspect entrances/landmarks. On touch devices, render ONLY a **single** bottom-left movement joystick plus `JOG` and `ACT` buttons (never add a second camera joystick).
- **Minimal UI**: Keep the 3D world unobstructed with a minimal top-left location badge, top-right Menu button (Resume, Music/SFX toggles, Restart, How to Play, Quit), and **top-center** transient interaction prompts, citizen dialogue cards, and architectural scan plaques.

Let me know if you want any adjustments to this handoff prompt!
