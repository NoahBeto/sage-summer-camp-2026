# 7/20/2026

## Intro

Why We're Here

- Use Sage to solve real science problems.
- Learn AI@Edge concepts and tools.
- Build prototypes + collaborate with others.

Daily Workflow

- Slack for communication + help.
- GitHub for project repos.
- Google Drive for shared docs.

Schedule

- 8:00–9:15 - Open hacking
- 9:15 - Q&A
- 9:30–12:30 - Morning session
- Lunch
- 13:30–16:30 - Afternoon session
- 16:30–18:00 - Open hacking

EVL Rules

- Only water in classroom.
- Keep food in kitchen/hall.
- Clean up before leaving.

Big 8 Goals

- Challenge problem + team
- classroom-notes.md
- 5‑minute presentation
- project.md
- ECR app (if relevant)
- Poster
- Hermes brain
- Course review

Sage Grande Testbed

- National AI@Edge testbed.
- 300 new AI-enabled platforms across the US.
- Real-time sensing: wildfire, flooding, drought.
- Focus on safety, privacy, and edge inference.

Reasons to use edge computing:

- Bandwidth: reduces the need to send large amounts of data to the cloud.
- Privacy: sensitive data stays on the device instead of being streamed out.
- Power usage: more efficient than constantly transmitting data.
- Low latency: decisions happen immediately, right where the data is produced.
- Resiliency: applications keep working even if connectivity or external power is lost - smart infrastructure shouldn’t fail just because the network does.

Example Edge AI Applications

- Bird sound ID + biodiversity monitoring.
- Flood + volcanic eruption detection.
- Pedestrian flow tracking (YOLO + BoT-SORT).
- Cloud motion vectors + weather nowcasting.

Hardware

- Cameras (sky + ground).
- Weather sensors.
- Microphone.
- NVIDIA Jetson (Xavier NX / AGX Orin).
- 4G/5G/WiFi connectivity.

AI Agents

- New abstraction layer above OS + hardware.
- Automate workflows, coding, and edge orchestration.
- Used for autonomous sensing + decision-making.

Bonsai 27B

- 27B model running on a phone (3.9–5.9GB).
- Supports reasoning, tool use, and vision tasks.

Project Ideas

- Adaptive sampling.
- Anomaly detection.
- Privacy-preserving sensing.
- Bird/insect detection.
- Edge pipelines (producer -> consumer).

## Sage Platform Fundamentals

Overview

- Session is a hands‑on introduction to the Sage platform: portal, data, node access, and app development.
- Goal: get comfortable using Sage tools and working directly on edge hardware.

Portal & Accounts

- The Sage portal is the main entry point for browsing nodes, sensors, and data.
- You need a Sage account + SSH keys added to access development nodes.
- Thor-based systems are new, so expect some rough edges.

Data Model

- Timeseries Data
- Lightweight sensor measurements stored for fast querying.

File-Oriented Data (images, audio, etc.)

- Larger data is staged on the node and uploaded to an object store when bandwidth allows.
- Object URLs are automatically referenced in timeseries entries.

Access Methods

- Sage Data Client (Python) - easiest, recommended.
- HTTP Data API - raw JSON stream; useful for non‑Python tools.

Node Access

- Development nodes let you test apps on real Jetson Thor hardware.
- SSH access is granted automatically once your key syncs.
- Nodes appear under “My Nodes” in the portal.

Edge Apps

- Apps read sensor/audio/video data, process it, and publish results.
- Built from code + dependencies + models, packaged for Waggle nodes.
- Lifecycle: develop -> package -> schedule -> analyze.

Edge Code Repository (ECR)

- Catalog of existing apps.
- Reference for building your own.

Deployment

- Apps submitted to ECR can be scheduled to run on specific nodes.
- Once deployed, you can query your app’s output using the data client.

# 7/21/2026

## Model Context Protocol

MCP

