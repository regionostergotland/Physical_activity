# Physical activity archetypes (2019-07-12_clst)
This is a set of experimental archetypes that attempt to model self-recorded
physical activity. These attempt to capture detailed information about running,
swimmming and cycling sessions as well as everyday activity and exercise based
activities such as strength, balance and flexibility training.

These archetypes experiment with using clusters in order to extend the modeling
to multiple types of activities.

## Overview of archetypes
The archetypes listed in the below sections are all the archetypes that can be
used when modeling physical activity.

### Experimental archetypes
The archetypes produced and available are listed below. These are meant to test
new ideas and are not proposals for fully complete archetypes. They may
therefore have lacking descriptions, improper element names, missing quantity
units and other issues that has not been addressed in order to not waste time
on archetypes that later may be scrapped.

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
experimental are listed below. Some of theser are reviewed and published while
some are not.

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
Physical activity can recorded by creating a template for a "Self monitoring"
composition and adding one or more "Physical activity" observations (or
specializations) to its content.

### Events
In order to support multiple use cases of recording data; there are four
different types of events available:
  * **Point**, to record data that is sampled from a single point in time
    during activity.
  * **Split**, to record data that summarizes a part of a workout, e.g. a lap
    within a running session or any other interval within a workout.
  * **Workout**, to record data that summarizes an entire workout, e.g. a
    running session.
  * **Aggregated**, to record data that is aggregated from multiple workouts or
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
The main observation archetype currently has the elements listed in below
sections.

#### Data
  The main archetype currently has the following data elements under each
  event:

  * **Activity name** (coded text / free text)

    Specify what type of activity has taken place, e.g. running or walking. The
    current archetype has coded these internally but this will hopefully be
    coded externally with SNOMED CT or similar.

  * **Physical activity level** (quantity)

    Specify PAL, the total energy expenditure (per 24 h) divided by the basal
    metabolic rate.

  * **Metabolic equivalent of task** (quantity)

    Specify MET, the ratio of the expenditure rate during the activity compared
    to the resting rate.

  * **Active / total energy expenditure** (quantity)

    Many watches record either active or total (basal+active) energy
    expenditure. Basal expenditure is not related to activity but if only total
    is available it can be used.

  * **Description** (free text)

    Describe the performed activity.

  * **Comment** (free text)

    Provide further details about the activity at runtime.

  * **Activity details** (slot)

    Provide activity specific details. Currently there is a "Distance activity"
    cluster with specializations that can be used as well as an "Exercise"
    cluster. Vendor specific data can also be recorded with the "Google Fit
    specific" and "Apple Health specific" clusters.

  * **Perceived exertion** (slot)

    Provide information about the perceived exertion of the individual.
    Currently there is only a single example of a cluster, Borg scale, which
    models the 6-20 scale proposed by Borg.

#### State
  The main archetype currently has the following state elements under each
  event:

  * **Equipment** (slot)

    Specify any equipment that has been used during the activity. Use the
    "Training equipment" cluster or a specialization of it.

  * **Environment** (slot)

    Specify environmental data during activity with e.g. the "Environmental
    Conditions" cluster. Watches often measure temperature and humidity and
    these may be helpful in interpreting the data.

  * **Venue/terrain** (cluster)

    * **Description** (free text)

    Describe the venue or terrain where the activity has taken place.

    * **Additional details** (slot)

    Add additional details about the venue/terrain. No examples have been
    created as of yet, but it may be of interest to model terrain and road
    surface types.

  * **Additional details** (slot)

    Allow adding more details about the state at template level.

#### Protocol
  The main archetype currently has the following protocol elements:

  * **Techniques** (coded text)

    Specify how the data was obtained.

  * **Device** (cluster)

    Specify one or more devices that was used to record data. Use the "Medical
    device" cluster or a specialization.

## Training sessions
The archetype can be used to capture training sessions of a wide range of
activites.

### Distance activites
Distance based activities can be recorded by using the main observation
"Physical activity" and either add the "Distance activity" cluster or a
specialization of it to the "Activity details" slot. Specializations currently
exist for walking/running, swimming and cycling activities.

#### Distance activity cluster
The general cluster has been divided into two separate subclusters; "Details"
and "Cumulative details". These subclusters are meant to be used mutually
exclusive in events, meaning that only one of the clusters should be used
inside a single event. The reason is that the cumulative subcluster only
contains data that accumulate over time and may not be sampled from a single
point. This cluster may only exist under a interval event with the math
function total. The details event contains sampled data that can either
represent a point in time or a interval of time with a math function such as
average, min or max.

The distance cluster contains more than only distance. Whenever a distance is
traveled, there is a duration of it and a speed at every point within that
duration. The duration can be modeled with the width element of the event and
the speed and distance can be modeled with the fields of the cluster.

For many distance based sports there is also a periodic action that is used to
propel the body forward. When running, these are steps, for cycling these are
pedal revolutions and for swimming it is swim strokes. Whenever there is a
periodic action, it is possible to measure its frequency at a point and its
total amount during an interval. Because of this; the cluster contains a
"Cadence" element for the frequency and a "Count" element for the total amount.

