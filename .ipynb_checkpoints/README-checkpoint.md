# Let’s Make Mapping Better
### Cam + Allie
### Friday, March 8, 2:15 – 4:30p

QGIS is a visual face for mapping with Python. So let’s use QGIS to show you the sorts of mapping things that are possible with Python.

We’d rather have a more intermediate class that is more replicable and comprehensive this year than a hard class that shows off a technical skill.


## Getting started
### If you have the virtual environment already set up on your machine
A virtual environment should be set up with the appropriate libraries already loaded. Simply use the command line to navigate into the folder (we'll let you know where that folder is at the beginning of class) and run `source env/bin/activate`.

Your terminal should now have an environment name (in this case `(env)`) appended to the command line. 

[img of this]

Troubleshooting: If you find that none of your code is running, try running the following command in the root of your project folder, while the virtual environment is running:

```
pip install -r requirements.txt
```

### If you don't have the virtual environment set up already
**Mac:** Using your terminal window, create a folder that will hold your work for this session. `cd` into that folder. Then run `python3 -m venv env`. Then run `source env/bin/activate`. Then install the following libraries: `pip -i pandas jupyterlab geopandas openpyxl`

**PC:** I have no idea... Cody help.

## What's this session all about?
OPTION 1: 

It can be challenging to make the mapping components of a projects **cohesive** - i.e. fit with the rest of your analysis and reporting steps - **collaborative** - able to be shared and edited/iterated upon by your peers and managers - and **repeatable** - able to be rerun for fact-checking and/or easily changed to repeat an analysis with slightly different parameters.

QGIS is a powerful tool that allows us to visualize and analyze geographic data with a relatively easy-to-use interface. However, it can be lacking when it comes cohesion, collaboration and repetition. 


OPTION 2:

We all know how valuable maps can be in a published story. But mapping for analysis and collaboration can be just as, if not more, valuable to your story and your sanity as a data reporter. Often times, data reporters are responsible for using their skills to build team resources and documentation, and not just for published stories. 

QGIS is a powerful tool that allows us to visualize and analyze geographic data with a relatively easy-to-use interface. However, it can be lacking when it comes **cohesion** - i.e. the ability to fit seamlessly with the rest of your analysis and reporting steps - **collaboration** - the able to be shared, edited and iterated upon by your peers and managers - and **repetition** - ability to be rerun for fact-checking purposes and/or to be easily changed in order to tweak an analysis.

In this session, we will show you examples (with QGIS and python) of how you can bring cohesion, collaboration and repetition into your map making efforts. We'll mostly use QGIS to illustrate the power of mapping for newsrooms, so that the greatest number of people can follow along, but each element we show you in QGIS will also have python companion code for those are familar with the language. 

**Why should I care about Python?** Scripting enhances the cohesion, collaboration and repetition of your mapping skills. QGIS is, under the hood, a python program. Most, if not all, of the things you can do in QGIS are do-able using various Python libraries. 

## COHESION
The ability to use mapping to create invaluable resources for your team, and to integrate mapping into the core of the reporting process.

### Creating a source of truth for spatial data in your newsroom
Mapping can be very useful in creating reference documents for teams that join togther different spatial data so that you can maintain consistency in how you report on your area. 

For example, knowing which school districts are within your city's metro area is important so you can know which school districts to pull data for, which to include in your analyses, etc. You can also do more complex spatial joins that will align multiple 

One document that has crosswalks for all nominal geographies (spatial join)

**For instance:** School ID 324321 → Facility ID 76543 → Popsicle School → Ice Cream Neighborhood → Dairy County

**Working example:** Cam did you have an example that you've created?

**QGIS walkthru**

**Python code**
[code/create-a-crosswalk.ipynb](../data/create-a-crosswalk.ipynb)

### Letting reporters know what you need in order to do your job
When File formats
Powerpoints are not acceptable forms of spatial data unless you’re really good at tracing (spoiler: no one is that good and if you are it's not worth your time to trace) (georeferencing data)

### Breaking down technical language for non-technical audiences
Census tract --> "areas"


## COLLABORATION
Pulling yourself into the reporting process early on working closely with your team to continuously develop the project.

Showing others how things are spatially related over time
 
Share your work with your team quickly and interactively.

[How to write a data summary](https://docs.google.com/document/d/16hR6wOSjXtBXDkSepsNH5hyIbg3XZgraPtFADD6yDt0/edit)

**QGIS walkthru** Buffers, clusters and Felt plugin for QGIS.

**Python code** [code/buffers-clusters-viz.ipynb](code/buffers-clusters-viz.ipynb) 


## REPETITION
Whether you’re working with a team or trying to help your future self, writing things down, being organized and having your analysis be repeatable is CRUCIAL.

### Building crosswalks (join by location in QGIS, spatial joins in python)
A reporter comes up to you and wants to know how many under-18 people live in a certain school district boundary.
Example: https://www.houstonchronicle.com/news/houston-texas/census/article/houston-neighborhood-demographics-census-data-18139717.php

### How to get Census data into city-managed geographic formats like neighborhoods

### Identifying hotspots (cluster analysis in QGIS, k-means or k-nearest neighbors in python)

### Finding surrounding properties ← buffers







