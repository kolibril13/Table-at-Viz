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

