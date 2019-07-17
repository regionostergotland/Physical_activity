# Physical activity archetypes (2019-07-03_sbrs)
This is a set of experimental archetypes that attempts to allow the modeling of
self-recorded physical activity such as training sessions and every day
activity.

## Overview of archetypes

### Experimental archetypes
The archetypes produced and available in this repository follows:

* `openEHR-EHR-OBSERVATION.physical_activity.v0`

  Main archetype, can be used on its own or specialized.

* `openEHR-EHR-OBSERVATION.physical_activity-walking_running.v0`

  Specialization of main archetype specific to walking or running activity.

* `openEHR-EHR-OBSERVATION.physical_activity-cycling.v0`

  Specialization of main archetype specific to cycling activity.

* `openEHR-EHR-OBSERVATION.physical_activity-swimming.v0`

  Specialization of main archetype specific to swimming activity.

* `openEHR-EHR-CLUSTER.cumulative_elevation_change.v0`

  Gain and drop of elevation, common for both running and cycling.

### Existing archetypes
A list of archetypes that already exists in CKM and are used by the
experimental archetypes follows:

* [`openEHR-EHR-COMPOSITION.self_monitoring.v0`][1]

  Composition to contain observations.

* [`openEHR-EHR-OBSERVATION.pulse.v1`][2]

  Specify heart rate.

* [`openEHR-EHR-CLUSTER.device.v1`][3]

  Specify device used to record data.

* [`openEHR-EHR-CLUSTER.level_of_exertion.v1`][4]

  Specify exertion during activity.

[1]: https://ckm.openehr.org/ckm/archetypes/1013.1.2430 "Self monitoring"
[2]: https://ckm.openehr.org/ckm/archetypes/1013.1.170 "Pulse/Heart beat"
[3]: https://ckm.openehr.org/ckm/archetypes/1013.1.17 "Medical device"
[4]: https://ckm.openehr.org/ckm/archetypes/1013.1.297 "Level of exertion"

## General
Physical activity can recorded by creating an observation

### Events
TODO

### Intensity/exertion data
TODO

### Specialization
TODO

### Shared clusters
TODO

## Training sessions
TODO

### Swimming / biking / running
TODO

### Other
TODO

## Daily activity
TODO
