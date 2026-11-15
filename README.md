NAZEER | Earth Analog Environments Explorer
A planetary analog research platform for exploring how Earth's
environments compare with selected locations on Mars and the Moon.

NAZEER (نظير) combines Earth-observation and environmental datasets with
field measurements from an ESP32-based rover concept. The platform helps
users select an Earth location, inspect its environmental and terrain
characteristics, compare it with planetary reference environments, and
organize candidate analog sites for further investigation.
Project at a Glance
- Project name: NAZEER (نظير)
- Project type: Web-based research and visualization platform
- Challenge: NASA Space Apps Challenge
- Primary goal: Explore and compare terrestrial analog
  environments for planetary exploration research
- Target bodies: Mars and the Moon
- Data approaches: NASA open data APIs and rover-based in-situ
  measurements
The Problem
Researchers and mission planners need ways to identify places on Earth
that can help investigate environmental and operational conditions
relevant to exploring other planetary bodies. Comparing locations using
a single measurement can be misleading: temperature, atmospheric
pressure, humidity, terrain, and other environmental characteristics all
matter, and data availability is not always uniform.

NAZEER brings several of these information sources into one interactive
workflow. It is intended as an exploratory decision-support and
educational tool, not as a substitute for field validation or a
mission-grade planetary environmental model.
Our Approach
NAZEER supports two complementary ways to add an Earth analog candidate:
1. Remote-data workflow: Select or enter an Earth location and
   retrieve available environmental information from open data
   services, including NASA POWER.
2. Field-measurement workflow: Use an ESP32-based rover setup to
   collect environmental readings and transmit telemetry to the web
   dashboard.
The platform stores candidate sites in a working site list. Users can
inspect individual locations, view them on a geographic atlas, and
compare one or more Earth candidates against a selected planetary
reference model.
Key Features
1. Earth Location Selection and Environmental Data
- Enter a location using geographic coordinates.
- Retrieve daily climate parameters from the NASA POWER API.
- The current NASA POWER climate retrieval in the application
  requests:
  - T2M --- air temperature at 2 meters
  - RH2M --- relative humidity at 2 meters
  - PS --- surface air pressure
- The current implementation requests the 2025 daily dataset and
  checks returned units before applying values.
- Elevation information is requested through the Open-Meteo Elevation
  API. The application uses nearby elevation samples to estimate local
  terrain slope.
Important: Not every environmental or terrain variable is available
from the same source. The application tracks data availability and
source information; missing values should not be treated as measured
values.
2. ESP32 Rover Telemetry
The rover workflow is designed to connect field measurements to the
platform.

The dashboard can receive and display telemetry fields including:
- Temperature
- Relative humidity
- Atmospheric pressure
- Terrain slope
- Altitude (when provided)
The web application includes MQTT connectivity, telemetry validation,
connection/status indicators, live charts, and mission controls.
Incoming packets are checked for valid numeric values and plausible
ranges before being accepted.

The application also contains a simulation/demo mode. Simulated
readings are not real rover measurements and must be clearly
distinguished from live hardware data during demonstrations and
evaluation.
3. Planetary Comparison
- Select a planetary reference environment available in the platform,
  including Mars- and Moon-related reference models.
- Compare an Earth candidate across available environmental and
  terrain factors.
- View factor-level results and an overall similarity indicator.
- Review data coverage and unavailable factors alongside the
  comparison.
The similarity indicator is an exploratory, model-dependent score. It
should not be interpreted as proof that two locations are physically
equivalent or that an Earth site reproduces the full planetary
environment. Results depend on the selected reference values, available
measurements, units, and configured factor weights.
4. Multi-Site Comparison
- Select a planetary or Earth reference baseline.
- Select multiple registered Earth analog candidates.
- Compare and rank candidates using the factors supported by the
  available data.
- Review comparison matrices, cards, and charts.
The comparison engine accounts for data availability and normalizes
configured weights over available factors. The interface also reports
data coverage and warns when the available information is insufficient
for a broad similarity judgment.
5. Analog Sites Library and Geographic Atlas
- Browse saved Earth analog candidates.
- Filter records by data-collection workflow, such as rover or
  manual/API entry.