When moving over distances, there may also be changes in altitude that alters
the incline. The cluster therefore also contains elements for sampled altitude
points as well as cumulative gain in elevation and drop.

The details subcluster also contains another cluster; pace. Primarily when
running, speed is almost exclusively measured in terms of minutes per km or
minutes per mile, also known as pace. It is however not possible to use min/km
as unit for an element as it is a duration divided by a distance. An element
may either be a duration or a quantity, not a mix of the two. A cluster
containing both the duration and the distance has therefore been used. A 5:30
/km pace can then be modeled by setting the "Time per distance" element to 5:30
and the distance element to 1 km.

#### Specialization clusters
The "Distance activity" cluster has been specialized for three different
activities; running, swimming and cycling in order to remove irrelevant
elements, add additional fields as well as further clarify what count and
cadence refers to for each type of activity.

The swimming archetype has renamed cadence and count to "Stroke cadence" and
"Stroke count" and disabled the elevation gain and drops because these are not
applicable to swimming. There is also an added element to specify swimming
style.

The cycling archetype has renamed cadence and count to "Pedaling rate" and
"Pedal revolutions" as well as added an element for power output which is often
measured when cycling.

The walking/running archetype has renamed cadence and count to "Step cadence"
and "Step count" as well as added an element for stride length which can be an
important metric of the running style.

### Exercise based (Strength / flexibility / balance)
Exercise based activities can be recorded by adding an "Exercise" cluster for
each "session" that has been performed for a specific type of exercise.
Examples of exercise based activities may be a strength training session, a
yoga session or a hand balancing session. Examples of exercises may be push
ups, headstands, handstands, shoulder stands, planches, pancakes, bench
presses, bicep curls and many, many, many more with mulitple variations of
each.

#### Exercise cluster
The exercise cluster, most importantly, has an element "Exercise name" that
specifies what exercise has been performed. Since there a huge amount of
possible exercises this should be externally coded or in any case allow for
free text.

In most cases the exercise name may be clear enough to determine what exercise
it is, e.g. if it is a common exercise such as a push up or a bench press. If
it however is a more obscure or not well-defined or local exercise it may also
require a description which can be added to the free text "Description"
element.

Exercises are often performed with multiple repetitions to form a set. And
often multiple sets are performed after each other with rest in-between. This
can be modeled with the "Number of sets" and "Number of repetitions" elements.
The "Rest after set" can also be used to specify how long the rest was after
each set.

Repetitions can often be performed with varying difficulties. The cluster
allows to specify the duration, resistance and resistance type for each
reptition if any. Duration may be relevant for e.g. static exercises such as a
plank, a balancing exercise such as a freestanding handstand or a stretching
exercise such as a pancake. Resistance are applicable for all exercises with
weights, such as bench presses, dead lifts, or weighted pull ups. Types of
resistances may be free weights, weight machines, bar bells and others.

The exercise also has slot for specifying equipment that was used during the
exercise. Examples may include gymnastic rings, training bars, weight machines
or any other type of equipment.

### Other
Other activities than distance based or exercise based may be modeled if
sufficient, simply by using the main archetype. An example may be a 2 h session
of football with some information about exertion. Activities that require more
specific and structured data may require that a cluster is created and added to
the "Activity details" slot.

## Daily activity
Daily activity is generally an aggregation of all activity that has been
performed during a longer period. Since the activity may be one of the types of
activities that model training sessions, the clusters for these may very well
be reused for tracking every day activity.

Watches and mobile phones often track individuals step count, floors climbed,
distance walked and distance cycled as well as calories expendend. These can be
modeled by using the "Walking/Running" and "Cycling" clusters and plug them
under activity details in an "Aggregated" event. The calories can be recorded
by using the elements in the main archetype.

The PAL and MET fields may also be used if these are available directly or if
they can be calculated from available data.

### Vendor specific data
There are some types of units created by vendors such as Google and Apple that
may be of interest if available. Because these are sometimes proprietary with
an unknown formula, often impossible to convert to standard quantities and
often specific to a single vendor; these has been modeled exactly as provided
and grouped by vendor.

Examples of vendor specific units are move minutes and heart points from
[Google][1]; stand time, stand hours and exercise time from [Apple][2] as well
as [NikeFuel][3] from Nike.

Currently, clusters have been created for the two largest providers, Google and
Apple.

[1]: https://support.google.com/fit/answer/7619539 "Heart points, move minutes"
[2]: https://www.apple.com/watch/close-your-rings/ "Stand and exercise rings"
[3]: https://news.nike.com/news/what-is-nikefuel "What is NikeFuel?"

#### Cluster reuse
This project has focused on observations and modeling recorded data, but
another interesting use may be to model similar data for instructions or
actions. Since most of the archetypes are clusters, these can simply be reused
by adding a slots for them.
