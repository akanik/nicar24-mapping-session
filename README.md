# Let’s Make Mapping Better
### Cam + Allie
### Friday, March 8, 2:15 – 4:30p

QGIS is a visual face for mapping with Python. So let’s use QGIS to show you the sorts of mapping things that are possible with Python.

We’d rather have a more intermediate class that is more replicable and comprehensive this year than a hard class that shows off a technical skill.


## Getting started
### If you have the virtual environment already set up on your machine
A virtual environment should be set up with the appropriate libraries already loaded. Simply use the command line to:
- navigate into the class folder `cd Desktop/hands_on_classes/20240308-friday-let-s-make-mapping-better`
- run `source env/bin/activate`
- Your terminal should now have an environment name (in this case `(env)`) appended to the command line.
- run `jupyter lab`

Troubleshooting: If you find that none of your code is running, try running the following command in the root of your project folder, while the virtual environment is running:

```
pip install -r requirements.txt
```

### If you don't have the virtual environment set up already
**Mac:** Using your terminal window, create a folder that will hold your work for this session. `cd` into that folder. Then run `python3 -m venv env`. Then run `source env/bin/activate`. Then install the following libraries: `pip -i pandas jupyterlab geopandas openpyxl`

**PC:** I have no idea... Cody help.

## What's this session all about?

We all know how valuable maps can be in a published story. But mapping for analysis and collaboration can be just as, if not more, valuable to your story and your sanity as a data reporter. Often times, data reporters are responsible for using their skills to build team resources and documentation, and not just for published stories. 

QGIS is a powerful tool that allows us to visualize and analyze geographic data with a relatively easy-to-use interface. However, it can be lacking when it comes **cohesion** - i.e. the ability to fit seamlessly with the rest of your analysis and reporting steps - **collaboration** - the able to be shared, edited and iterated upon by your peers and managers - and **repetition** - ability to be rerun for fact-checking purposes and/or to be easily changed in order to tweak an analysis.

In this session, we will show you examples (with QGIS and python) of how you can bring cohesion, collaboration and repetition into your map making efforts. We'll mostly use QGIS to illustrate the power of mapping for newsrooms, so that the greatest number of people can follow along, but each element we show you in QGIS will also have python companion code for those are familar with the language. 

**Why should I care about Python?** Scripting enhances the cohesion, collaboration and repetition of your mapping skills. QGIS is, under the hood, a python program. Most, if not all, of the things you can do in QGIS are do-able using various Python libraries. 

## COHESION
The ability to use mapping to create invaluable resources for your team, and to integrate mapping into the core of the reporting process.

### Creating a source of truth for spatial data in your newsroom
Mapping can be very useful in creating reference documents for teams that join togther different spatial data so that you can maintain consistency in how you report on your area. 

For example, knowing which school districts are within your city's metro area is important so you can know which school districts to pull data for, which to include in your analyses, etc. You can also do more complex spatial joins that will align multiple data files.

**For instance:** School ID 324321 → Facility ID 76543 → Popsicle School → Ice Cream Neighborhood → Dairy County

**Python code**
[code/create-a-crosswalk.ipynb](../data/create-a-crosswalk.ipynb)


## COLLABORATION
Pulling yourself into the reporting process early on working closely with your team to continuously develop the project.

Specifically, the ability to explain to your team and readers how things are spatially related and how spatial data change over time can be vital to accurately reporting on communities. Sharing your mapping work with your team quickly and interactively can help you accomplish this.

[How to write a data summary](https://docs.google.com/document/d/16hR6wOSjXtBXDkSepsNH5hyIbg3XZgraPtFADD6yDt0/edit)

**Python code** [code/buffers-clusters-viz.ipynb](code/buffers-clusters-viz.ipynb) 


## REPETITION
Whether you’re working with a team or trying to help your future self, writing things down, being organized and having your analysis be repeatable is CRUCIAL.

### Understanding how geographic shapes change over time
**Python code** [code/custom-geographies.ipynb](code/custom-geographies.ipynb)

### How to get Census data into city-managed geographic formats like neighborhoods
**Python code** [code/custom-geographies.ipynb](code/custom-geographies.ipynb)






