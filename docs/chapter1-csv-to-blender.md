---
title: "Chapter 1: CSV to Blender"
---

# Chapter 1: CSV to Blender

```python
from io import StringIO
from pathlib import Path
import bpy

from csv_importer.csv import load_csv

# ----------------------------------
# 1. CSV content
# ----------------------------------
csv_data = StringIO(
    """
FloatVal,IntVal,BoolVal,StringVal
1.23,10,true,Hello
4.56,20,false,World
"""
)

# ----------------------------------
# 2. Writable temp path
# ----------------------------------
temp_dir = Path(bpy.app.tempdir)
csv_path = temp_dir / "example.csv"

csv_path.write_text(csv_data.getvalue().strip(), encoding="utf-8")

# ----------------------------------
# 3. Load CSV
# ----------------------------------
obj = load_csv(csv_path)
print(obj.name)
```

![CSV imported into Blender](assets/csv-to-blender-result.png)


# DataFrame to Blender
```py
import polars as pl
from csv_importer.parsers import polars_df_to_bob

df = pl.DataFrame({
    "Intensity": ["Hello", "World"],
    "opacity": [0.34, 0.92],
    "Is_Visible": [True, False],
    "Star": [
        [3.4, 3.5, 0.0],
        [3.1, 5.6, 0.0]
    ]
})
obj = polars_df_to_bob(df, name="MeshVector")
``` 


# JSON to Blender

```py

```

# Excel to Blender
```py

```