- MCP = Model Context Protocol, a standard that lets AI agents safely interact with external tools, APIs, and data sources.
- It acts like a bridge between an AI model and real systems - giving the model controlled access to things like:
    - Sage APIs
    - Node‑management tools
    - File systems
    - Databases
    - Custom scientific services
- MCP servers expose capabilities (like “run this command” or “query this dataset”) in a structured, permissioned way.
- This makes AI agents much more useful because they can:
    - Fetch real data
    - Run code
    - Manage nodes
    - Trigger workflows
    - Build and test software

## More about Sage

AI@Edge Applications

- Sage hosts many edge AI apps (bird ID, cloud cover, smoke detection, motion tracking).
- You can explore apps in the Edge Code Repository and run them on Sage nodes.

Biodiversity Monitoring

- BirdNET models run on Sage nodes to identify birds from audio.
- Useful for ecosystem health tracking.

Building Edge Models

- Example workflows: cloud segmentation, wildfire smoke detection.
- Collect data -> label -> upload -> train -> deploy on nodes.

Doppler Lidar + AI

- AI classifies sky conditions (clear, cloudy, rainy) from lidar spectra.
- Edge-triggered processing saves storage by only analyzing full spectra when needed.
- Sage can steer lidars automatically based on weather conditions (e.g., low-level jets).

Future Edge Directions

- Research into ultra‑low‑power, battery‑free AI devices (Protean platform).
- Hardware‑accelerated ML on tiny energy-harvesting systems.

## Hermes, Compaction, and Token Costs

Hermes

- Hermes runs inside tmux, letting AI agents work persistently in a terminal session.
- Useful for long-running tasks, debugging, and keeping context alive across commands.
- Lets you “pause and resume” AI‑assisted development without losing state.

Compaction

- Before storage fills up, Hermes performs compaction - cleaning logs, trimming context, and reducing saved state.
- Prevents sessions from crashing due to disk limits.
- Helps keep the agent fast and responsive.

Token Cost Awareness

- Every piece of input you send to an LLM costs tokens.
- Rough rule: ~$12 per million tokens (varies by model).
- Important to keep prompts short, focused, and efficient.
- Avoid dumping huge logs or unnecessary text - it increases cost and slows the agent.
- Good habit: summarize, trim, and only send what the model actually needs.

## Deep Learning Basics

What Deep Learning Is

- Subfield of ML focused on pattern recognition using deep neural networks.
- Models don’t give absolute truth - they give best guesses under uncertainty.
- Think of predictions as probability distributions, not exact answers.

Neurons & Forward Pass
- A neuron = weighted sum + bias -> activation function.
- Forward pass: compute output from inputs.
- Activation functions (ReLU, Leaky ReLU, ELU, Swish) introduce non‑linearity.
- Hidden layers usually use ReLU; avoid sigmoid/tanh in hidden layers.

Networks
- More neurons = more “bends” in the function (Universal Approximation Theorem).
- Deeper networks often generalize better but can be harder to train.
- Different architectures exist (CNN, RNN, LSTM, Autoencoder, GAN, etc.) depending on the task.

Datasets

- Good datasets must be: relevant, diverse, labeled correctly, representative, and clean.
- Split data into train / validation / test (e.g., 70/15/15).
- Watch out for:
    - Imbalance
    - Concept drift
    - Data drift
    - Label drift
- Preprocessing helps: normalization, removing duplicates, handling missing values, augmentation.

Training Loop

- Forward pass
- Compute loss
- Backprop (compute gradients)
- Optimizer step (update weights)
- Common losses: cross‑entropy (classification), MSE/MAE (regression).
- Common optimizers: Adam, AdamW, SGD+Momentum.

Metrics

- Classification: accuracy, precision, recall, F1.
- Regression: RMSE, MAE, R^2.

Overfitting & Learning

- Compare training vs validation loss.
- Early stopping prevents overfitting.
- Regularization helps generalization.
- Hyperparameters (learning rate, batch size, depth, optimizer) strongly affect performance.

Anomaly Detection (Hawaii Team)

