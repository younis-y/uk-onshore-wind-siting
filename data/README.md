# Input data

None of these files are committed. Together they are roughly 340 MB, most of it
in the three conservation-designation shapefiles, and all of them are published
by their originators in a form you can download directly. Fetching them yourself
also means you get the current release rather than a frozen 2025 copy.

Place each file in the working directory alongside the notebook, keeping the
names below — the notebook refers to them by relative path.

| File | Source | Licence |
|---|---|---|
| `Countries_December_2021_UK_BGC_.gpkg` | ONS Open Geography Portal — Countries (December 2021) UK BGC boundaries | Open Government Licence v3 |
| `GB-SAC/GB_SAC_OSGB36_20250401.shp` | JNCC / Natural England — Special Areas of Conservation | Open Government Licence v3 |
| `GB-SPA/GB_SPA_OSGB36_20240509.shp` | JNCC / Natural England — Special Protection Areas | Open Government Licence v3 |
| `GB-RAMSAR/UK_RAMSAR_BNG_20210308.shp` | JNCC — Ramsar wetland sites | Open Government Licence v3 |
| `REPD_Publication_Q3_2025.csv` | DESNZ — Renewable Energy Planning Database, Q3 2025 | Open Government Licence v3 |
| `terrain.tif` | Terrain raster used for the slope criterion | see note below |
| `wind_speed.nc` | Seasonal mean wind speed, NetCDF with a `season` dimension | see note below |

Contains public sector information licensed under the Open Government Licence
v3.0. The OGL requires attribution, which is why each source is named above
rather than described generically.

## The two rasters

`terrain.tif` and `wind_speed.nc` were prepared during the coursework and their
exact provenance is not recorded in the notebook. They are small enough to have
been committed, and they are deliberately not, because shipping a raster whose
licence I cannot state would be worse than making you substitute your own.

Any equivalent source works. The notebook needs a terrain raster it can reproject
to EPSG:27700 and mask to the GB boundary, and a NetCDF carrying a `wind_speed`
variable with a `season` dimension. If you are rebuilding these, the Global Wind
Atlas and OS Terrain 50 are the obvious candidates, both freely available.

## Projection

Every layer is reprojected to EPSG:27700 (British National Grid) before any
overlay or distance calculation. Mixing a geographic CRS into a distance
threshold is the standard way to get a plausible and wrong answer out of this
kind of screening, so the reprojection is done once, up front, rather than per
operation.
