# Brain Region Colormap 🧠🎨  
**Author:** Dipesh Pokharel  

A small, opinionated set of color codes for common brain regions used in neuroscience figures.  
Designed for **consistent, publication-ready visualizations** in:

- Rodent brain schematics  
- Circuit diagrams  
- Neuroscience figures  
- Meta-analysis plots with anatomical grouping  

---

## 1. Brain Region Color Table

| Region            | Short Name | Hex Code |
|-------------------|-----------:|:--------:|
| Primary Motor Cortex      | M1      | `#1f77b4` |
| Primary Somatosensory Cortex | S1   | `#ff7f0e` |
| Striatum         | STR        | `#2ca02c` |
| Globus Pallidus  | GP         | `#17becf` |
| Substantia Nigra | SN         | `#d62728` |
| Ventral Tegmental Area | VTA | `#9467bd` |
| Thalamus         | TH         | `#8c564b` |
| Hippocampus      | HPC        | `#e377c2` |
| Amygdala         | AMG        | `#7f7f7f` |
| Cerebellum       | CB         | `#bcbd22` |
| Brainstem        | BS         | `#aec7e8` |
| Prefrontal Cortex | PFC       | `#ff9896` |

You can adjust these colors to match your lab’s style; this is just a clean starting palette.

---

## 2. Files in This Repository

### `brain_regions_colormap.csv`

Simple CSV version of the table above:

```csv
region,short_name,hex
Primary Motor Cortex,M1,#1f77b4
Primary Somatosensory Cortex,S1,#ff7f0e
Striatum,STR,#2ca02c
Globus Pallidus,GP,#17becf
Substantia Nigra,SN,#d62728
Ventral Tegmental Area,VTA,#9467bd
Thalamus,TH,#8c564b
Hippocampus,HPC,#e377c2
Amygdala,AMG,#7f7f7f
Cerebellum,CB,#bcbd22
Brainstem,BS,#aec7e8
Prefrontal Cortex,PFC,#ff9896
{
  "Primary Motor Cortex":        "#1f77b4",
  "Primary Somatosensory Cortex":"#ff7f0e",
  "Striatum":                    "#2ca02c",
  "Globus Pallidus":             "#17becf",
  "Substantia Nigra":            "#d62728",
  "Ventral Tegmental Area":      "#9467bd",
  "Thalamus":                    "#8c564b",
  "Hippocampus":                 "#e377c2",
  "Amygdala":                    "#7f7f7f",
  "Cerebellum":                  "#bcbd22",
  "Brainstem":                   "#aec7e8",
  "Prefrontal Cortex":           "#ff9896"
}
import json
from pathlib import Path

import matplotlib.pyplot as plt

# Load JSON colormap
this_dir = Path(__file__).resolve().parent
colormap_path = this_dir.parent / "brain_regions_colormap.json"

with open(colormap_path, "r") as f:
    region_colors = json.load(f)

regions = list(region_colors.keys())
colors = [region_colors[r] for r in regions]

fig, ax = plt.subplots(figsize=(6, 4))

y_pos = range(len(regions))
ax.barh(list(y_pos), [1] * len(regions), tick_label=regions)

for y, c in zip(y_pos, colors):
    ax.barh(y, 1, color=c)

ax.set_xlim(0, 1)
ax.set_xticks([])
ax.set_title("Brain Region Colormap (Dipesh Pokharel)", fontsize=10)

plt.tight_layout()

output_path = this_dir / "brain_region_colormap_preview.png"
plt.savefig(output_path, dpi=300)
print(f"Saved preview to: {output_path}")
