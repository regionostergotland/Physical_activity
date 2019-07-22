# Recording daily steps

Step counts can be recorded by using the _Walking/Running_ cluster inside a
_Physical Activity_ observation. A composition for three days of daily step
counts might look something like below.
```
self_monitoring: (composition)
  physical_activity: (observation)
    data:
      aggregrate: time: 2019-07-07T00:00, width: P1D, math_fn: total
        activity_details:
          walking_running:
            step_count: 15732
      aggregrate: time: 2019-07-08T00:00, width: P1D, math_fn: total
        activity_details:
          walking_running:
            step_count: 13490
      aggregrate: time: 2019-07-09T00:00, width: P1D, math_fn: total
        activity_details:
          walking_running:
            step_count: 10903
    protocol:
      device: (CLUSTER.device.v1)
        device_name: "FitBit Charge 3"
        type: "smartwatch"
```
We use the _Walking/Running_ observation inside a _Self monitoring_
composition. For each day, we create an _Aggregate_ event with a 1-day width
and set the _Step count_ data element to the number of steps recorded for that
day. We can also specify the device that was used to record the steps by using
the _Device_ element under the protocol branch.
