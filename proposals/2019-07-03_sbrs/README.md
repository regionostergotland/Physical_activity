# Physical activity archetypes (2019-07-03_sbrs)
This is a set of experimental archetypes that attempt to model self-recorded
physical activity such as training sessions and every day activity. When
creating these, focus was placed on running, cycling and swimming activities
and some daily activity. Extending these to other types of activity may require
altererations and additional archetypes.

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

* [`openEHR-EHR-CLUSTER.environmental_conditions.v1`][4]

  Specify environmental data during activity, e.g temperature and humidity.

* [`openEHR-EHR-CLUSTER.level_of_exertion.v1`][5]

  Specify exertion during activity.

[1]: https://ckm.openehr.org/ckm/archetypes/1013.1.2430 "Self monitoring"
[2]: https://ckm.openehr.org/ckm/archetypes/1013.1.170 "Pulse/Heart beat"
[3]: https://ckm.openehr.org/ckm/archetypes/1013.1.17 "Medical device"
[4]: https://ckm.openehr.org/ckm/archetypes/1013.1.165 "Environmental conditions"
[5]: https://ckm.openehr.org/ckm/archetypes/1013.1.297 "Level of exertion"

## General
Physical activity can recorded by creating a template for a `self_monitoring`
composition and adding one or more `physical_activity`-observations (or
specializations) to its content.

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
The general archetype currently has the following elements:

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

#### State
  * Environment (cluster)
  
    Specify environmental data during activity. Watches often measure
    temperature and humidity and these may be helpful in interpreting the data.

  * Additional details (slot)
    
    Allow adding more details about the state at template level.

### Specialization
As mentioned, there is a main archetype as well as multiple specializations.
Some elements like the ones above, can apply to any type of physical activity.
There are however data that is only applicable to certain activities. Distance
for example is very central to running but has no real interpretation in a
strength workout. There are also state data that is only relevant for certain
activites. Information about terrain and road surface may help interpretating a
cycling session but cannot be used for a swim in a pool.

Specialization has thus been used in order to not have a large single archetype
with data elements for every possible activity and not having to duplicate all
the common elements for each activity.

A reason to use specialization instead of clusters for each activity is that
with specialization it is possible to add both data and state elements that are
specific to a activity with a single archetype. If clusters are used, there
must be one cluster to place under data and another cluster to place under
activity.

### Shared clusters
It is also possible for data to be common between some activities but not for
all. An example is elevation change which is important for both running and
cycling but not for swimming. Cluster slots with a shared cluster can be used
to avoid duplication in this case.

## Training sessions
A session can now be
recorded by creating a composition with an observation of the performed
activity and simply adding the recorded data to it.

Multiple workout events can be recorded for the same observation if the same
activity is performed multiple times. If different activities are performed,
for e.g. a triathlon, multiple observations of different types can be added to
the composition.

### Swimming / cycling / walking / running
Specializations of the main archetype has been created in order to allow
recording sessions of swimming, cycling and running. 

The swimming specialization adds elements for data about distance, speed,
stroke count and style used. It also adds state elements about the swimming
venue, pool length and water temperature.

The cycling specialization adds elements for data about distance, speed,
cadence, power output, elevation change (shared cluster) and altitude. The
altitude can be used to determine the incline. It also adds state such as
bicycle type and wheel diameter as well as information about road surface.

The walking/running specialization adds elements for data about distance,
speed, cadence, stride length, elevation change (shared cluster) and altitude.
It also adds state about footwear and the terrain.

All of these three activities are distance based and whenever there is
distance, there is also speed. It would be nice to avoid remodeling these for
each activity somehow. It is also relevant for daily activity as watches/phones
often automatically record distances travelled by foot and by bike. It is
however important to know which type of activity each distance or speed is
based on since for example swimming 5km is very different from cycling 5km,
just like bicycling 40 km/h is very different from running 40 km/h.

### Other
Other types of activities can be recorded by either using any of the above
archetypes (general or specialization).

For activities that do not have much data and one simply is interested in the
type of activity and duration it is possible to use the main archetype and add
workout event with the activity name set to whatever activity is performed.
This can used to record e.g. a "1h aerobic session".

For activities that require more data than provided by above archetypes a
specialization can be created.

## Daily activity
One of the main interests of this project is to be able to record every day
activity that is not necessarily specific workouts. For this purpose, the
"Aggregated" event shall be used.

An interesting metric may be daily step count for a week. This can be achieved
by creating a walking/running observation with a "Aggregated" event for each
day and then setting the step count element.

If walking and cycling distances are available these can be recorded by adding
a walking/running and cycling observation and setting the distance elements for
each observation.
