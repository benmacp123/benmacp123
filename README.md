### Hi, I'm Benjamin

I turn research algorithms into production systems on AWS: Python,
serverless and GIS. In my career I build the Python products behind real-time
power-grid measurement. In my own time I apply the same engineering to conservation,
building pipelines on open wildlife data that a field team could trust.

Every project here runs from committed or public data with no accounts or
keys, is scored on data held out from tuning, and reports the result honestly,
even when it is negative.

I'm open to projects in conservation and environmental data. You can reach me
on [LinkedIn](https://www.linkedin.com/in/benjamin-david-macpherson-332052197).

### Projects

**[camera-trap-mlops](https://github.com/benmacp123/camera-trap-mlops)**:
decides, site by site, whether to trust an off-the-shelf camera-trap
classifier (SpeciesNet, BioCLIP 2) or replace it with an adapted one. The test
was fixed and hashed in advance, then ten camera sites held out from all tuning
were scored once.
- A small classifier on DINOv2 embeddings beat BioCLIP 2 zero-shot at all ten
  sites: balanced accuracy 0.933 against 0.836, a gain of 9.7 points (95%
  interval 5.5 to 15.0). Fine-tuning a whole CNN beat zero-shot but not the
  small classifier, after 14 hours of training against seconds. The promoted
  model is [published on Hugging Face](https://huggingface.co/benmacp123/orinoquia-dinov2-probe).
- The checks built to watch it afterwards were mostly modest or negative, and
  are reported as they fell: the model's confidence ranks sites by accuracy
  but predicts a site's accuracy only about a point better than guessing the
  average, and labelling twenty sequences per site moved accuracy by 0.3
  points. Sending answers under 50% confidence to a person means reviewing
  6.6% of sequences and cuts errors from 7.8% to 4.1%.
- Measured on AWS Lambda at $0.267 per 10,000 crops, with the same answers as
  the local model. One study area in Colombia, so it says nothing about a new
  region.

**[collar-telemetry](https://github.com/benmacp123/collar-telemetry)**
(in progress): an alerting pipeline for wildlife GPS collars. It turns late,
duplicated and missing fixes into alerts for possible deaths, silent collars,
unusual movement and park-boundary crossings, scored against real recorded
deaths in public Movebank data.
- Every held-out vulture death raised an alert (10 of 10), but only 3% of
  fast mortality alerts were real. Stillness alone cannot say a bird is dead:
  living vultures sit still for that long about 70 times as often as carcasses
  appear. The slower "potential death" alert did better: 27% (8.1-77%) with
  ideal data arrival and 40% (14-80%) with daily satellite uploads. With five
  carcasses, those intervals are wide.
- So the fast alert became a self-clearing "stationary: check" watch, and only
  an escalated tier that needs independent evidence is sent to a person.
  Targets for each tier were fixed before anything is scored again, to be
  validated once on studies not used so far.
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

- **[population-model](https://github.com/benmacp123/population-model)**
  (closed): how far can noisy aerial counts of Kruger herbivores be trusted?
  Two forecasting models failed to beat naive baselines, both documented as
  negative results. A third version simulated how reliably a threshold alert
  catches a real decline in roan, sable and tsessebe; a later review of it
  found its headline numbers depended on how the question was set up, and the
  README now says so.

### Tools

Python · AWS (Lambda, SQS, DynamoDB, SNS, EventBridge) · Terraform ·
Docker · polars and DuckDB · GIS (shapely, GeoJSON) · state-space models and Kalman filters ·
held-out evaluation and paired bootstrap · Hugging Face · pytest · GitHub Actions

### Background

MEng Computer Science (Distinction), University of Strathclyde.
Certificates in GIS and in ecology and ecosystem conservation; ZSL Academy
participant.
