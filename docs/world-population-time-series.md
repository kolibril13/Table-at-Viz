---
title: World Population Time Series
---

# World Population Time Series

![World population time series](assets/world-population-time-series.png)

## Preparing Data

In this tutorial, we will learn how to visualize a time series of the world population. We will start with a simple CSV file that contains urban agglomeration population data from the [United Nations World Urbanization Prospects](https://population.un.org/wup/downloads?tab=Countries%20and%20Aggregates) (WUP2018).

[Download WUP2018-F22-Cities_Over_300K_Annual.csv](assets/WUP2018-F22-Cities_Over_300K_Annual.csv){ .md-button }

![CSV file screenshot](assets/csv-screenshot.png)

From this dataset, we want the following columns:

- **Latitude** and **Longitude** — the geographic coordinates
- **1950–2035** — the population values for each year

## Import into Blender

First, install the [CSV Importer](https://extensions.blender.org/add-ons/csv-importer/) add-on and drag'n'drop the dataset into Blender's viewport.

Now we will see the spreadsheet like this:

![CSV imported into Blender](assets/blender-csv-import.png)

Next, we add a background image. A good choice is an [equirectangular projection](https://en.wikipedia.org/wiki/Equirectangular_projection) of the Earth, since the latitude and longitude values from our dataset map directly to x and y coordinates in this projection.

![Equirectangular projection of the Earth](assets/equirectangular-projection.jpg)

*Source: [Wikimedia Commons — Equirectangular projection](https://en.wikipedia.org/wiki/Equirectangular_projection#/media/File:Equirectangular_projection_SW.jpg)*

Now we scale it to match the Earth's longitude and latitude, and adjust the colors with shader nodes:

![Earth background with shader nodes in Blender](assets/blender-earth-material.png)

With this in place, we continue to add the data as bar charts using Geometry Nodes:

![Bar charts on the world map in Blender](assets/blender-bar-charts.png)

To color the bars, we create a separate reference cylinder and assign a material to it. This material uses a Color Ramp driven by the Z height of each bar, so taller bars appear in warmer colors. The Geometry Nodes setup then applies this material to all instanced bars automatically.

![Bar material with height-based color ramp](assets/blender-bar-material.png)
