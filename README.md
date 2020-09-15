# Modeling physical activity data from personal health devices and applications

<!-- TODO intro -->

## Background
A project in collaboration between [Region Östergötland][1] and a student group
at [Linköping university][2].

[Student project report][3] (in Swedish) with first prototype source code
available at https://github.com/alexvestin/wwv.

The application pulls data from Google Fitness (that is available on both
Android and iOS) and imports it to an openEHR platform. 

During the summer 2019 the source
code and openEHR models related to physical exercise 
were updated as a summer project (this project repository)
at Region Östergötland. The updated version of the software 
was released as free software (MIT license),
at https://github.com/regionostergotland/wwv/.

During the spring of 2020 another student group added and
modified functionality, see
https://github.com/regionostergotland/ipforregionen

[1]: https://www.regionostergotland.se/
[2]: https://liu.se/ 
[3]: http://urn.kb.se/resolve?urn=urn%3Anbn%3Ase%3Aliu%3Adiva-157977

## Repository contents
The repository currently contains the directories listed below.

### existing
Directory containing copies of archetypes that already exist in the [openEHR CKM](https://ckm.openehr.org/ckm/) repository and
are of interest to this project and may be used in templates or cluster slots
for modeling physical activity.

### proposals
Directory containing experimental archetypes created for the purpose of
modeling self recorded physical activity. Two different modeling approaches
are explored. Each batch of archetypes is stored in
its own subdirectory with documentation and example templates.

### mindmaps
A directory to store versioned mindmaps used for requirements gathering etc.
You may need to download Xmind to view/explore/edit them https://www.xmind.net/
Note that the link-symbols in the mindmaps that lead to sources, API
descriptions etc.

 * `platforms.xmind`
   exploration of data (mostly physical activity) gathered by different
   personal health platforms (Google Fitness, Apple Health, Samsung Health,
   Withings, Garmin, Polar, Strava, MyFitnessPal etc.)
 * `sleep.xmind`
   Data about sleep in various platforms
 * `activities.xmind`
   Aggregation/mashup of activity datapoints from different health platforms.
   Useful as background for modeling.
 * `PhysicalActivityInvestigation.xmind`
   some previous example gathering and modeling thoughts, now in part
   superseeded by recent archetype modeling

## Accessing archetypes

Archetypes and templates can be cloned or downloaded from this repository and
manually loaded in to any designer application. They can also be accessed from
the web based Archetype Designer at https://tools.openehr.org/designer/#/.

## Discussion of archetypes/templates
Discussions were initially in openEHR's Slack forum for modeling, then it was
suggested that discussions move to [this project's GitHub issues][4] (as a test 
of an alternative platform) but discussions never took off after [the initial posting][5].
Now (september 2020) we'll try to restart discussions in openEHR's discussion forum at 
https://discourse.openehr.org/t/physical-activity-archetypes-exercise-steps-etc-from-apps-devices/983

[4]: https://github.com/regionostergotland/Physical_activity/issues
[5]: https://github.com/regionostergotland/Physical_activity/issues/1
