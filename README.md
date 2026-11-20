# Figure code

Notebooks that reproduce the figures of the paper from the data files in this
deposit. Each notebook reads only the NetCDF files; there are no paths to the
model archive, no processing pipeline and no model configuration anywhere in this
code. Download the data files and the notebooks into one folder and run them.

| Notebook | Figures | Data files |
|---|---|---|
| `plot_Figure1.ipynb` | 1 | `Figure1_ssh_variability_<region>.nc` |
| `plot_Figure2.ipynb` | 2, and its two supporting-information counterparts | `Figure2_<region>_<product>_<cycle>.nc` |
| `plot_Figures3_4.ipynb` | 3, 4 | `Figures3_4_eddy_population_statistics.nc` |
| `plot_Figures5_6.ipynb` | 5, 6 | `Figures5_6_day1_eddy_persistence.nc` |
| `plot_Figure7.ipynb` | 7 | `Figure7_matching_statistics.nc` |
| `plot_Figures8_9_10.ipynb` | 8, 9, 10 | `Figures8_9_composite_<region>.nc`, `Figure10_radial_profiles.nc` |
| `plot_Figure11.ipynb` | 11 | `Figure11_swot_repeat_statistics_<region>.nc` |
| `plot_FigureS6.ipynb` | S6 | `FigureS6_spectra_<region>_<cycle>.nc`, `FigureS6_input_ssh_<region>_<cycle>.nc` |
| `plot_FigureS7.ipynb` | S7 | `FigureS7_matching_example_<region>_<cycle>.nc`, `FigureS7_separations_leadday1.nc` |

Set `DATA` at the top of a notebook if the files are in another folder. Figures are
written to `figures/`.

## Requirements

`numpy`, `xarray`, `netCDF4`, `matplotlib`. `cartopy` is used for coastlines in the
map figures; without it, or on a machine that cannot reach its coastline data, the
notebooks say so and draw the maps without them.

## What is in the deposit

Everything plotted in the figures, from both sides of every comparison: the
forecast, the mapped altimetry it is evaluated against, and the SWOT ground-track
statistics. Each file is self-describing — the method, the population, the
uncertainty and the caveats are recorded as attributes, so a panel can be
interpreted without returning to the paper.

Files are organised by what they support, not by variable:

- **Fields and detections** carry their eddy contours as a CF contiguous ragged
  array. The vertices of eddy `i` run from `contour_vertex_start[i]` for
  `contour_vertex_count[i]` points.
- **Statistics by lead day** have dimensions `(region, product, polarity,
  lead_day)`, each metric alongside a `_se` companion that is the half-width of the
  shaded band in the figure.
- **Composites** are on a grid normalised by each eddy's own radius. Alongside the
  lead-day-1 field and the change, they carry `*_reference`: the lead-day-1
  composite of *the eddies surviving to that day*, which is the baseline each
  change is differenced against. Comparing the two separates a real change from the
  shrinking population.
- **Derived diagnostics** — eddy separations, matching rates, and the standard
  deviations on the SWOT ground track — are distances and ratios rather than
  fields, and are archived in full.

Two conventions worth knowing. The `product` coordinate takes the values
`observed` and `forecast`. The altimetry has no forecast, so where a lead day is
given for it, that is the valid day matching the forecast, recorded in each file's
`altimetry_lead_day_note` or `lead_day_note`.

## Attribution

These files are a derivative work: subsets, detections and statistics computed by
the authors, not copies of any distributed product. Both source products permit
this, on condition that the credit travels with the derivative. Every file holding
altimetry- or SWOT-derived values carries that credit in its `licence` attribute,
and the notebooks print it below the figure. If you reuse these files, carry the
same credit forward and obtain the source products from their own archives.

The paper cites both products with their identifiers and DOIs in its Open Research
section.
