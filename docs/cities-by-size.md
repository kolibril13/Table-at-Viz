---
title: Cities by Size
---

# Cities by Size

In this tutorial, we will learn how to visualize German cities by population size in Blender 5.0.1.

Here's how the final result looks as an image:

![Cities by size](assets/cities-by-size.png)

And here as a video:

<video controls width="100%">
  <source src="../assets/cities_by_size.mp4" type="video/mp4">
</video>

[Download cities_by_size.blend](assets/cities_by_size.blend){ .md-button }

## Preparing Data

We start with a CSV file that contains German cities with more than 90,000 inhabitants, sourced from the [Statistisches Bundesamt](https://www.destatis.de) (as of 31.12.2023).

From this dataset, we want the following columns:

- **Latitude** and **Longitude** — the geographic coordinates
- **Population** — the number of inhabitants per city

## Import into Blender

First, install the [CSV Importer](https://extensions.blender.org/add-ons/csv-importer/) add-on and drag'n'drop the dataset into Blender's viewport.

Next, we add a background map of Germany. Similar to the world population tutorial, we use an equirectangular projection so that latitude and longitude values map directly to x and y coordinates.

We scale the map to match the geographic coordinates and adjust the colors with shader nodes.

With this in place, we add the data as circles using Geometry Nodes. Each city is represented by a circle whose radius corresponds to its population.

To color the circles, we create a reference object and assign a material to it. The Geometry Nodes setup then applies this material to all instances automatically.

We add a Sun light object for lighting and switch to the Cycles render engine.

Finally, we add a separate scene for the overlay — showing the legend, title, data source, and attribution. This overlay is rendered separately from the main 3D scene and then combined in DaVinci Resolve.

[Download cities_by_size.blend](assets/cities_by_size.blend){ .md-button }

If you come up with your own creations and post them online, you're welcome to tag me on [Bluesky](https://bsky.app/profile/kolibril13.bsky.social)!