- Uses YOLO + VLMs for fire/smoke detection.
- Goal: general anomaly detection that adapts to changing environments.
- Approaches include:
    - ResNet/VIT embeddings
    - Memory banks
    - Similarity scoring
    - PCA / alignment heads

# 7/22/2026

## Foundation Models & Edge Inference

BioCLIP + Imageomics

- Imageomics uses AI to study biological traits directly from images.
- BioCLIP models are large vision transformers trained on massive biodiversity datasets (10M–233M images).
- They learn “unsupervised biological structure” - e.g., age, sex, species differences - without explicit labels.

Why Foundation Models Matter

- They handle huge, multimodal biodiversity datasets (camera traps, UAVs, satellite, bioacoustics).
- They help fill gaps in global biodiversity knowledge (taxonomy, traits, distributions, interactions).
- Zero‑shot classification lets you identify species without training a custom model.

BioCLIP Ecosystem

- Includes models, datasets, benchmarks, software tools, and demos.
- Tools like pybioclip, TreeOfLife toolbox, and TaxonoPy help integrate BioCLIP into pipelines.
- Catalog provides ready‑to‑use models and datasets for research.

Adapting Foundation Models

- Different levels of adaptation depending on compute + data:
    - Zero-shot -> no training, just prompts.
    - Probe suite -> tiny classifiers trained on embeddings.
    - LoRA / prompt tuning -> ~1% of parameters.
    - Text tower tuning (LiT) -> update only text encoder.
    - Last-k block tuning -> partial fine‑tuning of vision tower.
    - Full fine‑tuning -> all ~1B parameters; expensive but highest performance.

Fine‑Tuning Costs (Real Example)

- 2.65M images, 7.8k species.
- 2x RTX 5090 GPUs.
- ~60 GPU‑hours total.
- Shows that full fine‑tuning is heavy but doable with strong hardware.

Quantization for Edge Deployment

- Reduces model size + latency at the cost of some accuracy.
- Options: FP16, BF16, INT8, INT4, FP8, FP4, QAT.
- Important for running large models on edge devices like Jetson Thor.

Edge Constraints

- Power, bandwidth, storage, memory.
- Latency requirements for real‑time science.
- Remote troubleshooting + limited compute.
- Foundation models must be optimized before deployment.

Example Activity: Peromyscus Classification

- Hard-to-distinguish species (P. leucopus vs P. maniculatus).
- Shows how BioCLIP can be adapted to specific taxonomic groups.

NDP JupyterHub Workspace

- Provides GPU-backed JupyterLab environments for BioCLIP experiments.
- Students can launch servers with RTX 3090 GPUs and run BioCLIP pipelines.

## Sage Image Search

What is it?

- System for searching Sage’s massive image archive using semantic embeddings.
- Built for edge + cloud environments.
- Uses vector databases (Milvus) + modern AI models.
- Supports scientific workflows like anomaly detection, environmental monitoring, and pattern discovery.

Resources

- GitHub repo: waggle-sensor/sage-nrp-image-search
- Learning guide + notebook for hands-on labs.
- NDP workspace available for GPU-backed experimentation.
- Production deployment: Sage Portal -> Image Search Lab.
- Blogs + poster publication explain design + benchmarking.
- Tools involved: Milvus, Gradio, Hugging Face, NDP.

Key Takeaways

- Sage Image Search is a scalable, reproducible AI system for scientific cyberinfrastructure.
- Demonstrates how semantic search + embeddings can unlock huge sensor datasets.
- Provides a foundation for building more advanced AI agents and multimodal scientific tools.

# 7/23/2026

## National Data Platform (NDP)

What NDP Is

- NSF‑funded platform for open data, AI services, and collaborative scientific computing.
- Built by UC San Diego (SDSC), University of Utah, University of Colorado Boulder, EarthScope Consortium.
- Goal: unify fragmented data sources and make them easy to find, analyze, and use.

Why NDP Matters

