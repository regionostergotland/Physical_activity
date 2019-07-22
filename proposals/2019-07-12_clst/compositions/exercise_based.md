# Exercise based training

Exercise based training sessions can be recorded by using the _Physical
activity_ observation along with the _Exercise_ cluster.

Below is an example of a composition that records a hand balancing session. The
session is divided into three _Split_ events; warmup, practice and cooldown.
Each event contains a set of _Exercise_ clustes that specify various types of
exercises that were performed during the session.

```
self_monitoring (composition):
  physical_activity:
    split: time: 2019-07-22T13:12:32, width: PT19M28S
      activity_name: "Hand balancing session"
      activity_details:
        exercise:
          exercise_name: "Rear facing wrist stretch, palms down"
          number_of_repetitions: 20
          number_of_sets: 1
        exercise:
          exercise_name: "Wall facing handstand"
          duration_of_repetition: PT60S
          number_of_repetitions: 1
          number_of_sets: 2
          rest_after_set: PT20S
        ..
      comment: "Warmup."
    split: time: 2019-07-22T13:32:00, width: PT20M10S
      activity_name: "Hand balancing session"
      activity_details:
        exercise:
          exercise_name: "Freestanding handstand"
          duration_of_repetition: PT60S
          number_of_repetitions: 1
          number_of_sets: 1
          rest_after_set: PT30S
        exercise:
          exercise_name: "Freestanding handstand push ups"
          number_of_repetitions: 8
          number_of_sets: 3
          rest_after_set: PT1M
       ..
      comment: "Practice."
    split: time: 2019-07-22T13:52:10, width: PT10M01S
      activity_name: "Hand balancing session"
      activity_details:
        exercise:
          exercise_name: "Ring shoulder stands"
          duration_of_repetition: PT60S
          number_of_repetitions: 1
          number_of_sets: 1
        ..
      comment: "Cooldown."
```
