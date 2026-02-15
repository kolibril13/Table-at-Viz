---
title: Network Visualization
---

# Network Visualization

In this tutorial, we will learn how to visualize a **network** in Blender 5.0.1.

Here's how the final result looks as an image:

![Network visualization](assets/network-visualization.png)

[Download network-visualization.blend](assets/network-visualization.blend){ .md-button }

## What the visualization shows

This visualization maps the dependency structure of Euclid's *Elements* across all 13 books. Each proposition in a book can reference definitions, postulates, common notions, and propositions from the same or earlier books. The more references a proposition accumulates (counted recursively), the taller its bar appears. Lines connect each proposition to its dependencies, so the web of logical connections across all books is revealed.

## Preparing Data

!!! warning "Advanced project"
    This is quite an advanced project, so take it as inspiration for the overall steps. It might be a difficult endeavour to reproduce this 100%.

The dependency data was extracted from Euclid's *Elements*. A full reference of the original text is available here: [Euclid's Elements (PDF)](https://farside.ph.utexas.edu/books/Euclid/Elements.pdf).

<details>
<summary>Dependency graph data (click to expand)</summary>

```json
{
  "book1": {
    "D1.1": [],
    "D1.2": [],
    "D1.3": [],
    "D1.4": [],
    "D1.5": [],
    "D1.6": [],
    "D1.7": [],
    "D1.8": [],
    "D1.9": [],
    "D1.10": [],
    "D1.11": [],
    "D1.12": [],
    "D1.13": [],
    "D1.14": [],
    "D1.15": [],
    "D1.16": [],
    "D1.17": [],
    "D1.18": [],
    "D1.19": [],
    "D1.20": [],
    "D1.21": [],
    "D1.22": [],
    "D1.23": [],
    "Prop1.1": ["Post.3", "Post.3", "Post.1", "CN.1", "D1.15"],
    "Prop1.2": ["Post.1", "Prop1.1", "Post.2", "Post.3", "Post.3", "CN.1", "CN.3", "D1.15"],
    "Prop1.3": ["Prop1.2", "Post.3", "CN.1", "D1.15"],
    "Prop1.4": ["Post.1", "CN.4"],
    "Prop1.5": ["Post.2", "Prop1.3", "Post.1", "Prop1.4", "Prop1.4", "CN.3"],
    "Prop1.6": ["Prop1.3", "Post.1", "Prop1.4", "CN.5"],
    "Prop1.7": ["Post.1", "Prop1.5", "Prop1.5", "CN.5"],
    "Prop1.8": ["Prop1.7", "CN.4"],
    "Prop1.9": ["Prop1.3", "Prop1.1", "Prop1.8"],
    "Prop1.10": ["Prop1.1", "Prop1.9", "Prop1.4"],
    "Prop1.11": ["Prop1.3", "Prop1.1", "Prop1.8", "D1.10"],
    "Prop1.12": ["Post.3", "Prop1.10", "Prop1.8", "D1.10"],
    "Prop1.13": ["Prop1.11", "CN.1", "CN.2", "D1.10"],
    "Prop1.14": ["Prop1.13", "CN.1", "CN.3", "Post.4"],
    "Prop1.15": ["Prop1.13", "Prop1.13", "CN.1", "CN.3", "Post.4"],
    "Prop1.16": ["Prop1.10", "Prop1.3", "Prop1.15", "Prop1.4"],
    "Prop1.17": ["Prop1.16", "Prop1.13"],
    "Prop1.18": ["Prop1.3", "Prop1.16", "Prop1.5"],
    "Prop1.19": ["Prop1.5", "Prop1.18"],
    "Prop1.20": ["Prop1.3", "Prop1.5", "Prop1.19"],
    "Prop1.21": ["Prop1.20", "Prop1.20", "Prop1.16"],
    "Prop1.22": ["Prop1.20", "Prop1.3"],
    "Prop1.23": ["Prop1.22", "Prop1.8"],
    "Prop1.24": ["Prop1.23", "Prop1.3", "Prop1.4", "Prop1.5", "Prop1.19", "Post.1"],
    "Prop1.25": ["Prop1.4", "Prop1.24"],
    "Prop1.26": ["Prop1.3", "Prop1.4", "Prop1.4", "Prop1.3", "Prop1.4", "Prop1.16", "Prop1.4"],
    "Prop1.27": ["Prop1.16", "D1.23"],
    "Prop1.28": ["Prop1.15", "Prop1.27", "Prop1.13", "Prop1.27", "Post.4"],
    "Prop1.29": ["Prop1.13", "Post.5", "Prop1.15", "Prop1.13", "D1.23"],
    "Prop1.30": ["Prop1.29", "Prop1.29", "Prop1.27"],
    "Prop1.31": ["Prop1.23", "Prop1.27"],
    "Prop1.32": ["Prop1.31", "Prop1.29", "Prop1.29", "Prop1.13"],
    "Prop1.33": ["Prop1.29", "Prop1.4", "Prop1.27"],
    "Prop1.34": ["Prop1.29", "Prop1.29", "Prop1.26", "Prop1.4"],
    "Prop1.35": ["Prop1.34", "Prop1.34", "Prop1.29", "Prop1.4"],
    "Prop1.36": ["Prop1.34", "Prop1.33", "Prop1.34", "Prop1.35", "Prop1.34"],
    "Prop1.37": ["Prop1.31", "Prop1.31", "Prop1.35", "Prop1.34", "Prop1.34"],
    "Prop1.38": ["Prop1.31", "Prop1.31", "Prop1.36", "Prop1.34"],
    "Prop1.39": ["Prop1.31", "Prop1.37"],
    "Prop1.40": ["Prop1.31", "Prop1.38"],
    "Prop1.41": ["Prop1.37", "Prop1.34"],
    "Prop1.42": ["Prop1.10", "Prop1.23", "Prop1.31", "Prop1.31", "Prop1.38", "Prop1.41"],
    "Prop1.43": ["Prop1.34", "Prop1.34"],
    "Prop1.44": ["Prop1.42", "Prop1.31", "Prop1.31", "Prop1.29", "Post.5", "Prop1.31", "Prop1.43", "Prop1.15", "Prop1.23"],
    "Prop1.45": ["Prop1.42", "Prop1.44", "Prop1.29", "Prop1.14", "Prop1.29", "Prop1.29", "Prop1.14", "Prop1.34", "Prop1.34", "Prop1.30", "Prop1.33"],
    "Prop1.46": ["Prop1.11", "Prop1.3", "Prop1.31", "Prop1.31", "Prop1.34", "Prop1.29", "Prop1.34", "D1.22"],
    "Prop1.47": ["Prop1.46", "Prop1.31", "Prop1.14", "Prop1.4", "Prop1.41", "Prop1.41", "Post.4"],
    "Prop1.48": ["Prop1.11", "Prop1.3", "Prop1.47", "Prop1.8"]
  },
  "book2": {
    "D2.1": [],
    "D2.2": [],
    "Prop2.1": ["Prop1.11", "Prop1.3", "Prop1.31", "Prop1.31", "Prop1.34"],
    "Prop2.2": ["Prop1.46", "Prop1.31"],
    "Prop2.3": ["Prop1.46", "Prop1.31"],
    "Prop2.4": ["Prop1.46", "Prop1.31", "Prop1.31", "Prop1.29", "Prop1.5", "Prop1.6", "Prop1.34", "Prop1.29", "Prop1.34", "Prop1.34", "Prop1.43"],
    "Prop2.5": ["Prop1.46", "Prop1.31", "Prop1.31", "Prop1.31", "Prop1.43", "Prop1.36", "Prop1.10"],
    "Prop2.6": ["Prop1.46", "Prop1.31", "Prop1.31", "Prop1.31", "Prop1.36", "Prop1.43", "Post.2", "Prop1.10"],
    "Prop2.7": ["Prop1.46", "Prop1.43"],
    "Prop2.8": ["Prop1.3", "Prop1.46", "Prop1.34", "Prop1.34", "Prop1.36", "Prop1.43", "Prop1.36", "Prop1.43"],
    "Prop2.9": ["Prop1.11", "Prop1.3", "Prop1.31", "Prop1.31", "Prop1.5", "Prop1.32", "Prop1.29", "Prop1.32", "Prop1.6", "Prop1.29", "Prop1.32", "Prop1.6", "Prop1.47", "Prop1.47", "Prop1.34", "Prop1.47", "Prop1.47"],
    "Prop2.10": ["Prop1.11", "Prop1.3", "Prop1.31", "Prop1.31", "Prop1.29", "Post.5", "Prop1.5", "Prop1.32", "Prop1.15", "Prop1.29", "Prop1.6", "Prop1.34", "Prop1.6", "Prop1.47", "Prop1.47", "Prop1.34", "Prop1.47", "Prop1.47", "Prop1.10"],
    "Prop2.11": ["Prop1.46", "Prop1.10", "Prop1.3", "Prop1.46", "Prop2.6", "Prop1.47", "Post.1", "Post.2"],
    "Prop2.12": ["Prop1.12", "Prop2.4", "Prop1.47", "Prop1.47"],
    "Prop2.13": ["Prop1.12", "Prop2.7", "Prop1.47", "Prop1.47"],
    "Prop2.14": ["Prop1.45", "Prop1.3", "Prop1.10", "Prop2.5", "Prop1.47"]
  },
  "book3": {
    "D3.1": [],
    "D3.2": [],
    "D3.3": [],
    "D3.4": [],
    "D3.5": [],
    "D3.6": [],
    "D3.7": [],
    "D3.8": [],
    "D3.9": [],
    "D3.10": [],
    "D3.11": [],
    "Prop3.1": ["Prop1.9", "Prop1.11", "Prop1.9", "Prop1.8", "D1.10"],
    "Prop3.2": ["Prop3.1", "Prop1.5", "Prop1.16", "Prop1.5", "Prop1.19"],
    "Prop3.3": ["Prop3.1", "Prop1.8", "Prop1.5", "Prop1.26", "D1.10"],
    "Prop3.4": ["Prop3.1", "Prop3.3", "Prop3.3"],
    "Prop3.5": ["Post.3", "Post.3", "Post.3"],
    "Prop3.6": ["Post.3", "Post.1", "Post.3"],
    "Prop3.7": ["Prop1.20", "Prop1.24", "Prop1.20", "Prop1.23", "Prop1.4", "Prop3.1"],
    "Prop3.8": ["Prop3.1", "Prop1.20", "Prop1.24", "Prop1.20", "Prop1.21", "Prop1.23", "Prop1.4", "Prop3.1"],
    "Prop3.9": ["Prop1.10", "Prop1.8", "Prop3.1", "D1.10"],
    "Prop3.10": ["Prop1.11", "Prop3.1", "Prop3.1", "Prop3.5", "Prop1.10"],
    "Prop3.11": ["Prop3.1", "Prop3.1", "Prop1.20"],
    "Prop3.12": ["Prop3.1", "Prop3.1", "Prop1.20"],
    "Prop3.13": ["Prop3.1", "Prop3.1", "Prop3.11", "Prop3.2", "D3.3"],
    "Prop3.14": ["Prop1.12", "Prop3.3", "Prop1.47", "Prop1.47", "Prop1.47", "Prop1.47", "D3.4", "Prop3.1"],
    "Prop3.15": ["Prop3.1", "Prop1.12", "Prop1.3", "Prop1.11", "Prop3.14", "Prop1.20", "Prop1.24", "D3.5"],
    "Prop3.16": ["Prop1.11", "Prop1.5", "Prop1.17", "Prop1.12", "Prop1.19", "Prop3.2", "Prop3.1"],
    "Prop3.17": ["Prop3.1", "Prop1.11", "Prop1.4", "Prop3.16"],
    "Prop3.18": ["Prop3.1", "Prop1.12", "Prop1.17", "Prop1.19"],
    "Prop3.19": ["Prop1.11", "Prop3.18", "Prop3.1"],
    "Prop3.20": ["Prop1.5", "Prop1.32", "Prop3.1", "Post.2"],
    "Prop3.21": ["Prop3.1", "Prop3.20"],
    "Prop3.22": ["Prop1.32", "Prop3.21", "Prop3.21"],
    "Prop3.23": ["Prop1.16", "D3.11"],
    "Prop3.24": ["Prop3.10", "CN.4", "Prop3.23"],
    "Prop3.25": ["Prop1.10", "Prop1.11", "Prop1.23", "Prop1.6", "Prop1.4", "Prop3.9", "Prop1.6", "Prop1.23", "Post.2", "Post.3"],
    "Prop3.26": ["Prop1.4", "Prop3.24", "D3.11", "Prop3.1"],
    "Prop3.27": ["Prop1.23", "Prop3.26", "Prop3.20", "Post.3"],
    "Prop3.28": ["Prop3.1", "Prop1.8", "Prop3.26", "D3.1"],
    "Prop3.29": ["Prop3.1", "Prop3.27", "Prop1.4", "D3.1"],
    "Prop3.30": ["Prop1.10", "Prop1.11", "Prop1.4", "Prop1.28"],
    "Prop3.31": ["Prop1.5", "Prop1.5", "Prop1.32", "Prop1.17", "Prop3.22", "D1.10", "Post.3", "Post.2"],
    "Prop3.32": ["Prop1.11", "Prop3.19", "Prop3.31", "Prop1.32", "Prop3.22", "Prop1.13"],
    "Prop3.33": ["Prop1.23", "Prop1.11", "Prop1.10", "Prop1.11", "Prop1.4", "Prop3.1", "Prop3.16", "Prop3.32", "Prop1.23", "Prop1.10", "Prop3.16", "Prop3.31", "Prop1.23", "Prop1.11", "Prop1.10", "Prop1.10", "Prop1.4", "Prop3.1", "Prop3.16", "Prop3.32", "Post.3"],
    "Prop3.34": ["Prop1.23", "Prop1.32", "Prop3.1", "Prop1.11"],
    "Prop3.35": ["Prop3.1", "Prop1.12", "Prop3.3", "Prop2.5", "Prop1.47", "Prop1.47", "Post.3"],
    "Prop3.36": ["Prop3.18", "Prop2.6", "Prop1.47", "Prop1.12", "Prop3.18", "Prop3.3", "Prop2.6", "Prop1.47", "Prop1.47", "Prop1.47", "Prop3.1"],
    "Prop3.37": ["Prop3.17", "Prop3.18", "Prop3.36", "Prop1.8", "Prop3.16", "Prop3.1"]
  },
  "book4": {
    "D4.1": [],
    "D4.2": [],
    "D4.3": [],
    "D4.4": [],
    "D4.5": [],
    "D4.6": [],
    "D4.7": [],
    "Prop4.1": ["Prop1.3", "Prop3.1", "Post.3"],
    "Prop4.2": ["Prop1.23", "Prop3.32", "Prop1.32", "Prop3.1", "Prop1.11"],
    "Prop4.3": ["Prop3.1", "Prop1.23", "Prop3.1", "Prop3.18", "Prop1.32", "Prop1.13", "Prop1.32", "Post.2", "Prop1.11"],
    "Prop4.4": ["Prop1.9", "Prop1.12", "Prop1.26", "Prop3.16"],
    "Prop4.5": ["Prop1.10", "Prop1.11", "Prop1.4", "Prop1.4", "Post.3", "Post.3", "Post.3"],
    "Prop4.6": ["Prop1.4", "Prop3.31", "D1.22", "Prop3.1", "Prop1.11"],
    "Prop4.7": ["Prop3.18", "Prop1.29", "Prop1.30", "Prop1.34", "Prop1.34", "Prop1.34", "D1.22", "Prop3.1", "Prop1.11"],
    "Prop4.8": ["Prop1.10", "Prop1.31", "Prop1.34", "Prop3.16", "Post.3"],
    "Prop4.9": ["Prop1.8", "Prop1.6", "Post.3"],
    "Prop4.10": ["Prop2.11", "Prop4.1", "Prop4.5", "Prop3.37", "Prop3.32", "Prop1.32", "Prop1.5", "Prop1.6", "Prop1.5", "Post.3"],
    "Prop4.11": ["Prop4.10", "Prop4.2", "Prop1.9", "Prop3.26", "Prop3.29", "Prop3.27"],
    "Prop4.12": ["Prop3.11", "Prop3.1", "Prop3.1", "Prop3.18", "Prop1.47", "Prop1.8", "Prop1.8", "Prop3.27", "Prop1.26", "Prop1.11"],
    "Prop4.13": ["Prop1.9", "Prop1.4", "Prop1.12", "Prop1.26", "Prop3.16", "Post.3"],
    "Prop4.14": ["Prop1.9", "Prop1.6"],
    "Prop4.15": ["Prop3.1", "Prop1.5", "Prop1.32", "Prop1.13", "Prop1.15", "Prop3.26", "Prop3.29", "Prop3.27", "Prop1.11", "Post.3", "Post.2"],
    "Prop4.16": ["Prop4.2", "Prop4.11", "Prop3.30", "Prop4.1"]
  },
  "book5": {
    "D5.1": [],
    "D5.2": [],
    "D5.3": [],
    "D5.4": [],
    "D5.5": [],
    "D5.6": [],
    "D5.7": [],
    "D5.8": [],
    "D5.9": [],
    "D5.10": [],
    "D5.11": [],
    "D5.12": [],
    "D5.13": [],
    "D5.14": [],
    "D5.15": [],
    "D5.16": [],
    "D5.17": [],
    "D5.18": [],
    "Prop5.1": [],
    "Prop5.2": [],
    "Prop5.3": ["Prop5.2"],
    "Prop5.4": ["Prop5.3", "D5.5"],
    "Prop5.5": ["Prop5.1"],
    "Prop5.6": ["Prop5.2"],
    "Prop5.7": ["D5.5"],
    "Prop5.8": ["Prop5.1", "D5.4", "D5.7", "D5.5"],
    "Prop5.9": ["Prop5.8", "Prop5.8"],
    "Prop5.10": ["Prop5.7", "Prop5.8", "Prop5.7", "Prop5.8"],
    "Prop5.11": ["D5.5"],
    "Prop5.12": ["Prop5.1", "D5.5"],
    "Prop5.13": ["D5.7", "D5.5", "D5.7"],
    "Prop5.14": ["Prop5.8", "Prop5.10"],
    "Prop5.15": ["Prop5.7", "Prop5.12"],
    "Prop5.16": ["Prop5.15", "Prop5.11", "Prop5.15", "Prop5.11", "Prop5.14", "D5.5"],
    "Prop5.17": ["Prop5.1", "Prop5.1", "Prop5.2", "D5.5"],
    "Prop5.18": ["Prop5.17", "Prop5.11", "Prop5.14"],
    "Prop5.19": ["Prop5.16", "Prop5.17", "Prop5.16"],
    "Prop5.20": ["Prop5.8", "Prop5.7", "Prop5.13", "Prop5.10"],
    "Prop5.21": ["Prop5.8", "Prop5.7", "Prop5.13", "Prop5.10"],
    "Prop5.22": ["Prop5.4", "Prop5.20", "D5.5"],
    "Prop5.23": ["Prop5.15", "Prop5.11", "Prop5.16", "Prop5.15", "Prop5.11", "Prop5.15", "Prop5.11", "Prop5.16", "Prop5.21", "D5.5"],
    "Prop5.24": ["Prop5.7", "Prop5.22", "Prop5.18", "Prop5.22"],
    "Prop5.25": ["Prop5.19"]
  },
  "book6": {
    "D6.1": [],
    "D6.2": [],
    "D6.3": [],
    "Prop6.1": ["Prop1.38", "Prop5.11", "Prop1.34", "Prop5.15", "D5.5", "Prop5.5", "Prop5.4"],
    "Prop6.2": ["Prop1.38", "Prop5.7", "Prop6.1", "Prop5.11", "Prop6.1", "Prop5.11", "Prop5.9", "Prop1.39"],
    "Prop6.3": ["Prop1.29", "Prop1.29", "Prop1.6", "Prop6.2", "Prop6.2", "Prop5.11", "Prop5.9", "Prop1.5", "Prop1.29"],
    "Prop6.4": ["Prop1.17", "Prop1.28", "Prop1.28", "Prop1.34", "Prop6.2", "Prop5.16", "Prop6.2", "Prop6.2", "Prop5.22", "CN.5"],
    "Prop6.5": ["Prop1.23", "Prop1.32", "Prop6.4", "Prop5.11", "Prop5.9", "Prop1.8", "Prop1.4"],
    "Prop6.6": ["Prop1.23", "Prop1.32", "Prop6.4", "Prop5.11", "Prop5.9", "Prop1.4", "Prop1.32"],
    "Prop6.7": ["Prop1.23", "Prop1.32", "Prop6.4", "Prop5.11", "Prop5.9", "Prop1.5", "Prop1.13", "Prop1.32", "Prop1.17", "Prop1.32"],
    "Prop6.8": ["Prop1.12", "Prop1.32", "Prop6.4", "Prop1.32", "Prop6.4", "D6.1"],
    "Prop6.9": ["Prop1.3", "Prop1.31", "Prop6.2"],
    "Prop6.10": ["Prop1.31", "Prop1.34", "Prop6.2", "Prop6.2"],
    "Prop6.11": ["Prop1.3", "Prop1.31", "Prop6.2"],
    "Prop6.12": ["Prop1.3", "Prop1.31", "Prop6.2"],
    "Prop6.13": ["Prop1.10", "Prop1.11", "Prop3.31", "Prop6.8"],
    "Prop6.14": ["Prop1.14", "Prop5.7", "Prop6.1", "Prop6.1", "Prop5.11", "Prop5.9"],
    "Prop6.15": ["Prop1.14", "Prop5.7", "Prop6.1", "Prop6.1", "Prop5.9"],
    "Prop6.16": ["Prop1.11", "Prop1.3", "Prop6.14", "Prop6.14"],
    "Prop6.17": ["Prop1.3", "Prop6.16", "Prop6.16"],
    "Prop6.18": ["Prop1.23", "Prop1.32", "Prop6.4", "Prop1.23", "Prop1.32", "Prop6.4", "D6.1"],
    "Prop6.19": ["Prop6.11", "Prop5.16", "Prop6.15", "Prop6.1", "D5.9"],
    "Prop6.20": ["Prop6.6", "Prop6.4", "Prop5.22", "Prop6.6", "Prop1.32", "Prop6.4", "Prop5.22", "Prop6.1", "Prop5.12", "Prop5.16", "Prop5.12", "Prop6.14", "D6.1"],
    "Prop6.21": ["D6.1", "D6.1"],
    "Prop6.22": ["Prop6.11", "Prop5.22", "Prop5.19", "Prop6.12", "Prop5.11", "Prop5.9", "Prop6.18", "Prop6.21"],
    "Prop6.23": ["Prop1.14", "Prop6.12", "Prop6.1", "Prop6.1", "Prop5.22"],
    "Prop6.24": ["Prop6.2", "Prop6.2", "Prop5.18", "Prop5.16", "Prop1.29", "Prop1.32", "Prop6.4", "Prop5.22", "Prop6.21", "D6.1"],
    "Prop6.25": ["Prop1.44", "Prop1.45", "Prop1.14", "Prop6.13", "Prop6.18", "Prop6.19", "Prop6.1", "Prop5.16"],
    "Prop6.26": ["Prop1.31", "Prop6.24", "Prop5.9"],
    "Prop6.27": ["Prop1.10", "Prop6.26", "Prop1.43", "Prop6.1"],
    "Prop6.28": ["Prop1.10", "Prop6.18", "Prop6.1", "Prop6.25", "Prop6.21", "Prop1.3", "Prop6.21", "Prop6.26", "Prop1.43", "Prop6.1", "Prop6.24"],
    "Prop6.29": ["Prop1.10", "Prop6.18", "Prop6.25", "Prop1.3", "Prop6.21", "Prop6.26", "Prop6.1", "Prop1.43", "Prop6.24"],
    "Prop6.30": ["Prop1.46", "Prop6.29", "Prop6.14", "Prop5.14"],
    "Prop6.31": ["Prop1.12", "Prop6.8", "Prop6.19", "Prop5.24", "Prop5.9", "D6.1"],
    "Prop6.32": ["Prop1.29", "Prop6.6", "Prop1.32", "Prop1.14"],
    "Prop6.33": ["Prop3.27", "Prop3.27", "Prop5.15", "Prop3.20", "D5.5"]
  },
  "book7": {
    "D7.1": [],
    "D7.2": [],
    "D7.3": [],
    "D7.4": [],
    "D7.5": [],
    "D7.6": [],
    "D7.7": [],
    "D7.8": [],
    "D7.9": [],
    "D7.10": [],
    "D7.11": [],
    "D7.12": [],
    "D7.13": [],
    "D7.14": [],
    "D7.15": [],
    "D7.16": [],
    "D7.17": [],
    "D7.18": [],
    "D7.19": [],
    "D7.20": [],
    "D7.21": [],
    "D7.22": [],
    "Prop7.1": [],
    "Prop7.2": ["Prop7.1"],
    "Prop7.3": ["Prop7.2", "Prop7.2", "Prop7.2", "Prop7.2", "Prop7.2", "Prop7.2"],
    "Prop7.4": ["Prop7.2"],
    "Prop7.5": [],
    "Prop7.6": ["Prop7.5"],
    "Prop7.7": ["Prop7.5"],
    "Prop7.8": ["Prop7.5", "Prop7.5"],
    "Prop7.9": ["Prop7.5", "Prop7.6"],
    "Prop7.10": ["Prop7.9", "Prop7.9", "Prop7.5", "Prop7.6"],
    "Prop7.11": ["Prop7.7", "Prop7.8", "D7.20"],
    "Prop7.12": ["Prop7.5", "Prop7.6", "D7.20"],
    "Prop7.13": ["Prop7.9", "Prop7.10", "D7.20"],
    "Prop7.14": ["Prop7.13", "Prop7.13", "Prop7.13"],
    "Prop7.15": ["Prop7.12", "D7.20"],
    "Prop7.16": ["Prop7.15", "D7.15"],
    "Prop7.17": ["Prop7.13", "D7.15", "D7.20"],
    "Prop7.18": ["Prop7.16", "Prop7.17"],
    "Prop7.19": ["Prop7.17", "Prop7.18", "Prop5.9", "Prop5.7", "Prop7.17", "Prop7.18"],
    "Prop7.20": ["Prop7.13", "Prop7.12", "Prop7.4", "Prop7.13", "D7.20"],
    "Prop7.21": ["Prop7.20", "Prop7.16", "Prop7.16"],
    "Prop7.22": ["Prop7.17", "D7.15"],
    "Prop7.23": [],
    "Prop7.24": ["Prop7.23", "Prop7.16", "Prop6.15", "Prop7.21", "Prop7.20", "D7.15"],
    "Prop7.25": ["Prop7.24"],
    "Prop7.26": ["Prop7.24", "Prop7.24"],
    "Prop7.27": ["Prop7.25", "Prop7.25", "Prop7.25", "Prop7.26"],
    "Prop7.28": [],
    "Prop7.29": [],
    "Prop7.30": ["Prop7.29", "Prop7.19", "Prop7.21", "Prop7.20", "D7.15"],
    "Prop7.31": [],
    "Prop7.32": ["Prop7.31"],
    "Prop7.33": ["Prop7.22", "Prop7.3", "Prop7.15", "Prop7.15", "Prop7.19", "Prop5.13", "D7.20"],
    "Prop7.34": ["Prop7.16", "Prop7.19", "Prop7.21", "Prop7.20", "Prop7.17", "Prop7.33", "Prop7.19", "Prop7.19", "Prop7.20", "Prop7.17"],
    "Prop7.35": [],
    "Prop7.36": ["Prop7.34", "Prop7.35", "Prop7.34", "Prop7.35", "Prop7.35"],
    "Prop7.37": ["Prop7.15"],
    "Prop7.38": ["Prop7.15"],
    "Prop7.39": ["Prop7.36", "Prop7.37", "Prop7.38"]
  },
  "book8": {
    "Prop8.1": ["Prop7.14", "Prop7.21", "Prop7.20"],
    "Prop8.2": ["Prop7.17", "Prop7.18", "Prop7.17", "Prop7.17", "Prop7.22", "Prop7.27", "Prop8.1"],
    "Prop8.3": ["Prop7.33", "Prop8.2", "Prop7.22", "Prop8.2", "Prop7.27"],
    "Prop8.4": ["Prop7.34", "Prop7.20", "Prop7.20", "Prop7.35", "Prop7.34", "Prop7.13", "Prop7.13", "Prop7.20", "Prop7.35", "Prop7.20", "Prop7.35", "D7.20"],
    "Prop8.5": ["Prop8.4", "Prop7.17", "Prop7.16", "Prop7.17", "Prop7.14"],
    "Prop8.6": ["Prop7.33", "Prop7.14", "Prop8.3", "D7.20"],
    "Prop8.7": ["Prop8.6"],
    "Prop8.8": ["Prop7.33", "Prop8.3", "Prop7.14", "Prop7.21", "Prop7.20", "D7.20"],
    "Prop8.9": ["Prop7.33", "Prop8.2", "Prop8.2", "Prop8.2", "Prop7.20", "D7.15", "D7.20"],
    "Prop8.10": ["Prop7.17", "Prop7.18", "Prop7.18", "D7.20"],
    "Prop8.11": ["Prop7.17", "Prop7.18", "D5.9"],
    "Prop8.12": ["Prop7.17", "Prop7.18", "Prop7.17", "Prop7.18", "Prop7.17", "D5.10"],
    "Prop8.13": ["Prop7.14"],
    "Prop8.14": ["Prop8.11", "Prop8.7", "D7.20"],
    "Prop8.15": ["Prop8.12", "Prop8.7", "D7.20"],
    "Prop8.16": ["Prop8.14", "Prop8.14"],
    "Prop8.17": ["Prop8.15", "Prop8.15"],
    "Prop8.18": ["Prop7.13", "Prop7.17", "Prop7.17", "Prop5.9", "D7.21"],
    "Prop8.19": ["Prop8.18", "Prop7.17", "Prop7.13", "Prop7.17", "Prop7.18", "Prop7.17", "D7.21", "D5.10"],
    "Prop8.20": ["Prop7.33", "Prop7.20", "Prop7.20", "Prop7.17", "Prop7.17", "Prop7.13", "D7.15", "D7.21"],
    "Prop8.21": ["Prop8.2", "Prop8.3", "Prop8.20", "Prop7.14", "Prop7.21", "Prop7.20", "Prop7.20", "Prop7.18", "D7.15", "D7.21"],
    "Prop8.22": ["Prop8.20", "D7.21"],
    "Prop8.23": ["Prop8.21", "D7.21"],
    "Prop8.24": ["Prop8.18", "Prop8.8", "Prop8.22"],
    "Prop8.25": ["Prop8.19", "Prop8.8", "Prop8.23"],
    "Prop8.26": ["Prop8.18", "Prop8.2", "Prop8.2"],
    "Prop8.27": ["Prop8.19", "Prop8.2", "Prop8.2"]
  },
  "book9": {
    "Prop9.1": ["Prop7.17", "Prop8.18", "Prop8.8", "Prop8.22"],
    "Prop9.2": ["Prop7.17", "Prop8.18", "Prop8.8", "Prop8.20"],
    "Prop9.3": ["Prop8.8", "Prop8.23", "D7.15", "D7.20"],
    "Prop9.4": ["Prop9.3", "Prop7.17", "Prop8.19", "Prop8.8", "Prop8.23"],
    "Prop9.5": ["Prop9.3", "Prop7.17", "Prop8.19", "Prop8.8", "Prop8.23"],
    "Prop9.6": ["Prop8.19", "Prop8.8", "Prop8.23"],
    "Prop9.7": ["D7.15"],
    "Prop9.8": ["Prop8.22", "Prop8.23", "D7.20", "D7.15"],
    "Prop9.9": ["Prop9.8", "Prop8.22", "Prop8.22", "Prop9.8", "Prop9.3", "Prop8.23"],
    "Prop9.10": ["Prop9.8", "Prop8.26", "Prop9.8", "Prop7.13", "Prop8.25", "Prop9.6"],
    "Prop9.11": ["Prop7.15"],
    "Prop9.12": ["Prop7.29", "Prop9.11", "Prop7.19", "Prop7.21", "Prop7.20", "Prop9.11", "Prop7.19", "Prop7.21", "Prop7.20", "Prop9.8", "Prop7.19", "Prop7.21", "Prop7.20", "D7.14", "D7.11"],
    "Prop9.13": ["Prop9.12", "Prop7.31", "Prop9.12", "Prop9.11", "Prop9.12", "Prop7.31", "Prop9.12", "Prop9.11", "Prop7.19", "Prop9.11", "Prop7.19", "Prop9.8", "Prop7.19"],
    "Prop9.14": ["Prop7.30"],
    "Prop9.15": ["Prop8.2", "Prop8.2", "Prop7.22", "Prop7.28", "Prop7.24", "Prop7.25", "Prop2.3", "Prop7.25", "Prop2.4"],
    "Prop9.16": ["Prop7.21", "Prop7.20"],
    "Prop9.17": ["Prop7.13", "Prop7.21", "Prop7.20", "D7.20"],
    "Prop9.18": ["Prop9.16", "Prop7.19", "Prop7.19"],
    "Prop9.19": ["Prop9.17", "Prop7.14", "Prop7.21", "Prop7.20", "Prop7.19"],
    "Prop9.20": ["Prop7.36", "Prop7.31", "Prop7.28"],
    "Prop9.21": ["D7.6"],
    "Prop9.22": ["Prop9.21", "Prop9.21", "D7.7"],
    "Prop9.23": ["Prop9.22", "Prop9.21", "D7.7"],
    "Prop9.24": ["D7.6"],
    "Prop9.25": ["Prop9.24", "D7.7"],
    "Prop9.26": ["Prop9.24", "D7.7"],
    "Prop9.27": ["Prop9.24", "D7.7"],
    "Prop9.28": ["Prop9.21", "D7.15"],
    "Prop9.29": ["Prop9.23", "D7.15"],
    "Prop9.30": ["Prop9.23"],
    "Prop9.31": ["Prop9.30"],
    "Prop9.32": ["Prop9.13", "D7.8"],
    "Prop9.33": ["D7.9", "D7.8"],
    "Prop9.34": ["D7.8", "D7.9"],
    "Prop9.35": ["Prop7.13", "Prop7.11", "Prop7.13", "Prop7.12"],
    "Prop9.36": ["Prop7.14", "Prop7.19", "Prop9.35", "Prop7.19", "Prop9.13", "Prop7.29", "Prop7.21", "Prop7.20", "Prop7.14", "Prop7.19", "Prop7.19", "D7.20", "D7.22"]
  },
  "book10": {
    "D10.1": [],
    "D10.2": [],
    "D10.3": [],
    "D10.4": [],
    "D10.5": [],
    "D10.6": [],
    "D10.7": [],
    "D10.8": [],
    "D10.9": [],
    "D10.10": [],
    "D10.11": [],
    "D10.12": [],
    "D10.13": [],
    "D10.14": [],
    "D10.15": [],
    "D10.16": [],
    "Prop10.1": ["D5.4"],
    "Prop10.2": ["D10.1", "Prop10.1"],
    "Prop10.3": ["Prop10.2"],
    "Prop10.4": ["Prop10.3", "D10.1", "Prop10.1"],
    "Prop10.5": ["Prop5.7", "Prop5.22", "D7.20"],
    "Prop10.6": ["Prop5.7", "Prop6.19", "Prop5.22", "Prop5.11", "Prop5.9", "D7.20", "D7.20", "D10.1"],
    "Prop10.7": ["Prop10.6"],
    "Prop10.8": ["Prop10.5"],
    "Prop10.9": ["Prop6.20", "Prop10.5", "Prop8.11", "Prop10.6"],
    "Prop10.10": ["Prop10.6", "Prop10.9", "Prop6.13", "D5.9"],
    "Prop10.11": ["Prop10.5", "Prop10.6", "Prop10.7", "Prop10.8"],
    "Prop10.12": ["Prop10.5", "Prop8.4", "Prop5.11", "Prop5.22", "Prop10.6"],
    "Prop10.13": ["Prop10.12", "Prop4.1", "Prop3.31", "Prop1.47"],
    "Prop10.14": ["Prop6.22", "Prop5.17", "Prop5.22", "Prop10.11", "Prop5.7"],
    "Prop10.15": ["D10.1"],
    "Prop10.16": ["D10.1"],
    "Prop10.17": ["Prop1.10", "Prop1.3", "Prop2.5", "Prop10.15", "Prop10.6", "Prop10.12"],
    "Prop10.18": ["Prop10.16", "Prop10.6", "Prop10.13"],
    "Prop10.19": ["Prop6.1", "Prop10.11", "Prop10.4", "D10.4"],
    "Prop10.20": ["Prop6.1", "Prop10.11", "D10.4", "D10.3"],
    "Prop10.21": ["Prop6.1", "Prop10.11", "D10.4"],
    "Prop10.22": ["Prop10.21", "Prop6.14", "Prop6.22", "Prop10.11", "Prop10.13", "D10.4"],
    "Prop10.23": ["Prop10.22", "Prop6.1", "Prop10.11", "Prop10.13", "Prop10.21", "D10.3"],
    "Prop10.24": ["Prop6.1", "Prop10.11", "Prop10.23"],
    "Prop10.25": ["Prop10.22", "Prop6.1", "Prop10.11", "Prop10.19", "Prop5.11", "Prop6.17", "Prop10.21"],
    "Prop10.26": ["Prop10.22", "Prop10.20", "Prop10.13", "Prop10.11", "Prop10.6", "Prop2.4", "Prop10.16", "D10.4"],
    "Prop10.27": ["Prop6.13", "Prop6.12", "Prop6.17", "Prop10.21", "Prop10.11", "Prop10.23", "Prop5.16", "Prop5.11"],
    "Prop10.28": ["Prop6.13", "Prop6.12", "Prop6.17", "Prop10.21", "Prop10.11", "Prop10.23", "Prop5.16", "Prop6.16", "Prop9.24", "Prop9.26", "Prop2.6", "Prop9.1", "Prop2.6"],
    "Prop10.29": ["Prop10.28", "Prop10.6", "Prop5.19", "Prop10.9", "Prop3.31", "Prop1.47", "D10.4"],
    "Prop10.30": ["Prop3.31", "Prop1.47", "Prop10.9", "Prop10.28", "Prop10.6", "Prop5.19", "Prop3.31"],
    "Prop10.31": ["Prop10.29", "Prop10.21", "Prop10.11", "Prop10.23", "Prop10.14", "Prop10.30"],
    "Prop10.32": ["Prop10.29", "Prop10.21", "Prop10.11", "Prop10.23", "Prop10.14", "Prop10.30", "Prop6.8", "Prop6.4", "Prop6.17", "Prop6.16"],
    "Prop10.33": ["Prop10.30", "Prop6.28", "Prop10.18", "Prop10.32", "Prop10.11", "Prop1.47", "Prop10.6", "Prop10.21", "Prop10.23"],
    "Prop10.34": ["Prop10.31", "Prop6.28", "Prop10.18", "Prop10.11", "Prop10.32", "Prop3.31", "Prop1.47", "Prop10.32", "Prop10.6", "D10.4"],
    "Prop10.35": ["Prop10.32", "Prop10.18", "Prop10.11", "Prop3.31", "Prop1.47", "Prop10.13"],
    "Prop10.36": ["Prop10.11", "Prop10.6", "Prop10.15", "Prop10.13", "Prop2.4", "Prop10.16", "D10.4"],
    "Prop10.37": ["Prop2.4", "Prop10.16", "D10.4", "Prop10.36"],
    "Prop10.38": ["Prop10.28", "Prop1.44", "Prop2.4", "Prop10.22", "Prop10.21", "Prop10.11", "Prop10.15", "Prop10.6", "Prop10.13", "Prop6.1", "Prop10.36", "Prop10.20", "D10.4"],
    "Prop10.39": ["Prop10.33", "Prop10.6", "Prop10.23", "Prop2.4", "Prop10.16", "D10.4"],
    "Prop10.40": ["Prop10.34", "Prop10.16", "D10.4"],
    "Prop10.41": ["Prop10.35", "Prop2.4", "Prop10.22", "Prop6.1", "Prop10.11", "Prop10.36", "D10.4", "Prop2.5"],
    "Prop10.42": ["Prop10.36", "Prop2.4", "Prop10.21", "Prop10.26"],
    "Prop10.43": ["Prop10.37", "Prop10.26", "Prop10.41"],
    "Prop10.44": ["Prop10.38", "Prop10.41", "Prop2.4", "Prop10.22", "Prop10.21", "Prop10.15", "Prop10.6", "Prop10.13", "Prop6.1", "Prop10.11", "Prop10.36", "Prop10.42"],
    "Prop10.45": ["Prop10.39", "Prop10.26"],
    "Prop10.46": ["Prop10.40", "Prop10.26"],
    "Prop10.47": ["Prop10.41", "Prop2.4", "Prop10.22", "Prop6.1", "Prop10.11", "Prop10.36", "Prop10.42"],
    "Prop10.48": ["Prop10.28", "Prop10.6", "Prop10.9", "Prop10.36", "Prop5.14", "Prop5.19", "D10.3", "D10.5"],
    "Prop10.49": ["Prop10.28", "Prop10.6", "Prop10.9", "Prop10.36", "Prop5.7", "Prop5.14", "Prop5.19", "D10.6"],
    "Prop10.50": ["Prop10.6", "Prop10.9", "Prop10.36", "Prop5.22", "Prop5.14", "Prop5.19", "D10.7"],
    "Prop10.51": ["Prop10.28", "Prop10.6", "Prop10.9", "Prop10.36", "Prop5.14", "Prop5.19", "D10.8"],
    "Prop10.52": ["Prop10.38", "Prop10.6", "Prop10.9", "Prop10.36", "Prop5.7", "Prop5.14", "Prop5.19"],
    "Prop10.53": ["Prop1.34", "Prop6.1", "Prop5.18", "Prop5.11", "Prop10.28", "Prop10.6", "Prop10.9", "Prop10.36", "Prop5.22", "Prop5.14", "Prop5.19", "D10.10"],
    "Prop10.54": ["Prop10.17", "Prop2.14", "Prop10.53", "Prop6.17", "Prop6.1", "Prop1.43", "Prop10.15", "Prop10.12", "Prop10.19", "Prop10.13", "Prop10.11", "Prop10.36", "D10.5"],
    "Prop10.55": ["Prop10.17", "Prop10.53", "Prop10.13", "Prop10.15", "Prop10.21", "Prop6.1", "Prop10.11", "Prop10.12", "Prop10.19", "Prop10.37", "D10.6"],
    "Prop10.56": ["Prop10.13", "Prop10.21", "Prop10.38", "D10.7"],
    "Prop10.57": ["Prop10.18", "Prop6.1", "Prop10.11", "Prop10.19", "Prop10.13", "Prop10.21", "Prop10.39", "D10.8"],
    "Prop10.58": ["Prop10.18", "Prop6.1", "Prop10.11", "Prop10.13", "Prop10.21", "Prop10.12", "Prop10.19", "Prop10.40", "D10.9"],
    "Prop10.59": ["Prop10.21", "Prop10.13", "Prop10.21", "Prop6.1", "Prop10.11", "Prop10.41", "D10.10", "Prop2.5", "Prop2.9"],
    "Prop10.60": ["Prop2.4", "Prop10.36", "Prop10.15", "Prop10.20", "Prop10.21", "Prop10.22", "Prop10.13", "Prop10.53", "Prop6.1", "Prop6.17", "Prop10.11", "Prop10.59", "Prop5.14", "Prop10.17", "D10.5"],
    "Prop10.61": ["Prop10.37", "Prop10.21", "Prop10.15", "Prop10.23", "Prop10.22", "Prop10.20", "Prop10.36", "Prop10.59", "Prop6.1", "Prop10.11", "Prop10.17", "D10.6"],
    "Prop10.62": ["Prop10.38", "Prop10.15", "Prop10.23", "Prop10.22", "Prop10.21", "Prop10.11", "Prop10.12", "Prop10.13", "Prop6.1", "Prop10.36", "Prop10.17", "D10.7"],
    "Prop10.63": ["Prop10.39", "Prop10.20", "Prop10.22", "Prop10.13", "Prop10.36", "Prop6.1", "Prop10.11", "Prop10.18", "D10.8"],
    "Prop10.64": ["Prop10.40", "Prop10.22", "Prop10.20", "Prop10.13", "Prop10.36", "Prop10.18", "D10.9"],
    "Prop10.65": ["Prop10.41", "Prop10.22", "Prop6.1", "Prop10.11", "Prop10.36", "Prop10.18", "D10.10"],
    "Prop10.66": ["Prop10.36", "Prop6.12", "Prop6.16", "Prop5.19", "Prop10.11", "Prop5.11", "Prop5.16", "Prop10.14", "Prop10.12", "Prop10.13", "D10.5", "D10.6", "D10.7", "D10.8", "D10.9", "D10.10", "Prop10.8"],
    "Prop10.67": ["Prop10.37", "Prop10.38", "Prop6.12", "Prop5.19", "Prop6.16", "Prop10.11", "Prop10.23", "Prop10.21", "Prop5.16", "Prop10.23"],
    "Prop10.68": ["Prop10.39", "Prop5.11", "Prop10.11", "Prop5.16", "Prop5.18", "Prop6.20", "Prop10.23", "Prop10.13"],
    "Prop10.69": ["Prop10.40"],
    "Prop10.70": ["Prop10.41"],
    "Prop10.71": ["Prop10.20", "Prop10.22", "Prop6.1", "Prop10.11", "Prop10.36", "Prop5.14", "Prop10.54", "Prop10.57", "Prop10.55", "Prop10.58", "D10.5", "D10.8", "D10.6", "D10.9"],
    "Prop10.72": ["Prop10.22", "Prop6.1", "Prop10.11", "Prop10.36", "Prop10.56", "Prop10.59", "Prop10.22", "Prop10.60", "Prop10.61", "Prop10.62", "Prop10.63", "Prop10.64", "Prop10.65", "D10.7", "D10.10"],
    "Prop10.73": ["Prop10.21", "Prop10.11", "Prop10.15", "Prop10.6", "Prop2.7", "Prop10.13", "Prop10.16", "D10.4"],
    "Prop10.74": ["Prop10.27", "Prop2.7", "Prop10.16", "D10.4"],
    "Prop10.75": ["Prop10.28", "Prop2.7", "Prop10.15", "Prop10.23", "Prop10.22", "Prop10.21", "Prop10.6", "Prop10.13", "Prop6.1", "Prop10.11", "Prop10.73", "Prop10.20", "D10.4"],
    "Prop10.76": ["Prop10.33", "Prop2.7", "Prop10.16", "D10.4"],
    "Prop10.77": ["Prop10.34", "Prop2.7", "Prop10.16", "D10.4"],
    "Prop10.78": ["Prop10.35", "Prop2.7", "Prop10.22", "Prop6.1", "Prop10.11", "Prop10.73", "Prop10.20"],
    "Prop10.79": ["Prop10.73", "Prop2.7", "Prop10.21", "Prop10.26"],
    "Prop10.80": ["Prop10.74", "Prop2.7", "Prop10.15", "Prop10.23", "Prop10.26"],
    "Prop10.81": ["Prop10.75", "Prop2.7", "Prop10.15", "Prop10.23", "Prop10.22", "Prop10.21", "Prop10.11", "Prop10.6", "Prop10.13", "Prop6.1", "Prop10.73", "Prop10.79"],
    "Prop10.82": ["Prop10.76", "Prop2.7", "Prop10.26"],
    "Prop10.83": ["Prop10.77", "Prop10.26"],
    "Prop10.84": ["Prop10.78", "Prop2.7", "Prop10.22", "Prop6.1", "Prop10.11", "Prop10.73", "Prop10.79"],
    "Prop10.85": ["Prop10.28", "Prop10.6", "Prop10.9", "Prop10.73", "Prop10.13", "Prop5.19", "D10.11"],
    "Prop10.86": ["Prop10.28", "Prop10.6", "Prop10.9", "Prop10.73", "Prop10.13", "Prop5.19", "D10.12"],
    "Prop10.87": ["Prop10.6", "Prop10.9", "Prop10.73", "Prop5.22", "Prop10.13", "Prop5.19", "D10.13"],
    "Prop10.88": ["Prop10.6", "Prop10.9", "Prop10.73", "Prop10.13", "Prop5.19", "D10.14"],
    "Prop10.89": ["Prop10.6", "Prop10.9", "Prop10.73", "Prop10.13", "Prop5.19", "D10.15"],
    "Prop10.90": ["Prop10.6", "Prop10.9", "Prop10.73", "Prop5.22", "Prop10.13", "Prop5.19", "D10.16"],
    "Prop10.91": ["Prop10.73", "Prop10.17", "Prop10.15", "Prop10.12", "Prop10.19", "Prop10.13", "Prop10.21", "Prop6.26", "Prop6.17", "Prop6.1", "Prop5.11", "Prop10.53", "Prop1.43", "Prop10.11", "D10.11"],
    "Prop10.92": ["Prop10.73", "Prop10.17", "Prop10.15", "Prop10.13", "Prop10.21", "Prop10.19", "Prop6.26", "Prop6.1", "Prop5.11", "Prop10.53", "Prop1.43", "Prop10.11", "Prop10.74", "D10.12"],
    "Prop10.93": ["Prop10.73", "Prop10.17", "Prop6.1", "Prop10.11", "Prop10.15", "Prop10.13", "Prop10.21", "Prop6.26", "Prop6.17", "Prop5.11", "Prop10.53", "Prop1.43", "Prop10.75", "D10.13"],
    "Prop10.94": ["Prop10.73", "Prop10.18", "Prop10.19", "Prop10.21", "Prop6.1", "Prop10.11", "Prop6.26", "Prop6.17", "Prop6.1", "Prop5.11", "Prop10.13", "Prop1.43", "Prop10.76", "D10.14"],
    "Prop10.95": ["Prop10.73", "Prop10.18", "Prop10.21", "Prop10.19", "Prop6.26", "Prop10.77", "D10.15"],
    "Prop10.96": ["Prop10.73", "Prop10.18", "Prop6.1", "Prop10.11", "Prop10.21", "Prop6.26", "Prop10.78", "D10.16"],
    "Prop10.97": ["Prop10.73", "Prop2.7", "Prop10.20", "Prop10.22", "Prop6.1", "Prop10.11", "Prop10.21", "Prop6.17", "Prop10.17", "D10.15"],
    "Prop10.98": ["Prop10.74", "Prop10.15", "Prop10.23", "Prop10.22", "Prop2.7", "Prop10.20", "Prop6.1", "Prop10.11", "Prop10.21", "Prop10.73", "Prop5.11", "Prop6.17", "Prop10.17", "D10.16"],
    "Prop10.99": ["Prop10.75", "Prop10.15", "Prop10.23", "Prop10.22", "Prop2.7", "Prop6.1", "Prop10.11", "Prop10.21", "Prop10.13", "Prop10.73", "Prop5.11", "Prop6.17", "Prop10.17", "D10.13"],
    "Prop10.100": ["Prop10.76", "Prop10.20", "Prop2.7", "Prop10.22", "Prop6.1", "Prop10.11", "Prop10.73", "Prop10.21", "Prop5.11", "Prop6.17", "Prop10.18", "D10.14"],
    "Prop10.101": ["Prop10.77", "Prop10.22", "Prop2.7", "Prop10.20", "Prop6.1", "Prop10.11", "Prop10.73", "Prop10.18", "D10.15"],
    "Prop10.102": ["Prop10.78", "Prop10.22", "Prop2.7", "Prop6.1", "Prop10.11", "Prop10.73", "Prop10.21", "Prop10.18", "D10.16"],
    "Prop10.103": ["Prop10.73", "Prop6.12", "Prop5.12", "Prop10.11", "Prop10.13", "Prop5.16", "Prop10.14", "Prop10.12", "Prop10.15", "Prop10.16", "D10.11", "D10.12", "D10.13", "D10.14", "D10.15", "D10.16"],
    "Prop10.104": ["Prop10.74", "Prop10.75", "Prop6.12", "Prop5.12", "Prop10.11", "Prop10.23", "Prop10.13", "Prop10.74", "Prop10.75", "Prop5.12", "Prop5.16", "Prop10.21", "Prop10.11", "D10.4"],
    "Prop10.105": ["Prop10.76", "Prop10.13", "Prop5.12", "Prop5.16", "Prop6.22", "Prop5.18", "Prop10.104", "Prop10.11", "D10.4", "Prop10.21", "Prop10.23"],
    "Prop10.106": ["Prop10.77"],
    "Prop10.107": ["Prop10.78"],
    "Prop10.108": ["Prop10.20", "Prop10.22", "Prop10.13", "Prop10.73", "Prop10.91", "Prop10.14", "Prop10.94", "D10.1"],
    "Prop10.109": ["Prop10.13", "Prop10.73", "Prop10.92", "Prop10.95", "D10.12", "D10.15"],
    "Prop10.110": ["Prop10.22", "Prop6.1", "Prop10.11", "Prop10.73", "Prop10.93", "Prop10.96", "D10.3", "D10.16"],
    "Prop10.111": ["Prop10.98", "Prop10.102", "Prop10.97", "Prop10.60", "Prop10.12", "Prop10.15", "Prop10.13", "Prop10.73", "D10.10", "D10.5", "Prop10.22"],
    "Prop10.112": ["Prop6.16", "Prop5.16", "Prop5.14", "Prop5.17", "Prop5.12", "Prop5.11", "Prop10.36", "Prop6.22", "Prop10.11", "Prop10.15", "Prop10.20", "Prop10.12", "Prop10.73", "D5.9", "D10.3", "Prop10.10", "Prop10.14", "D10.5", "D10.6", "D10.7", "D10.8", "D10.9", "D10.10"],
    "Prop10.113": ["Prop10.73", "Prop10.20", "Prop6.16", "Prop5.19", "Prop10.11", "Prop5.11", "Prop10.15", "Prop10.12", "Prop5.16", "Prop10.13", "Prop10.36", "Prop10.14", "D5.9", "D10.3", "D10.5", "D10.6", "D10.7", "D10.8", "D10.9", "D10.10", "Prop5.14", "Prop10.5", "Prop10.6", "Prop10.7", "Prop10.8", "Prop10.9", "Prop10.10"],
    "Prop10.114": ["Prop10.112", "Prop5.16", "Prop5.19", "Prop10.12", "Prop10.11", "Prop6.1"],
    "Prop10.115": ["Prop10.20", "D10.4"]
  },
  "book11": {
    "D11.1": [],
    "D11.2": [],
    "D11.3": [],
    "D11.4": [],
    "D11.5": [],
    "D11.6": [],
    "D11.7": [],
    "D11.8": [],
    "D11.9": [],
    "D11.10": [],
    "D11.11": [],
    "D11.12": [],
    "D11.13": [],
    "D11.14": [],
    "D11.15": [],
    "D11.16": [],
    "D11.17": [],
    "D11.18": [],
    "D11.19": [],
    "D11.20": [],
    "D11.21": [],
    "D11.22": [],
    "D11.23": [],
    "D11.24": [],
    "D11.25": [],
    "D11.26": [],
    "D11.27": [],
    "D11.28": [],
    "Prop11.1": [],
    "Prop11.2": ["Prop11.1"],
    "Prop11.3": [],
    "Prop11.4": ["Prop1.15", "Prop1.4", "Prop1.26", "Prop1.8", "D1.10", "D11.3"],
    "Prop11.5": ["Prop11.4", "D11.3"],
    "Prop11.6": ["Prop1.4", "Prop1.8", "Prop11.5", "Prop11.2", "Prop1.28", "D11.3"],
    "Prop11.7": ["Prop11.3"],
    "Prop11.8": ["Prop11.7", "Prop1.29", "Prop1.4", "Prop1.8", "Prop11.4", "Prop11.2", "D11.3"],
    "Prop11.9": ["Prop11.4", "Prop11.8", "Prop11.6"],
    "Prop11.10": ["Prop1.33", "Prop11.9", "Prop1.8"],
    "Prop11.11": ["Prop1.12", "Prop1.11", "Prop1.31", "Prop11.4", "Prop11.8", "D11.3"],
    "Prop11.12": ["Prop11.11", "Prop1.31", "Prop11.8"],
    "Prop11.13": ["Prop11.3", "D11.3"],
    "Prop11.14": ["Prop11.3", "Prop1.17", "D11.3", "D11.8"],
    "Prop11.15": ["Prop11.11", "Prop1.31", "Prop11.9", "Prop1.29", "Prop11.4", "Prop11.14", "D11.3"],
    "Prop11.16": ["Prop11.1", "D1.23"],
    "Prop11.17": ["Prop11.16", "Prop6.2", "Prop5.11"],
    "Prop11.18": ["Prop1.11", "Prop1.28", "Prop11.8", "D11.3", "D11.4"],
    "Prop11.19": ["Prop11.13", "D11.4"],
    "Prop11.20": ["Prop1.4", "Prop1.20", "Prop1.25"],
    "Prop11.21": ["Prop11.20", "Prop1.32"],
    "Prop11.22": ["Prop1.4", "Prop1.24", "Prop1.20"],
    "Prop11.23": ["Prop11.21", "Prop11.22", "Prop4.5", "Prop1.8", "Prop6.2", "Prop1.29", "Prop6.4", "Prop5.16", "Prop5.14", "Prop1.25", "Prop11.12", "Prop1.4", "Prop1.47", "Prop1.8", "Prop4.1", "Prop3.31"],
    "Prop11.24": ["Prop11.16", "Prop11.10", "Prop1.34", "Prop1.4"],
    "Prop11.25": ["Prop11.24", "D11.10", "D5.5"],
    "Prop11.26": ["Prop11.11", "Prop1.23", "Prop11.12", "Prop1.4", "Prop1.8", "D11.3"],
    "Prop11.27": ["Prop11.26", "Prop6.12", "Prop5.22", "D11.9"],
    "Prop11.28": ["Prop1.34", "Prop11.24", "D11.10"],
    "Prop11.29": ["Prop1.34", "Prop1.4", "Prop1.8", "Prop1.36", "Prop11.24"],
    "Prop11.30": ["Prop11.29"],
    "Prop11.31": ["Prop1.23", "Prop6.14", "Prop11.24", "Prop11.29", "Prop1.35", "Prop5.7", "Prop11.25", "Prop5.11", "Prop5.9", "Prop11.30", "D11.10"],
    "Prop11.32": ["Prop1.45", "Prop11.31", "Prop11.25"],
    "Prop11.33": ["Prop11.24", "Prop6.1", "Prop11.32", "D11.10", "D5.10", "D6.1", "D11.9"],
    "Prop11.34": ["Prop11.32", "Prop5.7", "Prop11.25", "Prop6.1", "Prop11.31", "Prop5.9", "Prop11.29", "Prop11.30"],
    "Prop11.35": ["Prop11.8", "Prop1.47", "Prop1.48", "Prop1.26", "Prop1.4", "Prop1.8"],
    "Prop11.36": ["Prop11.23", "Prop6.14", "Prop11.35", "Prop11.31"],
    "Prop11.37": ["Prop11.33"],
    "Prop11.38": ["Prop1.29", "Prop1.4", "Prop1.14", "Prop11.9", "Prop1.33", "Prop1.15", "Prop1.26"],
    "Prop11.39": ["Prop1.34", "Prop11.31", "Prop11.28"]
  },
  "book12": {
    "Prop12.1": ["Prop6.6", "Prop3.27", "Prop3.31", "Prop1.32", "Prop6.4", "Prop6.20", "D6.1"],
    "Prop12.2": ["Prop4.6", "Prop1.47", "Prop10.1", "Prop12.1", "Prop5.11", "Prop5.16", "Prop5.7", "Prop5.14"],
    "Prop12.3": ["Prop6.2", "Prop1.34", "Prop1.29", "Prop1.4", "Prop11.10", "Prop6.6", "Prop1.41", "Prop11.39", "D11.10", "D6.1", "D11.9"],
    "Prop12.4": ["Prop12.3", "Prop6.22", "Prop5.16", "Prop11.39", "Prop5.12", "Prop11.17", "Prop11.32", "Prop11.28"],
    "Prop12.5": ["Prop12.3", "Prop10.1", "Prop12.4", "Prop5.11", "Prop5.16", "Prop5.14", "Prop5.7", "Prop12.2"],
    "Prop12.6": ["Prop12.5", "Prop5.18", "Prop5.22"],
    "Prop12.7": ["Prop12.5", "Prop1.34"],
    "Prop12.8": ["Prop11.24", "Prop11.33", "Prop11.28", "Prop12.7", "D11.9", "Prop6.20", "Prop5.12"],
    "Prop12.9": ["Prop11.34", "Prop1.34", "Prop5.11"],
    "Prop12.10": ["Prop4.6", "Prop12.2", "Prop4.7", "Prop11.32", "Prop12.2", "Prop10.1", "Prop12.7"],
    "Prop12.11": ["Prop4.6", "Prop12.2", "Prop4.7", "Prop12.6", "Prop12.10", "Prop10.1", "Prop6.18", "Prop12.1", "Prop5.11", "Prop5.16", "Prop5.14", "Prop12.10", "Prop5.7", "Prop12.2"],
    "Prop12.12": ["Prop4.6", "Prop12.2", "Prop12.10", "Prop10.1", "Prop6.18", "Prop5.16", "Prop6.6", "Prop5.22", "Prop6.5", "Prop12.8", "Prop5.12", "Prop5.7", "D11.24", "D6.1", "D6.1", "D11.9"],
    "Prop12.13": ["Prop12.11", "D5.5"],
    "Prop12.14": ["Prop12.11", "Prop12.13", "Prop12.10"],
    "Prop12.15": ["Prop12.11", "Prop5.7", "Prop12.13", "Prop5.11", "Prop5.9"],
    "Prop12.16": ["Prop3.16", "Prop10.1", "Prop3.3", "Prop1.4", "Prop1.28", "Prop4.1"],
    "Prop12.17": ["Prop3.15", "Prop12.16", "Prop11.18", "Prop11.11", "Prop3.27", "Prop1.26", "Prop6.2", "Prop11.6", "Prop1.33", "Prop11.1", "Prop11.7", "Prop11.2", "Prop1.47", "Prop3.31", "Prop6.8", "Prop12.8", "Prop5.12", "D11.14", "D3.1", "D11.4", "D11.3"],
    "Prop12.18": ["Prop12.17", "Prop5.16", "Prop5.14", "Prop5.7", "Prop12.2"]
  },
  "book13": {
    "Prop13.1": ["Prop6.17", "Prop6.1", "Prop1.43", "D6.3"],
    "Prop13.2": ["Prop6.1", "Prop1.43", "Prop6.17", "Prop5.14", "Prop2.4"],
    "Prop13.3": ["Prop6.17", "D6.3", "Prop6.1", "Prop1.43"],
    "Prop13.4": ["Prop6.17", "Prop1.43", "D6.3"],
    "Prop13.5": ["Prop6.17", "Prop1.43", "Prop5.14", "D6.3"],
    "Prop13.6": ["Prop13.1", "Prop10.6", "Prop10.9", "Prop10.73", "Prop6.17", "Prop10.97", "D10.4", "D6.3"],
    "Prop13.7": ["Prop1.4", "Prop1.6", "Prop1.8", "Prop1.5"],
    "Prop13.8": ["Prop4.14", "Prop1.4", "Prop1.32", "Prop3.28", "Prop6.33", "Prop1.6", "Prop1.5", "Prop6.4", "Prop5.14"],
    "Prop13.9": ["Prop3.1", "Prop6.33", "Prop1.5", "Prop1.32", "Prop4.15", "Prop6.4", "Prop5.14"],
    "Prop13.10": ["Prop3.1", "Prop1.5", "Prop1.26", "Prop3.26", "Prop6.33", "Prop1.32", "Prop6.4", "Prop6.17", "Prop1.4", "Prop3.29", "Prop2.2", "Prop4.15"],
    "Prop13.11": ["Prop3.1", "Prop1.4", "Prop1.32", "Prop6.4", "Prop5.18", "Prop13.8", "Prop13.1", "Prop10.9", "Prop10.73", "Prop10.15", "Prop10.12", "Prop5.19", "Prop10.9", "Prop10.94", "Prop6.8", "D10.14"],
    "Prop13.12": ["Prop4.2", "Prop3.1", "Prop4.15", "Prop3.31", "Prop1.47"],
    "Prop13.13": ["Prop6.10", "Prop4.2", "Prop3.1", "Prop11.12", "Prop1.4", "Prop13.12", "Prop6.17", "Prop6.8", "Prop3.31", "Prop6.4", "Prop6.1", "D11.3"],
    "Prop13.14": ["Prop11.12", "Prop1.47", "Prop1.4", "Prop3.31", "Prop6.8", "D5.9"],
    "Prop13.15": ["Prop11.4", "Prop1.47", "Prop6.8", "D11.3", "D5.9"],
    "Prop13.16": ["Prop6.10", "Prop4.11", "Prop11.6", "Prop1.33", "Prop13.10", "Prop3.1", "Prop11.6", "Prop1.33", "Prop4.15", "Prop1.29", "Prop13.9", "Prop6.8", "Prop3.31", "Prop13.3", "Prop13.11", "D11.3", "D5.9"],
    "Prop13.17": ["Prop13.15", "Prop13.4", "Prop1.47", "Prop11.6", "Prop6.32", "Prop11.1", "Prop13.5", "Prop13.4", "Prop1.8", "Prop13.7", "Prop11.38", "Prop5.15", "Prop5.14", "Prop13.6", "D11.3"],
    "Prop13.18": ["Prop6.8", "Prop13.13", "Prop13.15", "Prop13.14", "Prop6.4", "Prop1.47", "Prop13.16", "Prop4.15", "Prop13.10", "Prop6.20", "Prop13.17", "Prop6.4", "Prop13.9", "Prop11.21", "Prop4.14", "Prop3.1", "Prop1.4", "Prop1.32", "D5.9", "D11.11"]
  }
}
```

</details>

and their recursive reference counts:

<details>
<summary>Recursive counts data (click to expand)</summary>

```json
{
  "Prop1.1": 4,
  "Prop1.2": 10,
  "Prop1.3": 13,
  "Prop1.4": 2,
  "Prop1.5": 18,
  "Prop1.6": 17,
  "Prop1.7": 20,
  "Prop1.8": 21,
  "Prop1.9": 38,
  "Prop1.10": 44,
  "Prop1.11": 42,
  "Prop1.12": 46,
  "Prop1.13": 86,
  "Prop1.14": 92,
  "Prop1.15": 94,
  "Prop1.16": 137,
  "Prop1.17": 223,
  "Prop1.18": 177,
  "Prop1.19": 195,
  "Prop1.20": 216,
  "Prop1.21": 569,
  "Prop1.22": 219,
  "Prop1.23": 221,
  "Prop1.24": 472,
  "Prop1.25": 476,
  "Prop1.26": 365,
  "Prop1.27": 139,
  "Prop1.28": 371,
  "Prop1.29": 280,
  "Prop1.30": 560,
  "Prop1.31": 361,
  "Prop1.32": 813,
  "Prop1.33": 563,
  "Prop1.34": 841,
  "Prop1.35": 1807,
  "Prop1.36": 3549,
  "Prop1.37": 2935,
  "Prop1.38": 4207,
  "Prop1.39": 3296,
  "Prop1.40": 4568,
  "Prop1.41": 3340,
  "Prop1.42": 5642,
  "Prop1.43": 1682,
  "Prop1.44": 7175,
  "Prop1.45": 7308,
  "Prop1.46": 1055,
  "Prop1.47": 7358,
  "Prop1.48": 1099,
  "Prop2.1": 585,
  "Prop2.2": 1416,
  "Prop2.3": 1416,
  "Prop2.4": 2524,
  "Prop2.5": 4087,
  "Prop2.6": 4953,
  "Prop2.7": 2103,
  "Prop2.8": 3786,
  "Prop2.9": 5070,
  "Prop2.10": 5166,
  "Prop2.11": 5150,
  "Prop2.12": 6540,
  "Prop2.13": 6631,
  "Prop2.14": 11464,
  "Prop3.1": 86,
  "Prop3.2": 322,
  "Prop3.3": 126,
  "Prop3.4": 334,
  "Prop3.5": 3,
  "Prop3.6": 3,
  "Prop3.7": 705,
  "Prop3.8": 927,
  "Prop3.9": 171,
  "Prop3.10": 263,
  "Prop3.11": 302,
  "Prop3.12": 302,
  "Prop3.13": 689,
  "Prop3.14": 340,
  "Prop3.15": 945,
  "Prop3.16": 419,
  "Prop3.17": 599,
  "Prop3.18": 640,
  "Prop3.19": 1058,
  "Prop3.20": 816,
  "Prop3.21": 1632,
  "Prop3.22": 4080,
  "Prop3.23": 139,
  "Prop3.24": 542,
  "Prop3.25": 450,
  "Prop3.26": 683,
  "Prop3.27": 1643,
  "Prop3.28": 830,
  "Prop3.29": 2327,
  "Prop3.30": 372,
  "Prop3.31": 1735,
  "Prop3.32": 3826,
  "Prop3.33": 4146,
  "Prop3.34": 908,
  "Prop3.35": 5165,
  "Prop3.36": 7291,
  "Prop3.37": 7456,
  "Prop4.1": 89,
  "Prop4.2": 3959,
  "Prop4.3": 5648,
  "Prop4.4": 506,
  "Prop4.5": 52,
  "Prop4.6": 967,
  "Prop4.7": 2969,
  "Prop4.8": 668,
  "Prop4.9": 39,
  "Prop4.10": 8144,
  "Prop4.11": 12218,
  "Prop4.12": 2576,
  "Prop4.13": 631,
  "Prop4.14": 68,
  "Prop4.15": 5571,
  "Prop4.16": 29862,
  "Prop5.1": 0,
  "Prop5.2": 0,
  "Prop5.3": 1,
  "Prop5.4": 2,
  "Prop5.5": 1,
  "Prop5.6": 1,
  "Prop5.7": 1,
  "Prop5.8": 4,
  "Prop5.9": 8,
  "Prop5.10": 12,
  "Prop5.11": 1,
  "Prop5.12": 2,
  "Prop5.13": 3,
  "Prop5.14": 13,
  "Prop5.15": 3,
  "Prop5.16": 15,
  "Prop5.17": 4,
  "Prop5.18": 16,
  "Prop5.19": 19,
  "Prop5.20": 17,
  "Prop5.21": 17,
  "Prop5.22": 19,
  "Prop5.23": 21,
  "Prop5.24": 23,
  "Prop5.25": 25,
  "Prop6.1": 1697,
  "Prop6.2": 3421,
  "Prop6.3": 3858,
  "Prop6.4": 7302,
  "Prop6.5": 12136,
  "Prop6.6": 16172,
  "Prop6.7": 20286,
  "Prop6.8": 12225,
  "Prop6.9": 1418,
  "Prop6.10": 5268,
  "Prop6.11": 1418,
  "Prop6.12": 1418,
  "Prop6.13": 5179,
  "Prop6.14": 3414,
  "Prop6.15": 3413,
  "Prop6.16": 6831,
  "Prop6.17": 13662,
  "Prop6.18": 16181,
  "Prop6.19": 7267,
  "Prop6.20": 32414,
  "Prop6.21": 2,
  "Prop6.22": 27254,
  "Prop6.23": 5126,
  "Prop6.24": 19508,
  "Prop6.25": 13802,
  "Prop6.26": 19511,
  "Prop6.27": 21232,
  "Prop6.28": 40790,
  "Prop6.29": 40831,
  "Prop6.30": 34456,
  "Prop6.31": 19645,
  "Prop6.32": 3002,
  "Prop6.33": 1820,
  "Prop7.1": 0,
  "Prop7.2": 1,
  "Prop7.3": 6,
  "Prop7.4": 1,
  "Prop7.5": 0,
  "Prop7.6": 1,
  "Prop7.7": 1,
  "Prop7.8": 2,
  "Prop7.9": 2,
  "Prop7.10": 6,
  "Prop7.11": 5,
  "Prop7.12": 4,
  "Prop7.13": 8,
  "Prop7.14": 24,
  "Prop7.15": 5,
  "Prop7.16": 7,
  "Prop7.17": 10,
  "Prop7.18": 25,
  "Prop7.19": 71,
  "Prop7.20": 14,
  "Prop7.21": 23,
  "Prop7.22": 12,
  "Prop7.23": 0,
  "Prop7.24": 31,
  "Prop7.25": 32,
  "Prop7.26": 62,
  "Prop7.27": 126,
  "Prop7.28": 0,
  "Prop7.29": 0,
  "Prop7.30": 78,
  "Prop7.31": 0,
  "Prop7.32": 1,
  "Prop7.33": 93,
  "Prop7.34": 346,
  "Prop7.35": 0,
  "Prop7.36": 347,
  "Prop7.37": 7,
  "Prop7.38": 7,
  "Prop7.39": 1009,
  "Prop8.1": 38,
  "Prop8.2": 202,
  "Prop8.3": 391,
  "Prop8.4": 385,
  "Prop8.5": 578,
  "Prop8.6": 490,
  "Prop8.7": 491,
  "Prop8.8": 686,
  "Prop8.9": 595,
  "Prop8.10": 54,
  "Prop8.11": 55,
  "Prop8.12": 111,
  "Prop8.13": 25,
  "Prop8.14": 548,
  "Prop8.15": 603,
  "Prop8.16": 1096,
  "Prop8.17": 1206,
  "Prop8.18": 138,
  "Prop8.19": 305,
  "Prop8.20": 491,
  "Prop8.21": 1476,
  "Prop8.22": 593,
  "Prop8.23": 1573,
  "Prop8.24": 1324,
  "Prop8.25": 2086,
  "Prop8.26": 340,
  "Prop8.27": 609,
  "Prop9.1": 1468,
  "Prop9.2": 585,
  "Prop9.3": 1673,
  "Prop9.4": 2541,
  "Prop9.5": 2541,
  "Prop9.6": 2087,
  "Prop9.7": 1,
  "Prop9.8": 1669,
  "Prop9.9": 6748,
  "Prop9.10": 6404,
  "Prop9.11": 7,
  "Prop9.12": 103,
  "Prop9.13": 1321,
  "Prop9.14": 79,
  "Prop9.15": 8814,
  "Prop9.16": 23,
  "Prop9.17": 38,
  "Prop9.18": 94,
  "Prop9.19": 156,
  "Prop9.20": 395,
  "Prop9.21": 1,
  "Prop9.22": 3,
  "Prop9.23": 4,
  "Prop9.24": 1,
  "Prop9.25": 2,
  "Prop9.26": 2,
  "Prop9.27": 2,
  "Prop9.28": 3,
  "Prop9.29": 6,
  "Prop9.30": 5,
  "Prop9.31": 6,
  "Prop9.32": 1323,
  "Prop9.33": 2,
  "Prop9.34": 2,
  "Prop9.35": 122,
  "Prop9.36": 1550,
  "Prop10.1": 1,
  "Prop10.2": 3,
  "Prop10.3": 4,
  "Prop10.4": 7,
  "Prop10.5": 21,
  "Prop10.6": 45,
  "Prop10.7": 46,
  "Prop10.8": 22,
  "Prop10.9": 6512,
  "Prop10.10": 6571,
  "Prop10.11": 112,
  "Prop10.12": 185,
  "Prop10.13": 1158,
  "Prop10.14": 6689,
  "Prop10.15": 2,
  "Prop10.16": 2,
  "Prop10.17": 1381,
  "Prop10.18": 1163,
  "Prop10.19": 6806,
  "Prop10.20": 6813,
  "Prop10.21": 6802,
  "Prop10.22": 20510,
  "Prop10.23": 27338,
  "Prop10.24": 27340,
  "Prop10.25": 40987,
  "Prop10.26": 21734,
  "Prop10.27": 47885,
  "Prop10.28": 48158,
  "Prop10.29": 58068,
  "Prop10.30": 58201,
  "Prop10.31": 106227,
  "Prop10.32": 133652,
  "Prop10.33": 181803,
  "Prop10.34": 287981,
  "Prop10.35": 289265,
  "Prop10.36": 1378,
  "Prop10.37": 2758,
  "Prop10.38": 94652,
  "Prop10.39": 183273,
  "Prop10.40": 290729,
  "Prop10.41": 291892,
  "Prop10.42": 23116,
  "Prop10.43": 294951,
  "Prop10.44": 1309158,
  "Prop10.45": 206409,
  "Prop10.46": 1267169,
  "Prop10.47": 1032066,
  "Prop10.48": 59635,
  "Prop10.49": 59746,
  "Prop10.50": 59768,
  "Prop10.51": 59746,
  "Prop10.52": 96219,
  "Prop10.53": 155097,
  "Prop10.54": 269157,
  "Prop10.55": 425127,
  "Prop10.56": 291914,
  "Prop10.57": 474001,
  "Prop10.58": 1244932,
  "Prop10.59": 499012,
  "Prop10.60": 924346,
  "Prop10.61": 655414,
  "Prop10.62": 1094338,
  "Prop10.63": 1193562,
  "Prop10.64": 1296783,
  "Prop10.65": 1032189,
  "Prop10.66": 218833,
  "Prop10.67": 103548,
  "Prop10.68": 1179433,
  "Prop10.69": 290730,
  "Prop10.70": 291893,
  "Prop10.71": 3149302,
  "Prop10.72": 7230255,
  "Prop10.73": 1389,
  "Prop10.74": 48197,
  "Prop10.75": 95072,
  "Prop10.76": 183312,
  "Prop10.77": 1161386,
  "Prop10.78": 293304,
  "Prop10.79": 22123,
  "Prop10.80": 49559,
  "Prop10.81": 144783,
  "Prop10.82": 206448,
  "Prop10.83": 1268054,
  "Prop10.84": 316615,
  "Prop10.85": 60996,
  "Prop10.86": 60996,
  "Prop10.87": 61018,
  "Prop10.88": 60996,
  "Prop10.89": 60996,
  "Prop10.90": 61018,
  "Prop10.91": 276305,
  "Prop10.92": 324553,
  "Prop10.93": 433303,
  "Prop10.94": 530651,
  "Prop10.95": 1270208,
  "Prop10.96": 595009,
  "Prop10.97": 507233,
  "Prop10.98": 612299,
  "Prop10.99": 709409,
  "Prop10.100": 767845,
  "Prop10.101": 1318381,
  "Prop10.102": 878742,
  "Prop10.103": 222113,
  "Prop10.104": 152130,
  "Prop10.105": 1800881,
  "Prop10.106": 1161387,
  "Prop10.107": 293305,
  "Prop10.108": 1591181,
  "Prop10.109": 1823518,
  "Prop10.110": 1712786,
  "Prop10.111": 2718637,
  "Prop10.112": 238002,
  "Prop10.113": 323185,
  "Prop10.114": 554319,
  "Prop10.115": 6815,
  "Prop11.1": 0,
  "Prop11.2": 1,
  "Prop11.3": 0,
  "Prop11.4": 97,
  "Prop11.5": 100,
  "Prop11.6": 376,
  "Prop11.7": 1,
  "Prop11.8": 290,
  "Prop11.9": 566,
  "Prop11.10": 1175,
  "Prop11.11": 529,
  "Prop11.12": 1145,
  "Prop11.13": 2,
  "Prop11.14": 141,
  "Prop11.15": 1238,
  "Prop11.16": 139,
  "Prop11.17": 3562,
  "Prop11.18": 381,
  "Prop11.19": 3,
  "Prop11.20": 498,
  "Prop11.21": 1314,
  "Prop11.22": 818,
  "Prop11.23": 9617,
  "Prop11.24": 1481,
  "Prop11.25": 1508,
  "Prop11.26": 669,
  "Prop11.27": 3893,
  "Prop11.28": 4962,
  "Prop11.29": 5526,
  "Prop11.30": 5527,
  "Prop11.31": 11308,
  "Prop11.32": 16834,
  "Prop11.33": 34461,
  "Prop11.34": 22406,
  "Prop11.35": 2256,
  "Prop11.36": 31152,
  "Prop11.37": 34463,
  "Prop11.38": 1845,
  "Prop11.39": 16291,
  "Prop12.1": 45529,
  "Prop12.2": 58126,
  "Prop12.3": 74430,
  "Prop12.4": 133427,
  "Prop12.5": 191621,
  "Prop12.6": 210131,
  "Prop12.7": 193364,
  "Prop12.8": 320911,
  "Prop12.9": 22443,
  "Prop12.10": 251620,
  "Prop12.11": 451468,
  "Prop12.12": 893516,
  "Prop12.13": 452495,
  "Prop12.14": 704180,
  "Prop12.15": 704319,
  "Prop12.16": 1463,
  "Prop12.17": 19754,
  "Prop12.18": 78024,
  "Prop13.1": 58,
  "Prop13.2": 2582,
  "Prop13.3": 117,
  "Prop13.4": 117,
  "Prop13.5": 133,
  "Prop13.6": 507476,
  "Prop13.7": 58,
  "Prop13.8": 3073,
  "Prop13.9": 6012,
  "Prop13.10": 9899,
  "Prop13.11": 1169287,
  "Prop13.12": 9648,
  "Prop13.13": 24910,
  "Prop13.14": 8586,
  "Prop13.15": 7535,
  "Prop13.16": 1237611,
  "Prop13.17": 716773,
  "Prop13.18": 1621828
}
```

</details>

## Prepare data structure in blender






Next, we propagate these datablocks into the network:

<details>
<summary>Full Blender script (click to expand)</summary>

```py
import bpy
import databpy as db
import json
import math
import re
from pathlib import Path

# load all_books_processed.json

data_file = Path('all_books_processed.json')
all_books_processed = json.loads(data_file.read_text())

print(f"Loaded data for {len(all_books_processed)} books")
print(f"Books: {list(all_books_processed.keys())}")

# Show structure of first book
first_book = list(all_books_processed.keys())[0]
print(f"Sample entries: {list(all_books_processed[first_book].keys())[:5]}")

def delete_collections_and_purge(collections_to_delete=['Books']):
    """Delete specified collections and all elements in them, then purge unused data blocks"""
    for collection_name in collections_to_delete:
        collection = bpy.data.collections.get(collection_name)
        if collection:
            
            # Remove all objects from the collection
            for obj in collection.objects:
                bpy.data.objects.remove(obj, do_unlink=True)
            
            # Remove the collection itself
            bpy.data.collections.remove(collection)

    # Purge unused data blocks
    bpy.ops.outliner.orphans_purge(do_local_ids=True, do_linked_ids=True, do_recursive=True)



delete_collections_and_purge()


# Load recursive counts data
recursive_counts_path = Path('recursive_counts.json')
with recursive_counts_path.open('r') as f:
        recursive_counts = json.load(f)


# Create a top-level books collection
books_collection = db.create_collection(name="Books", parent=None)

# Process all books
placed_propositions = set()  # Track which propositions we've already placed
placed_definitions = set()  # Track which definitions we've already placed
placed_common_notions = set()  # Track which common notions we've already placed
placed_postulates = set()  # Track which postulates we've already placed

for book_idx, (book_name, book_data) in enumerate(all_books_processed.items()):
    print(f"Processing {book_name} with {len(book_data)} entries")
    
    # Create a collection for this book under the books collection
    book_collection = db.create_collection(name=book_name, parent=books_collection)
    
    # Calculate scale factor based on book index (start at 1.0 for first book, decrease by 0.1 for each subsequent book)
    scale_factor = book_idx

    # Collect all unique strings from keys and values
    all_strings = set(book_data.keys())
    for values in book_data.values():
        all_strings.update(values)

    # Use regex to categorize strings and sort them numerically
    def sort_key(s):
        """Extract numbers from string for proper numerical sorting"""
        if re.match(r'^D\d+\.\d+$', s):
            parts = s[1:].split('.')
            return (int(parts[0]), int(parts[1]))
        elif re.match(r'^CN\.\d+$', s):
            return (0, int(s.split('.')[1]))
        elif re.match(r'^Post\.\d+$', s):
            return (0, int(s.split('.')[1]))
        elif re.match(r'^Prop\d+\.\d+$', s):
            parts = s[4:].split('.')
            return (int(parts[0]), int(parts[1]))
        return (0, 0)

    D = sorted([s for s in all_strings if re.match(r'^D\d+\.\d+$', s)], key=sort_key)
    print(f"D: {D}")
    CN = sorted([s for s in all_strings if re.match(r'^CN\.\d+$', s)], key=sort_key)
    print(f"CN: {CN}")
    Post = sorted([s for s in all_strings if re.match(r'^Post\.\d+$', s)], key=sort_key)
    print(f"Post: {Post}")
    Prop = sorted([s for s in all_strings if re.match(r'^Prop\d+\.\d+$', s)], key=sort_key)
    print(f"Prop: {Prop}")


    # Create D collection for this book
    d_collection = db.create_collection(name=f'{book_name}_D', parent=book_collection)

    # Get the source D object
    d1_obj = bpy.data.objects['1D']

    new_d = [d_name for d_name in D if d_name not in placed_definitions]

    # get the DefinitionsCurve object
    definitions_curve_collection = db.create_collection(name=f'{book_name}_DefinitionsCurve', parent=book_collection)
    
    definitions_curve_obj = bpy.data.objects['DefinitionsCurve']
    definitions_curve_copy = definitions_curve_obj.copy()
    definitions_curve_copy.name = f"{book_name}_DefinitionsCurve"
    definitions_curve_collection.objects.link(definitions_curve_copy)
    definitions_curve_copy.modifiers["GeometryNodes"]["Socket_3"] = book_idx +1 # CurrentBook
    definitions_curve_copy.modifiers["GeometryNodes"]["Socket_4"] = len(new_d)  # NumberofProps
    definitions_curve_copy.modifiers["GeometryNodes"]["Socket_5"] = -(book_idx +1) /13  *math.pi# StartAngle


    # Create copies for each D element - only if not already placed
    for i, d_name in enumerate(D):
        if d_name not in placed_definitions:
            d_copy = d1_obj.copy()
            d_copy.name = f"{book_name}_{d_name}"
            d_collection.objects.link(d_copy)
            # Set the String socket value to the D element name
            d_copy.modifiers["GeometryNodes"]["Socket_2"] = d_name
            # Set the scale factor based on book index
            d_copy.modifiers["GeometryNodes"]["Socket_6"] = scale_factor
            # Place them at the origin
            d_copy.location = (0, 0, 0)
            placed_definitions.add(d_name)
            d_copy.modifiers["GeometryNodes"]["Socket_7"] = bpy.data.objects[f"{book_name}_DefinitionsCurve"]
            d_copy.modifiers["GeometryNodes"]["Socket_8"] = int(d_name.split('.')[-1]) if '.' in d_name else 0


    cn_collection = db.create_collection(name=f'{book_name}_CN', parent=book_collection)

    # Get the source CN object
    cn1_obj = bpy.data.objects['2CN']

    # Create copies for each CN element - only if not already placed
    for i, cn_name in enumerate(CN):
        if cn_name not in placed_common_notions:
            cn_copy = cn1_obj.copy()
            cn_copy.name = f"{book_name}_{cn_name}"
            cn_collection.objects.link(cn_copy)
            # Set the String socket value to the CN element name
            cn_copy.modifiers["GeometryNodes"]["Socket_2"] = cn_name
            # Set the scale factor based on book index
            cn_copy.modifiers["GeometryNodes"]["Socket_6"] = scale_factor
            # Place them at the origin
            cn_copy.location = (0, 0, 0)
            placed_common_notions.add(cn_name)

    post_collection = db.create_collection(name=f'{book_name}_Post', parent=book_collection)

    # Get the source Post object
    post1_obj = bpy.data.objects['3Post']

    # Create copies for each Post element - only if not already placed
    for i, post_name in enumerate(Post):
        if post_name not in placed_postulates:
            post_copy = post1_obj.copy()
            post_copy.name = f"{book_name}_{post_name}"
            post_collection.objects.link(post_copy)
            # Set the String socket value to the Post element name
            post_copy.modifiers["GeometryNodes"]["Socket_2"] = post_name
            # Set the scale factor based on book index
            post_copy.modifiers["GeometryNodes"]["Socket_6"] = scale_factor
            # Place them at the origin
            post_copy.location = (0, 0, 0)
            placed_postulates.add(post_name)

    prop_collection = db.create_collection(name=f'{book_name}_Prop', parent=book_collection)

    # Get the source Prop object
    prop1_obj = bpy.data.objects['4Prop']

    # Create copies for each Prop element - only if not already placed
    # First, collect the new propositions that haven't been placed
    new_props = [prop_name for prop_name in Prop if prop_name not in placed_propositions]
    # Reverse the list of new propositions


    # Create book text collection for this book
    book_text_collection = db.create_collection(name=f'{book_name}_BookText', parent=book_collection)

    # Get the source BookText object
    book_text_obj = bpy.data.objects['RefBookString']

    book_text_copy = book_text_obj.copy()
    book_text_copy.name = f"{book_name}_BookText"
    book_text_collection.objects.link(book_text_copy)
    book_text_copy.modifiers["GeometryNodes"]["Socket_5"] = book_idx +1
    book_text_copy.modifiers["GeometryNodes"]["Socket_4"] = book_idx +1 # CurrentBook


    # Get the source BookSpiral object
    book_spiral_collection = db.create_collection(name=f'{book_name}_BookSpiral', parent=book_collection)

    book_spiral_obj = bpy.data.objects['BookSpiral']
    book_spiral_copy = book_spiral_obj.copy()
    book_spiral_copy.name = f"{book_name}_BookSpiral"
    book_spiral_collection.objects.link(book_spiral_copy)
    book_spiral_copy.modifiers["GeometryNodes"]["Socket_3"] = book_idx +1 # CurrentBook
    book_spiral_copy.modifiers["GeometryNodes"]["Socket_4"] = len(new_props)  # NumberofProps



    # new_props = new_props[::-1]
    for i, prop_name in enumerate(Prop):
        if prop_name not in placed_propositions:
            prop_copy = prop1_obj.copy()
            prop_copy.name = f"{book_name}_{prop_name}"
            prop_collection.objects.link(prop_copy)

            # Set the String socket value to the Prop element name
            prop_copy.modifiers["GeometryNodes"]["Socket_2"] = prop_name

            # Set the scale factor based on recursive counts
            if prop_name in recursive_counts:
                node_scale_factor = max(1, recursive_counts[prop_name])  # At least 1
            else:
                node_scale_factor = 1  # Default scale if no recursive count found
                print(f"No recursive count found for {prop_name}")

            prop_copy.modifiers["GeometryNodes"]["Socket_6"] = int(node_scale_factor)
            prop_copy.modifiers["GeometryNodes"]["Socket_8"] = bpy.data.objects[f"{book_name}_BookSpiral"]
            prop_copy.modifiers["GeometryNodes"]["Socket_9"] = int(prop_name.split('.')[-1]) if '.' in prop_name else 0



            # Place them all at the origin
            prop_copy.location = (0, 0, 0)
            placed_propositions.add(prop_name)

    # Create simple lines for all connections by copying the "Line" object
    line_collection = db.create_collection(name=f'{book_name}_Lines', parent=book_collection)

    # Get the source Line object
    source_line_obj = bpy.data.objects['Line']

    # Get all keys from book_data
    for key, values in book_data.items():
        # If the dictionary has values (dependencies)
        if values:
            # Iterate over every dependency name in values
            for dependency in values:
                # Copy the existing Line object
                line_copy = source_line_obj.copy()
                line_copy.name = f"{book_name}_Line_{key}_to_{dependency}"
                
                # Set the source and target dependencies in the modifiers
                key_obj_name = f"{book_name}_{key}"
                
                # Find the dependency object - look for the first occurrence across all books
                dependency_obj_name = None
                for prev_book_name, _ in list(all_books_processed.items())[:book_idx + 1]:
                    candidate_name = f"{prev_book_name}_{dependency}"
                    if bpy.data.objects.get(candidate_name) is not None:
                        dependency_obj_name = candidate_name
                        break
                
                # If not found in any book, try current book
                if dependency_obj_name is None:
                    dependency_obj_name = f"{book_name}_{dependency}"
                
                dependency_obj = bpy.data.objects.get(dependency_obj_name)
                key_obj = bpy.data.objects.get(key_obj_name)
                
                if dependency_obj is not None and key_obj is not None:
                    line_copy.modifiers["GeometryNodes"]["Socket_2"] = bpy.data.objects[dependency_obj_name]
                    line_copy.modifiers["GeometryNodes"]["Socket_3"] = bpy.data.objects[key_obj_name]
                    
                    # Add to the Lines collection
                    line_collection.objects.link(line_copy)

    print(f"Created {len(line_collection.objects)} simple dependency lines for {book_name}")

```

</details>



If you come up with your own creations and post them online, you're welcome to tag me on [Bluesky](https://bsky.app/profile/kolibril13.bsky.social)!
