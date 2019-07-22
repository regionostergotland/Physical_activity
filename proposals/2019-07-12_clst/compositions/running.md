# Running session

A running session can be recorded by using the "Walking/Running" cluster inside
a "Physical activity" observation.  Heart rate is often recorded during running
and this can be recorded by using the "Pulse/Heart beat" observation next to
the "Physical activity" observation.

A composition that records a running session as captured by a typical sports
watch may look something like the example below.

Even though a session might only consist of single workout, it may be necessary
to use multiple events of different types. A single workout event can only
contain summarized data about an event that has been aggregated with a single
math function. Therefore, if we wish to record both averages and totals of a
workout, we must use at least two overlapping "Workout" events.

If we have more detailed information such as lap times or a time series of
sampled data, we may use overlapping "Split" and "Point" events as well like in
the below example. The below example tracks a single workout but has two
"Workout" event and as well as "Split" event for each lap and a "Point" event
for each sampled point within the workout.

```
self_monitoring (composition):
  pulse_heart_beat:
    data:
      any_event: time: 2019-07-04T12:49:26, width: PT1H50M52S, math_fn: average
        rate: 155
      maximum: time: 2019-07-04T12:49:26, width: PT1H50M52S, math_fn: max
        rate: 172
  physical_activity:
    data:
      workout: time: 2019-07-04T12:49:26, width: PT1H50M52S, math_fn: total
        activity_name: "Running"
        active_energy_expenditure: 1476 kcal
        activity_details:
          walking_running:
            cumulative_details:
              distance: 20.8 km
              step_count: 19030
              elevation_gain: 201 m
              elevation_drop: 202 m
      workout: time: 2019-07-04T12:49:26, width: PT1H50M52S, math_fn: average
        activity_name: "Running"
        activity_details:
          walking_running:
            details:
              pace:
                time_per_distance: PT5M21S
                distance: 1 km
              speed: 11.2 km/h
              step_cadence: 173 /min
              stride_length: 1.1 m
      split: time: 2019-07-04T12:49:26, width: PT5M25S, math_fn: total
        activity_name: "Running"
        activity_details:
          walking_running:
            cumulative_details:
              distance: 1 km
              step_count: 952
              elevation_gain: 10 m
              elevation_drop: 2 m
      ..
      split: time: 2019-07-04T12:55:01, width: PT3M10S, math_fn: total
        activity_name: "Running"
        activity_details:
          walking_running:
            cumulative_details:
              distance: 0.8 km
              step_count: 730
              elevation_gain: 2 m
              elevation_drop: 12 m
      point: time: 2019-07-04T12:49:26
        activity_name: "Running"
        activity_details:
          walking_running:
            details:
              pace:
                time_per_distance: PT5M53S
                distance: 1 km
              step_cadence: 170 /min
              altitude: 80 m
              stride_length: 1.0 m
      ..
      point: time: 2019-07-04T14:40:18
        activity_name: "Running"
        activity_details:
          walking_running:
            details:
              pace:
                time_per_distance: PT3M58S
                distance: 1 km
              step_cadence: 180 /min
              altitude: 79 m
              stride_length: 1.4 m
```