- Scientific data is hard to use because of:
- messy formats + inconsistent metadata
- scattered storage locations
- lack of tools for collaboration
- difficulty deploying compute near data
- limited access to scalable infrastructure
- NDP tries to solve all of this with a federated data ecosystem.

What NDP Provides

1. Searchable Data Catalogs
    - Standardized metadata + vocabularies.
    - Integrates data from research groups, government agencies, and national facilities.
    - Supports FAIR data principles.
2. Collaborative Workspaces
    - Run analysis directly in the browser (JupyterLab).
    - No need to download huge datasets.
    - Bring your own data + build near‑data services.
3. Access to National Cyberinfrastructure
    - Deploy workflows to HPC, cloud, or edge resources.
    - Standardized software stack for reproducible compute.
4. AI‑Integrated Workflows
    - Tools for training, testing, and deploying ML models.
    - Supports multimodal scientific AI pipelines.
5. Education + Data Challenges
    - Classroom tools, tutorials, and hands‑on learning experiences.

Using NDP

- Registering
    - Go to nationaldataplatform.org -> Log In/Register.
    - Authenticate via CI‑Logon (institution or ORCID).
    - Create/edit your profile (roles, expertise, bio).
- Catalog Search
    - Search datasets by keyword, tags, organization.
    - Explore metadata + resources (WMS, WCS, data files).
    - Example: “Water” -> climatic water deficit datasets.
- Map Search
    - Draw polygons on a map to filter datasets spatially.
    - Useful for geospatial collections (e.g., lidar).
    - Example: draw around CA/AZ -> explore USGS lidar datasets.
- Registering Digital Assets
    - Add datasets to your catalog.
    - View metadata, provenance, and resource links.

Key Takeaways

- NDP is a central hub for scientific data + AI workflows.
- Makes large datasets usable without heavy setup.
- Provides compute, collaboration, and education tools.
- Perfect for Sage users who need structured access to national data resources.

## NDP Workspaces

Sage Data API Client

- Used to query Sage node data (e.g., weekly humidity + temperature from node W06C).
- Supports correlation analysis and environmental data exploration.
- Example workflow:
    - Pull humidity + temperature.
    - Compute correlation (e.g., RH decreases ~1.6% per °F).
    - Compare with NEON Eddy Covariance data (evapotranspiration vs VPD).

NDP ARGUS (Agentic Coding)

- Jupyter notebook add‑on that enables agentic coding inside cells.
- Adds:
    - Skills
    - MCP servers
    - Automated data‑query tools
- Lets you ask questions like: “What’s the highest temperature recorded today across all nodes?”  
and get structured results from Sage APIs.

Wildfire Smoke Detection

- Includes Sage’s current smoke‑detection plugin.
- NDP workspace supports:
    - Running multimodal SmokeyNet models.
    - Integrating Sage sensors with external sources (NEON, ATMOS).
- Useful for real‑time wildfire monitoring and anomaly detection.

Sage Live Eddy Covariance (SLEC)

- NEON eddy‑covariance data streamed into Sage (provisional since July 2025).
- Edge plugin processes flux tower data.
- Applications:
    - Rain‑pulse effects (Birch Effect).
    - Drought recovery.
    - Real‑time ecosystem monitoring.

Key Takeaways

- NDP workspaces let you run Sage data workflows without local setup.
- ARGUS enables AI‑assisted coding directly in Jupyter.
- Sage + NEON + NDP = powerful combined ecosystem for environmental science.
- Supports smoke detection, flux analysis, climate correlations, and more.

# 7/24/2026

## Sensors, Hardware, and Physical Integration

Big Picture

- Sage nodes are edge computing platforms deployed outdoors with cameras, weather sensors, audio, and expansion ports.
- The session explains what goes into an edge device, how sensors connect, how communication works, and how next‑gen Sage Thor nodes support foundation‑model inference.

What an Edge Device Needs

