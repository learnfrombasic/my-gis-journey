# My GIS Journey

A collection of notebook-based GIS and spatial-analysis projects using Python. The current notebooks explore restaurant locations and ratings in Bangalore and Uber pickup patterns across New York City.

## Projects

| Notebook | Analysis |
| --- | --- |
| [`notebooks/spatial_analysis_zomato.ipynb`](notebooks/spatial_analysis_zomato.ipynb) | Explores Bangalore restaurant data, prepares geographic coordinates, maps restaurant density and clusters, cleans rating values, and compares highly rated restaurants. |
| [`notebooks/uber_spatial_analysis.ipynb`](notebooks/uber_spatial_analysis.ipynb) | Joins September 2014 Uber pickup coordinates to NYC taxi zones and explores busy pickup areas, pickup clusters, and demand by hour and day type. |

The Uber notebook exports an interactive hourly demand map to [`outputs/uber_demand_by_hour.html`](outputs/uber_demand_by_hour.html).

## Data

Place the supplied data in the existing `data/` directory:

- `data/zomato.csv` is the Bangalore restaurant dataset used by the Zomato notebook (approximately 547 MB).
- `data/uber-raw-data-sep14.csv` contains NYC Uber pickup timestamps, latitude/longitude, and base identifiers for September 2014 (approximately 45 MB).
- `data/taxi_zones/` contains the NYC taxi-zone shapefile and its supporting `.dbf`, `.prj`, and `.shx` files. Keep these files together.

The datasets are not installed by the setup commands below. Their source and usage terms may differ from the license for this repository; check the applicable terms before redistributing them.

## Setup

The project uses Python 3.14 or later. From the repository root, create and activate a virtual environment, then install the notebook dependencies:

```bash
python3.14 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install jupyter pandas numpy matplotlib seaborn geopy folium geopandas shapely
```

The `pyproject.toml` currently contains project metadata but does not declare these notebook dependencies.

## Run the Notebooks

Start Jupyter from the repository root:

```bash
jupyter notebook
```

Open a notebook under `notebooks/` and run its cells from top to bottom. The Uber notebook resolves its input files from the repository's `data/` directory. The Zomato notebook currently contains a Windows-specific CSV path; change its `pd.read_csv(...)` argument to `../data/zomato.csv` when the notebook's working directory is `notebooks/`, or `data/zomato.csv` when Jupyter was started from the repository root.

The Zomato analysis uses OpenStreetMap's Nominatim geocoder to look up restaurant locations. This requires an internet connection, can issue many requests, and may be slow or rate-limited. Follow the geocoding service's usage policy; do not repeatedly geocode the full dataset when cached coordinates are available.

## Acknowledgements

The learning material and tutorial inspiration are credited in [`docs/ACKNOWLEDGEMENTS.md`](docs/ACKNOWLEDGEMENTS.md).

## License

The project is distributed under the Apache License 2.0; see [`LICENSE`](LICENSE). This license notice does not necessarily cover the datasets or external map/geocoding services.
