# Creating spatial joins in QGIS

By far one of the most helpful tools that QGIS can run for you with the least painful learning curve is the all-powerful **spatial join**. Also known as a "join on location", spatial joins can align different overlapping boundaries, with their attributes, to help you spot patterns, crunch numbers and create **crosswalks**.

Picking up where we left off in the [basics walkthrough](./qgis-walkthrough.md), you should have the file `md-census-tracts` open in a QGIS project that's probably named something along the lines of `bettermapping` or `allieandcamarethebest` or something like that.

If you don't have it open, feel free to open it, make any recommended reprojections, and **save your project!!!**

In order to run a spatial join, you'll need more than one file. For this walkthrough, we'll be joining Maryland's census tracts against Baltimore neighborhoods and schools to create a beautiful **data source of truth**. But a journey starts with a single step: so import `bmore-neighborhoods` and `md-public-schools` into QGIS using the guide in the basics walkthrough.

Your layer menu should now look like this:

![](./assets/joins/qgis_layermenu.png)  

All three of these are shapefiles, but they're different types of spatial data — `md-census-tracts` and `bmore-neighborhoods` are both polygons, and `md-public-schools` is a point type file. These are good attributes to keep tabs on, because it can help you shape your joining strategy (especially if you're trying to get things done quickly). 

## Pre-processing your files

### Make a spatial index

Because they're all shapefiles, before we get started with joins, we're going to create what's called a **spatial index** for each file. Creating a spatial index will help speed up the processing time on QGIS's end, which is a great thing for us. *(If you want to read more about what a spatial index is and why we need them, LINK TK.)*

In order to make one, we'll go to the top QGIS toolbar. Select `Vector` then `Data Management Tools` and `Create Spatial Index...` with the little gear icon. 

![](./assets/joins/qgis_spatialindex.png) 

It should open up a new window called **"Create Spatial Index"**, which is a pretty straightforward looking menu (compared to some other ones that QGIS has). The main focus is the `input layer` option, which likely has your active layer already selected. In my case, it's "`Neighborhood [EPSG:2248]`". 

![](./assets/joins/qgis_spatindwindow.png)

From here, all you have to do is hit **Run**. Repeat this process for the other layers to create spatial indexes for each! Nothing overt will happen — no new layers or files will be added — but trust the process. :)


### Making your layers make sense
There's no need to make working with QGIS any more confusing for yourself, so let's **rename our layers**. This won't change the file name, and it's pretty superficial, but it helps when we'll be running through spatial joins and selecting different layers as inputs. 

To change your layer names, select a layer and hit the `enter` or `return` key. Like using a code editor, it'll highlight and become editable, and you can rename the layers. Here are my recommended renaming options, though do what makes the most sense to you:
* `Neighborhood` to `bmore-neighborhoods`
* `EDGE_GEOCODE_PUBLICSCH_2223_Maryland` to `md-schools`
* `tl_2022_24_tract` to `md-tracts`

Keeping it standardized like this helps us to stay organized (and it makes the walkthrough process easier). If there's a better renaming option that you like more (like, say, renaming `Neighborhood` to `all_the_places_where_allie_and_cam_are_super_cool`), feel free to do that. 

We're also going to **add our feature count** to the layer menu. Having your feature count visible (as mentioned in the basics walkthrough) helps to gut check the data, and with spatial joins, it can help you ID whether something has gone awry.

To do that, we'll stick with the layer menu in the bottom left corner, and select all of the layers by clicking the first layer, holding shift, and clicking the last layer in the list. Then, right click, and select **Show Feature Count** toward the top of the menu:

![](./assets/joins/qgis_featurecount_menu.png)

It should make some numbers magically appear next to each of your beautifully-renamed layers, like this:

![](./assets/joins/qgis_featurect_layer.png)

In this case, you have **279** features for `bmore-neighborhoods`, **1425** features for `md-schools`, and **1475** features for `md-tracts`. 


### Thinking through the join
In order to do the join, you've gotta _think_ like the join. You have to _be_ the join. So let's talk about what goes on when things are spatially joined together!

Typically when you do a join in SQL or Python, for example, you'll have a shared field to join against. Like if you were trying to match up a list of albums and artists with a list of songs and those artists, your data might look like this initially:

<table>
<tr>
<th>albums</th>
<th>songs</th>
</tr>
<tr>

<td>

| artist_name | album_name |
|--|--|
| Stevie Wonder | Songs In The Key of Life |
| Miles Davis | Kind of Blue |
| B-52s | Wild Planet |
| Janelle Monáe | The Age of Pleasure |
| Taylor Swift | Midnights |

</td><td>

| artist_name | song_name |
|--|--|
| B-52s | Private Idaho |
| Janelle Monáe | Float |
| Stevie Wonder | Sir Duke |
| Taylor Swift | Lavender Haze |
| Miles Davis | Blue in Green|

