# Modeling physical activity data from personal health devices and applications

<!-- TODO intro -->

## Background
A project in collaboration between [Region Östergötland][1] and a student group
at [Linköping university][2].

[Student project report][1] (in Swedish) with first prototype source code
available at https://github.com/alexvestin/wwv.

The application pulls data from Google Fitness (that is available on both
Android and iOS) and imports it to an openEHR platform. Currently the source
code and openEHR models are updated as a summer project at Region Östergötland.
The updated version will be periodically released as free software (MIT
license) too, at https://github.com/regionostergotland/wwv/.

[1]: https://www.regionostergotland.se/
[2]: https://liu.se/ 
[3]: http://urn.kb.se/resolve?urn=urn%3Anbn%3Ase%3Aliu%3Adiva-157977

## Repository contents
The repository currently contains the directories listed below.

### existing
Directory containing archetypes that already exist in the CKM repository and
are of interest to this project and may be used in templates or cluster slots
for modeling physical activity.

### proposals
Directory containing experimental archetypes created for the purpose of
modeling self recorded physical activity. Each batch of archetypes is stored in
its own directory with documentation and example templates.

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
the web based ADL designer at https://ehrscape.marand.si/designerv2.
