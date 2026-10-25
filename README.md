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
  fast mortality alerts were real; the slower "potential death" alert was
  right 29-43% of the time, ten to fifteen times more trustworthy.
- On Kruger elephants, every "left the park" alert came from the unfenced
  western edge shared with private reserves: the boundary matters as much
  as the detector.
- Deployed to AWS with Terraform (SQS FIFO, Lambda, DynamoDB, SNS),
  replayed over 3,466 animal-months with every incident matching the local
  run, then torn down. The full run cost $0.23; the idle queue trigger, not
  the animals, is most of a small project's bill.

**[vessel-anomaly](https://github.com/benmacp123/vessel-anomaly)**:
flags vessel behaviour worth a fisheries analyst's attention in public AIS
tracks from the US Northeast: fishing in closures that ban the gear in use,
unexplained transmission gaps, encounters at sea and loitering. Thresholds
were frozen before a held-out block of 542 unseen vessels was scored once.
- A coverage mask records where receivers cannot see; it removes two-thirds
  to three-quarters of gap alerts that would otherwise be reception holes,
  not vessels going dark.
- Gaps planted into real tracks were found 71% of the time, and a
  classifier shows planted gaps are easier than real ones, so that is an
  upper estimate. The other detectors caught every planted event and none
  of the planted near misses.
- Runs as a restartable streaming service in Docker that matches the batch
  run event for event, even after a mid-run kill. Costed from measured work
  against AWS prices: batching costs about $0.76 a month at regional volume,
  against $42 for processing each message on its own.

### Also

- **[population-model](https://github.com/benmacp123/population-model)**:
  how far can noisy aerial counts of Kruger herbivores be trusted? Two
  forecasting models failed to beat naive baselines, both documented as
  negative results; a third version shows survey precision matters more
  than frequency for catching a real decline in roan, sable and tsessebe.

### In progress

- **[camera-trap-mlops](https://github.com/benmacp123/camera-trap-mlops)**:
  decides, site by site, whether to trust a zero-shot camera-trap
  classifier (SpeciesNet, BioCLIP 2) or replace it with an adapted one,
  and watches for label-free signs that the decision needs revisiting.

### Tools

Python · AWS (Lambda, SQS, DynamoDB, SNS, EventBridge) · Terraform ·
Docker · polars and DuckDB · GIS (shapely, GeoJSON) · state-space models and Kalman filters ·
pytest · GitHub Actions

### Background

MEng Computer Science (Distinction), University of Strathclyde.
Certificates in GIS and in ecology and ecosystem conservation; ZSL Academy
participant.