- Compute: low‑power CPU/GPU SoCs (Jetson Xavier, Jetson Thor).
- Sensors & Instruments: cameras, weather sensors, microphones, air quality sensors, etc.
- Communication: Ethernet, Wi‑Fi, LoRaWAN, USB, UART, RS‑485.
- Device Management: power distribution, watchdogs, brownout detection, fault recovery.
- Power: AC/DC input, conversion, PoE for sensors.
- Resiliency: must survive weather, outages, and hardware faults.

Design Principles (Deep Space Probe Analogy)

- Stay alive - recover from faults, use backup partitions, read‑only filesystems.
- Call home - restore communication, retry hardware/software recovery.
- Gracefully degrade - shut down subsystems to preserve core functionality.
- Operate autonomously - handle long communication gaps.

Wild Sage Node (Previous Generation)

- ~3 ft tall outdoor enclosure.
- Includes:
    - Sky-facing camera (POE)
    - Ground-facing camera (POE)
    - Optical rain sensor
    - BME680/BME280 weather sensors
    - Microphone
    - 4G/5G/WiFi connectivity
    - PoE + USB sensor expansion ports
- Ruggedized for environmental deployment.

Sage Node Interfaces

- POE Ports (Sen1–Sen4)
    - 30W max power.
    - DHCP addressing.
    - Used for cameras, Stevenson shield, and additional sensors.
- USB2 Port (Sen5)
    - For legacy USB sensors.
    - Only accessible to main processing module.
- Additional Interfaces
    - LoRaWAN, GPIO, UART, RS‑485 via adapters.

Sensor Categories

- Sensors
    - Raw measurement devices (temperature, humidity, PM2.5, microphones).
- Instruments
    - More complex, calibrated systems (lidars, gas analyzers, disdrometers).
- Actuators
    - Devices that change the physical world (PTZ motors, relays).
- Software‑Defined Sensors
    - ML apps that publish derived measurements (e.g., “car count” from video).

How Devices Attach to a Node (5 Ways)

- Direct (USB, GPIO, I2C, UART)
- Networked (Ethernet/PoE)
- Wireless IP (Wi‑Fi)
- Microcontroller‑mediated
- Gateway‑mediated (LoRaWAN)
- Rule of thumb: The farther, lower‑power, or more numerous the sensors, the more you move toward gateway‑mediated.

Communication Layer Cake

- Each layer is independent:
- Transducer -> Electrical Interface -> Bus/Signaling -> Transport Protocol -> Application Protocol -> Data Format -> OS Interface -> Application > Data Product
- Examples:
    - USB -> CDC‑ACM -> ASCII -> CSV -> /dev/ttyACM0
    - Ethernet -> TCP -> HTTP -> JSON -> eth0

Communication Technologies

- USB
    - Host/device model.
    - Enumeration creates /dev/ttyACM*, /dev/ttyUSB*, /dev/video*.
    - Short cable limits (3–5m).
    - Limited power.
- Ethernet/IP
    - Long cable runs (100m).
    - PoE powers sensors.
    - Supports RTSP, REST, Modbus‑TCP.
- Wi‑Fi
    - Convenient but unreliable for unattended systems.
    - Reconnection behavior is critical.
- Bluetooth/BLE
    - Good for provisioning or short‑range sensors.
    - Not reliable for long‑term unattended deployments.
- LoRa vs LoRaWAN
    - Long range, tiny bandwidth.
    - Great for low‑rate environmental sensors.
    - Gateway -> network server > application server.
- UART
    - Simple serial interface.
    - Must match baud rate + voltage levels.
    - Often accessed via USB‑UART adapters.
- RS‑232
    - Legacy serial standard.
    - High voltages; requires level shifting.
- RS‑485
    - Differential signaling.
    - Long distances (up to ~1 km).
    - Multi‑drop bus for many sensors.

Next‑Generation Sage Thor Nodes

- Designed for foundation model inference at the edge.
- Transformer models (SAM2, Gemini, GPT‑style) require:
    - High memory (Gemini 27B ~60GB)
    - High power (+100W)
- Jetson Thor provides:
    - High‑end GPU
    - Multiple fans
    - Rugged carrier board
    - Out‑of‑band management
    - Power distribution + router