- Inspect location details, coordinates, source labels, and available
  metrics.
- View registered locations on an interactive map.
6. Reports and Data Export
The application includes print-oriented report views and CSV export for
registered analog-site records. Exported fields can include site
identity, country, coordinates, environmental measurements, terrain
descriptors, source information, and ISRU-readiness metadata where
present.
Data Sources and Services
The current application code references the following services:
  Source / Service                                      Role in NAZEER
  NASA POWER            Daily climate parameters such as
temperature, relative humidity, and
surface pressure

  Open-Meteo Elevation                                 Elevation samples used by the
API    application to estimate local slope

  MQTT                             Message-based communication for
rover telemetry

  HiveMQ Public                                        Public MQTT broker endpoint used by
Broker   the current browser implementation
OpenStreetMap       Map data displayed through the
Leaflet mapping library
Other data categories and metadata fields appear in the application (for
example, terrain, solar, and radar-related attributes). Their
availability and provenance can vary by record. Consult each site's
displayed source and availability information rather than assuming every
field is retrieved live from NASA.
Technology Stack
- HTML5 --- application structure
- CSS3 --- styling and responsive interface
- JavaScript --- application logic and data processing
- Tailwind CSS --- utility-based styling
- Three.js --- 3D planetary visualization
- Leaflet --- interactive maps
- Chart.js --- charts and telemetry visualization
- Lucide --- interface icons
- MQTT.js --- browser MQTT client
- ESP32 --- rover-side microcontroller platform
How to Use
1. Open the deployed NAZEER application (add the public URL below when
   available).
2. Choose the remote-data workflow or the rover workflow.
3. For a remote-data site, enter its name and coordinates, then request
   the available environmental and elevation data.
4. For a rover site, connect the supported hardware and confirm that
   live telemetry is being received. Do not use simulated readings as
   field observations.
5. Save the candidate site to the analog-site library.
6. Open the planetary comparison module and choose a Mars or Moon
   reference model.
7. Review the overall indicator, factor-level comparisons, data
   coverage, and source notes.
8. Use the multi-site module to compare several candidates, or export
   the site records for further analysis.
Scientific Scope and Limitations
NAZEER is an exploratory analog-site comparison platform. Earth and
planetary environments differ in important ways, and a limited set of
surface or near-surface variables cannot fully describe those
environments.

Please keep the following limitations in mind:
- Earth datasets and planetary reference values may differ in spatial
  resolution, temporal coverage, measurement method, and units.
- A climate parameter from NASA POWER is not a direct measurement of
  the complete local microclimate at a rover's exact position.
- Rover readings represent the conditions at the sensor location and
  time; they should be accompanied by calibration and measurement
  metadata for scientific use.
- Elevation-derived slope is an estimate based on nearby elevation
  samples, not a full geotechnical terrain assessment.
- Missing or unavailable factors reduce comparison coverage.
- Similarity scores are model outputs for screening and exploration,
  not validated probabilities, mission-suitability certifications, or
  proof of environmental equivalence.
- ISRU-related readiness or terrain metadata should be treated as
  indicative unless supported by documented datasets and a defined
  validation method.
We aim to make data provenance and coverage visible so that users can
understand what supports each comparison.
Repository Contents
A suggested repository structure:
NAZEER/
├── README.md
├── index.html
├── assets/
│   ├── images/
│   └── screenshots/
├── rover/
│   ├── firmware/
│   └── README.md
└── docs/
    ├── methodology.md
    └── data-sources.md
The structure above is a recommendation for organizing the project.
Adjust it to match the files actually included in this repository.
Demo and Project Links
- Live platform: Add deployment URL
- Project video: Add video URL
- Presentation: Add presentation URL
- NASA Space Apps Challenge project page: Add project page URL
Team
Add the names and roles of the project team members.
Acknowledgments
We acknowledge NASA and the open-data providers whose public resources
support exploration, learning, and research. NAZEER is an independent
project developed for the NASA Space Apps Challenge and is not an
official NASA product.
License
  this project return to CEO'S team
