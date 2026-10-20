# Hex Tile Maps with Regions: From QGIS to Tableau Public

## 📝Table of Contents
1. [What Is a Hex Tile Map](#point-1)
2. [The Challenge: Regions on a Hex Map](#point-2)
3. [Creating the Hex Map Shapefile of US States](#point-3)
4. [Map with regions](#point-4)
   - 4.a) [ Way 1: Merged hexagons (no coding)](#point-4a)
   - 4.b) [ Way 2: Generate the shapefile with Python](#point-4b)
6. [Import map into Tableau](#point-5)
7. [Drill-Down effect for map](#point-6)
8. [Author and License](#point-7)

## 1. What Is a Hex Tile Map? <a id="point-1"></a>

Hex tile maps are an excellent way to display geographic data in a simplified form while preserving the relative positions of regions or states. Each state becomes an equally sized tile, so small states (like Rhode Island or Delaware) don't get lost next to huge ones (like Texas or Alaska). Alaska and Hawaii can also be placed compactly, close to the mainland, instead of sitting far away on the map.

A classic US map can be misleading: large states with minimal data visually dominate the view, while small but important ones are barely visible. Square grids solve this problem, but hexagons fit together more tightly and better reflect the actual shape of the country.

## 2. The Challenge: Regions on a Hex Map <a id="point-2"></a>

Recently, I created a **Call Center Dashboard** in Tableau https://public.tableau.com/views/CallCenterDashboard_17482539625320/CHANNEL?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link
, where I needed this type of US map. The task turned out to be more interesting than simply drawing a standard map. The idea was to show different communication channels, with each channel having its own map, and each map divided into regions. Dashboard space was tight, so the map had to be very compact.

My first thought was the obvious one: build the hex map directly in Tableau, which even has dedicated functions for this. However, this approach has limitations. Here is what I got in Tableau:

![Figure 1: Hex map of states built in Tableau](images/figure1.png)

Because every hexagon keeps its own border, there are too many lines between states that belong to the same region. This adds unnecessary visual noise.

So I decided to aim for something like this instead:

![Figure 2: Hexagons merged into regions](images/figure2.png)

The hexagons are merged into regions (West, Midwest, South, Northeast), each with its own data. On top of that, I wanted to add a **drill-down**: clicking on a region opens a map with fewer tiles and a state-level breakdown of the data.

![Figure 3: Drill-down into the selected region](images/figure3.png)

At the high level, a manager can see in a second where the workload is highest. If they need details, one click takes them to the state level, and the dashboard stays clean and uncluttered.

In short, I needed **two maps**: one with hexagons (states) and one with regions. However, Tableau cannot merge hexagons into custom regions without internal borders. This is where my favorite tool, **QGIS**, came to the rescue, since it can produce both maps.

At this point the idea felt like a real challenge. Let's go through the process step by step, using a simplified sample dataset with number of calls by states.

## 3. Creating the Hex Map Shapefile of US States in QGIS <a id="point-3"></a>

First, install QGIS. Then create a new project: in the **Project** menu, choose **New**.
![New Project Created](files/images/Project.png)

In the bottom-right corner of the window, make sure your project uses the coordinate reference system **EPSG:4326**. 
If it doesn't, click the CRS code in the bottom-right corner, or open **Project → Properties**. In the Project Properties window, select the **CRS** tab on the left and type **EPSG:4326** into the search box.

![Project Properties with EPSG:4326 selected](files/images/CRS.png)

> **Why EPSG:4326?** EPSG:4326 (WGS84) is the standard system of latitude and longitude coordinates, and it is exactly what Tableau expects when you import a shapefile. If your shapefile uses a different coordinate reference system (for example, one measured in meters), Tableau will place the shapes in the wrong location. This is what happened in Figure 1: the tiles ended up near point (0, 0), off the coast of Africa.

> **Not familiar with Python?** You can download a ready-made `.shp` file [here](#) (or use any other open hex-map shapefile) and start from **Step [4.a) Merging hexagons (no coding)](#point-4a) **.

Open **Plugins → Python Console → Show Editor**, paste the code, change `OUT_PATH` (the path to the folder where your files will be saved) and click **Run**.

![Python Console](files/images/Python_Console.png)

Open **Plugins → Python Console → Show Editor**, paste the code and click **Run**.


-----------------------------------------------------------------------------
## 7. Author and License <a id="point-7"></a>

**Author:** Iaroslava Mizai

**Tutorial and documentation:** Licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

**Source code:** Licensed under the [MIT License](LICENSE).

You are welcome to reuse, adapt, and share this tutorial and code. When referencing or adapting the tutorial, please credit the original author and link to this repository.

If you make changes, please indicate that the material has been modified.

**Author links:**
- GitHub: https://github.com/iaroslavamizai
- Tableau Public: https://public.tableau.com/app/profile/iaroslava/vizzes