</td></tr> </table>

And you'd have a goal of maybe making it like this, by matching the shared field between the two datasets (which in this case is `artist_name`):
<table>
<tr>
<th>artists_music</th>
</tr>
<tr>
<td>

| artist_name | album_name | song_name |
|--|--|--|
| Stevie Wonder | Songs In The Key of Life | Sir Duke |
| Miles Davis | Kind of Blue | Blue in Green |
| B-52s | Wild Planet | Private Idaho |
| Janelle Monáe | The Age of Pleasure | Float |
| Taylor Swift | Midnights | Lavender Haze|

</td></tr> </table>

This is also a phenomenon known as a **one-to-one** join — each row has one corresponding row that gets matched. For the join to be considered **one-to-many**, your original data might look like this:

<table>
<tr>
<th>albums</th>
<th>songs</th>
</tr>
<tr>

<td>

| artist_name | album_name |
|--|--|
| Stevie Wonder | Songs In The Key of Life |
| Miles Davis | Kind of Blue |
| B-52s | Wild Planet |
| Janelle Monáe | The Age of Pleasure |
| Taylor Swift | Midnights |

</td><td>

| artist_name | song_name |
|--|--|
| B-52s | Private Idaho |
| Janelle Monáe | Float |
| Stevie Wonder | Sir Duke |
| Taylor Swift | Lavender Haze |
| Miles Davis | Blue in Green|
| Janelle Monáe | Champagne Shit |
| Taylor Swift | Karma |
| Stevie Wonder | As |
| B-52s | Give Me Back My Man |
| B-52s | Quiche Lorraine|

</td></tr> </table>

And your end result, after a join, would look something like this:

<table>
<tr>
<th>artists_music</th>
</tr>
<tr>
<td>

| artist_name | album_name | song_name |
|--|--|--|
| Stevie Wonder | Songs In The Key of Life | Sir Duke |
| Stevie Wonder | Songs In The Key of Life | As |
| Miles Davis | Kind of Blue | Blue in Green |
| B-52s | Wild Planet | Private Idaho |
| B-52s | Wild Planet | Quiche Lorraine |
| B-52s | Wild Planet | Give Me Back My Man |
| Janelle Monáe | The Age of Pleasure | Float |
| Janelle Monáe | The Age of Pleasure | Champagne Shit |
| Taylor Swift | Midnights | Lavender Haze|
| Taylor Swift | Midnights | Karma|

</td></tr> </table>

Your end result will be larger than the two datasets individually, because a **one to many** join matches values from table one and table two and adds rows for each matching value between table two and table one. (TLDR, it uses the matching field (in this case `artist_name`) from table one as an anchor, and matches up every row that has matching data (`song_name`) from table two, and duplicates all existing data in table one (`album_name`) for each row that has matching table two data.)

Again... _be_ the join. Think like the join. 

## Executing spatial joins

For spatial joins, like standard joins, you'll want to think about what your end goal is. The way I do this is by thinking about my reporting question and what I'm trying to answer.

With the data we have on deck in our layer menu, we can try and work through this question ourselves. If the goal is **to create a spatial source of truth**, which has a bunch of datasets joined against each other into one mega-file, we'll probably want to do two different kinds of joins:
1. If the question is `"Which Census tracts correspond to each neighborhood in Baltimore?`", a **one to one (largest overlap)** join is probably best. In this case, our `md-tracts` layer will be our "table one" (our "`albums`" table) and our `bmore-neighborhoods` will be our "table two" (our "`songs`" table). This way, each Census tract is able to be matched up against a corresponding neighborhood boundary. We also could do a **one to many** join, because not every Census tract neatly corresponds to a matching neighborhood boundary — sometimes one Census tract could span two or three neighborhood boundaries, for example.
2. For the question of `"What Census tracts have schools, and which schools are they?"`, we'll want to do a **one to one (first matching)** join as well. Because the `md-schools` file is a point-type shapefile, it's unlikely that it'll span multiple Census tracts, which makes a one-to-one join a pretty solid choice. It'll also turn up `NULL` values for Census tracts that don't have an overlapping school, which can later be processed in a way for visualizations or othe analysis.

A special third question, which will be the basis of our "spatial source of truth":

3. For the question of `"What neighborhoods and Census tracts are Maryland schools located in?"`, we'll want to do a **one to one** join as well. For the same reason as #2, we'll be joining `bmore-neighborhoods` and (separately) `md-tracts` against `md-schools`, and because `md-schools` is a point-type file, we don't have to worry about it pulling multiple matches from the neighborhood and tract files. (*generally.*)

This all comes down to making things **collaborative** and **cohesive** — we're often working with reporters to tackle questions they (and our readers) have about data. By breaking down spatial processing and data work into a question that we're trying to answer instead of a task we're trying to execute, it can help us explain and work through strategies better with the larger team! 











* predicates
* what is your end goal?


