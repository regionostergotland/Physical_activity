# Physical activity archetypes (2019-07-12_clst)
This is a set of experimental archetypes that attempt to model self-recorded
physical activity. These attempt to capture detailed information about running,
swimmming and cycling sessions as well as everyday activity and exercise based
activities such as strength, balance and flexibility training.

## Overview of archetypes

### Experimental archetypes
The archetypes produced and available in this repository follows:

* `openEHR-EHR-OBSERVATION.physical_activity.v0`
  
  Main archetype to be used for all types of physical activity.

* `openEHR-EHR-CLUSTER.distance_activity.v0`

  Cluster for recording data about distance based activities. Can be used on
  its own or be specialized.

* `openEHR-EHR-CLUSTER.distance_activity-cycling.v0`

  Specialization of distance activity for cycling.

* `openEHR-EHR-CLUSTER.distance_activity-swimming.v0`

  Specialization of distance activity for swimming.

* `openEHR-EHR-CLUSTER.distance_activity-walking_running.v0`

  Specialization of distance activity for walking and running.

* `openEHR-EHR-CLUSTER.exercise.v0`

  Cluster for specifiying an exercise and how many reps and sets that were
  performed.

* `openEHR-EHR-CLUSTER.training_equipment.v0`
  
  Cluster for specifying a type of equipment that was used during an activity.

* `openEHR-EHR-CLUSTER.vendor_apple_health.v0`

  Quantities that are specific to Apple Health.

* `openEHR-EHR-CLUSTER.vendor_google_fit.v0`

  Quantities that are specific to Google Fit.

* `openEHR-EHR-CLUSTER.borg_scale.v0`

  A measurement of perceived exertion.

### Exisiting archetypes
A list of archetypes that already exists in CKM and are used by the
experimental archetypes follows:

* [`openEHR-EHR-COMPOSITION.self_monitoring.v0`][1]

  Composition to contain one or more instances of the physical activity
  observation.

* [`openEHR-EHR-OBSERVATION.pulse.v1`][2]

  Specify heart rate.

* [`openEHR-EHR-CLUSTER.device.v1`][3]

  Specify device used to record data.

* [`openEHR-EHR-CLUSTER.environmental_conditions.v1`][4]

  Specify environmental data during activity, e.g temperature and humidity.

[1]: https://ckm.openehr.org/ckm/archetypes/1013.1.2430 "Self monitoring"
[2]: https://ckm.openehr.org/ckm/archetypes/1013.1.170 "Pulse/Heart beat"
[3]: https://ckm.openehr.org/ckm/archetypes/1013.1.17 "Medical device"
[4]: https://ckm.openehr.org/ckm/archetypes/1013.1.165 "Environmental conditions"

## General
TODO

### Events
In order to support multiple use cases of recording data; there are four
different types of events available:
  * Point: to record data that is sampled from a single point in time during
    activity.
  * Split, to record data that summarizes a part of a workout, e.g. a lap
    within a running session or any other interval within a workout.
  * Workout, to record data that summarizes an entire workout, e.g. a running
    session.
  * Aggregate, to record data that is aggregated from multiple workouts or
    during a longer period, e.g. a day or a week.

#### Intervals vs points
Some types of data accumulate over time and cannot be sampled from single
points in time, for example traveled distance, expended energy and step count.
Currently all events can host all data elements but these types of data should
not be possible to place under a point event.

However, all types of sampled data such as speed and cadence, can always be
placed under interval events if aggregated with a math function such as
averaging.

The standard allows having different type of elements for different events but
there is not yet sufficient tooling support for this. When there is support;
all elements can be placed under an event and then referenced to all events
where they are appropriate.

### Elements
The main archetype currently has the following elements:

#### Data
  * Activity name (coded text / free text)
    
    Specify what type of activity has taken place, e.g. running or walking. The
    current archetype has coded these internally but this will hopefully be
    coded externally with SNOMED CT or similar.

  * Level of exertion (slot for `openEHR-EHR-CLUSTER.level_of_exertion.v1`)
    
    Specify the exertion from the individual during the activity.

  * Physical activity level (quantity)

    Specify PAL, the total energy expenditure (per 24 h) divided by the basal
    metabolic rate.

  * Active / total energy expenditure (quantity)

    Many watches record either active or total (basal+active) energy
    expenditure. Basal expenditure is not related to activity but if only total
    is available it can be used.

  * Comment (free text)

    Provide further details about the activity at runtime.

  * Additional details (slot)

    Allow providing further detail at template level.

## Training sessions
TODO

### Distance activites
TODO

### Exercise based (Strength / flexibility / balance)
TODO

### Other
TODO

## Daily activity
TODO

### Vendor specific data
TODO
