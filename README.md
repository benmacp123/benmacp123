### Hi, I'm Benjamin

I turn research algorithms into production systems on AWS: Python,
serverless and GIS. In my career I build the Python products behind real-time
power-grid measurement. In my own time I apply the same engineering to conservation, 
building pipelines on open wildlife data that a field team could trust.

Every project here runs from committed data with no accounts or keys, is
scored against data it never saw, and reports the result honestly, even
when it is negative.

### Projects

**[collar-telemetry](https://github.com/benmacp123/collar-telemetry)**:
an alerting pipeline for wildlife GPS collars. It turns late, duplicated
and missing fixes into alerts for possible deaths, silent collars, unusual
movement and park-boundary crossings, scored against real recorded deaths
in public Movebank data.
- Every held-out vulture death raised an alert (10 of 10), but only 3% of
  fast mortality alerts were real; the "likely death" alert was about ten
  times more trustworthy.
- On Kruger elephants, every "left the park" alert came from the unfenced
  western edge shared with private reserves: the boundary matters as much
  as the detector.
- Pure-Python detection core, AWS Lambda handlers tested end to end
  against an emulator, and Terraform infrastructure validated in CI.

**[population-model](https://github.com/benmacp123/population-model)**:
a two-stage population model for Kruger National Park herbivores,
calibrated on 1965-1979 census counts and tested against 1980-1995.
- It fits the calibration period to within 11-13% but cannot beat simply
  carrying the last count forward, a documented negative result. The most
  likely missing ingredient is rainfall.

### Tools

Python · AWS (Lambda, SQS, DynamoDB) · Terraform · Docker · GIS (shapely,
GeoJSON) · pytest · GitHub Actions

### Background

MEng Computer Science (Distinction), University of Strathclyde.
Certificates in GIS and in ecology and ecosystem conservation; ZSL Academy
participant.