Thor-Blade Benchmarking (LLM Inference)

- Devkit
    - Throughput: 8–9.7 tokens/sec
    - Power: 80–100W
    - SoC temp: 60–70°C
    - Efficiency: ~0.1 tok/s/W
- AVerMedia Variant
    - Throughput: 9.2–10.4 tokens/sec
    - Power: 120–140W
    - SoC temp: 58–62°C
    - Efficiency: ~0.078 tok/s/W

Sensor Integration in Sage Grande Testbed

- Supported sensors include:
    - LoRaWAN devices
    - Air quality sensors (Vaisala AQT530)
    - Weather stations
    - PTZ cameras
    - Infrared cameras
    - Soil sensors (CSU MKR WAN)
    - BME280/BME680
    - Lidar ceilometers (Vaisala CL61)

PyWaggle Message Layer

- Provides unified messaging between:
    - Sensors
    - Applications
    - Drivers
- Supports AMQP, RTSP, RTP.
- Enables apps to share intermediate results.

Accessing Sensors (Examples)

- Networked (PoE)
    - High bandwidth
    - HTTP/RTSP interfaces
- USB
    - Serial communication
    - Sensitive to cable noise
- Sensor-in-the-box
    - Microcontroller wraps sensor -> network interface
- Wireless (LoRaWAN)
    - Low-power, long-range, tiny messages
- Linux Industrial I/O (IIO)
    - Example: reading BME280 via /sys/bus/iio/devices

Key Takeaways

- Edge devices must be robust, fault‑tolerant, and autonomous.
- Sensor integration requires understanding electrical, protocol, and software layers.
- Sage Thor nodes bring foundation-model inference to the edge.
- Communication technologies each have tradeoffs - choose based on distance, bandwidth, power, and reliability.
- PyWaggle + Sage Grande Testbed provide a flexible platform for multimodal sensing and AI@Edge.

# 7/27/2026

## Agentic PTZ Cameras

Why PTZ Agents Matter

- PTZ cameras have thousands of possible views; fixed scan loops miss important events.
- An agent can decide where to look, based on goals like smoke detection, wildlife tracking, or cloud observation.
- Instead of rigid scripts, you give the node a plain‑English goal, and it plans movements, chooses models, and interprets what it sees.

Core Components
- Brain (LLM): reasoning loop (ReAct), local or cloud; plans actions and interprets results.
- Eyes (Vision Models):
    - YOLO -> objects & motion
    - BioCLIP -> species & biodiversity
    - Gemma -> scene descriptions
- Hands (Gateway): the only part that touches hardware; drives PTZ, reads sensors, returns structured outputs.

Architecture

- Agent loop is stable “core”; extensions happen via config, drivers, skills, tools.
- Hardware is always accessed through the gateway, never directly.
- Errors degrade gracefully instead of crashing the agent.

Vision at the Edge

- Runs multiple models on Jetson Orin / Thor.
- Memory is the main constraint -> lazy loading, eviction, fallback behavior.
- Supports tiled inference for wide views and small distant targets.

Using the Agent

- One command runs a task: python -m ptz_node run "…goal…"
- Preflight tools check hardware and config.
- Demo workflows available (smoke patrol, biodiversity scan, land cover).
- Outputs include progress logs, final English summary, and a saved trace.

Autonomy

- Built‑in scheduler for unattended operation.
- Supports repeating tasks, cron‑style triggers, and bounded runs.
- Crash‑safe, SQLite‑backed, isolated subprocess per job.

Camera Support

- Fully drivable now: simulated panorama, Reolink PTZ.
- View + identify (PTZ pending): Axis, Hanwha/Wisenet, Mobotix, Hikvision, Dahua.
- Auto‑discovery finds vendor, model, RTSP URL.

Getting Started

- Quick bootstrap on-node with Python 3.11 + requirements.
- Supports both local LLMs (Ollama) and cloud LLMs (OpenRouter).
- Backend can be set to simulation for development.