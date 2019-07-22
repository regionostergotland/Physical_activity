# Recording daily steps

Tracking of step count can be done by using the Walking/Running specialization
of "Physical Activity". A composition for three days of daily step counts might
look something like below.
```
self_monitoring: (composition)
  walking_running: (observation)
    data:
      aggregrate: time: 2019-07-07T00:00, width: P1D, math_fn: total
        step_count: 15732
      aggregrate: time: 2019-07-08T00:00, width: P1D, math_fn: total
        step_count: 13490
      aggregrate: time: 2019-07-09T00:00, width: P1D, math_fn: total
        step_count: 10903
    protocol:
      device: (CLUSTER.device.v1)
        device_name: "FitBit Charge 3"
        type: "smartwatch"
```
We use the "Walking/Running" observation inside a "Self monitoring" composition.
For each day, we create an "Aggregate" event with a 1-day width and set the
step count data element. We can also specify the device that was used to record
the step by using the "Device" element under the protocal branch.
