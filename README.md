# VOCMIP input data repository

This is a input data repostitory for the [VOCMIP](https://cicero.oslo.no/en/projects/vocmip) experiment [GMD - Introducing Volatile Organic Compound Model Intercomparison Project (VOCMIP)](https://gmd.copernicus.org/articles/19/2577/2026/)


# Emissions

## Emission Inputs

### Anthropogenic emissions

`CEDS_v2021`: CEDS v2021 gridded emissions are available to 2019. Data can be downloaded here: [CEDS v_2021_04_21 gridded emissions data | Datahub (PNNL)](https://data.pnnl.gov/dataset/CEDS-4-21-21).

Use the corrected version of the aircraft emission data: [CEDS Version 2021-04-21 Aircraft Emissions Fix](https://zenodo.org/records/7846185).

For Phase II simulations, a more recent release of CEDS will be used.

### Biomass burning emissions

For biomass burning emissions, [GFEDv4](https://www.geo.vu.nl/~gwerf/GFED/GFED4/) is preferred.

### Natural emissions

Model's own choice, but diagnose/specify in as much detail as possible. Total emissions (anthropogenic and natural) should be diagnosed and delivered ([VOCMIP_diagnostics.xlsx](data/VOCMIP_diagnostics.xlsx)).

## Boundary conditions

### H2 boundary conditions

For hydrogen surface concentration fields to drive the models for the years 2015-2019, the NOAA flask observations (Petron et al. 2024) have been used in the following manner. All stations that had monthly data for every month in a given year have been used to make smoothed monthly zonal fields using the lowess algorithm to a smoothness of `0.5`.

Input file is available in the `data/` folder of this repository: [`hydrogen_concentrations_lowess_201001-201912.nc`](data/hydrogen_concentrations_lowess_201001-201912.nc)

### CH4 boundary conditions

The methane boundary conditions should be a latitudinally varying surface field, for example as provided for CMIP6 up to 2014. The annual global values should match the NOAA observations listed in Table 1. The methane concentration should be representative for the years 2015 to 2019.

Model's own choice how the boundary condition is implemented in the model, but the global values should match the NOAA global observations.

Table 1: Global evolution 2010-2019 of CH4 from the [NOAA observations](https://gml.noaa.gov/webdata/ccgg/trends/ch4/ch4_annmean_gl.txt).

| Year | Mean (ppb) |
| --- | ---: |
| 2010 | 1798.89 |
| 2011 | 1803.09 |
| 2012 | 1808.12 |
| 2013 | 1813.43 |
| 2014 | 1822.53 |
| 2015 | 1834.26 |
| 2016 | 1843.12 |
| 2017 | 1849.58 |
| 2018 | 1857.33 |
| 2019 | 1866.58 |

Files on 1 by 1 degree resolution are in the `data/` folder of this repository:

- [`methane_concentrations_1by1_2010.nc`](data/methane_concentrations_1by1_2010.nc)
- [`methane_concentrations_1by1_2011.nc`](data/methane_concentrations_1by1_2011.nc)
- [`methane_concentrations_1by1_2012.nc`](data/methane_concentrations_1by1_2012.nc)
- [`methane_concentrations_1by1_2013.nc`](data/methane_concentrations_1by1_2013.nc)
- [`methane_concentrations_1by1_2014.nc`](data/methane_concentrations_1by1_2014.nc)
- [`methane_concentrations_1by1_2015.nc`](data/methane_concentrations_1by1_2015.nc)
- [`methane_concentrations_1by1_2016.nc`](data/methane_concentrations_1by1_2016.nc)
- [`methane_concentrations_1by1_2017.nc`](data/methane_concentrations_1by1_2017.nc)
- [`methane_concentrations_1by1_2018.nc`](data/methane_concentrations_1by1_2018.nc)
- [`methane_concentrations_1by1_2019.nc`](data/methane_concentrations_1by1_2019.nc)

### Long-lived GHG and ODS boundary conditions

If possible, use `ssp245`, but it should at least correspond to the time period simulated.

## Filenames

Each variable should be delivered in one (or several divided into different time slices if necessary) file for each experiment and model.

The format of the file name should be:

```text
<variable_id>_<table_id>_<model_id>_vocmip_<experiment_id>_<member_id>_<time_range>.nc
```

Exceptions are for `table_id` `fixed`:

```text
<variable_id>_<table_id>_<model_id>_hyway.nc
```

These are fixed variables that do not change by time and experiments.

Table 2: Description of the different elements in the file names.

| Element | Description |
| --- | --- |
| `<variable_id>` | The output variable name. Given as `Output variable name` in the spreadsheet. |
| `<table_id>` | Denote the temporal resolution such as `monthly` for monthly data, `fixed` for fixed data, and `3hourly` for 3-hourly instantaneous data. Given as the name (ignore the dimensions, `3D`, `2D`) of the tab in the spreadsheet. |
| `<model_id>` | The name of your model. |
| `<experiment_id>` | The name of the experiment, `exp` following the experiment number given in Table 1 in [GMD - Introducing Volatile Organic Compound Model Intercomparison Project (VOCMIP)](https://gmd.copernicus.org/articles/19/2577/2026/). |
| `<member_id>` | If more ensembles are run: `r1`, `r2`, etc. |
| `<time_range>` | Denotes the start and end date of the run on `YYYYMM-YYYYMM` or `YYYYMMDD-YYYYMMDD` format. |

### Example

```text
hcho_monthly_OsloCTM3-v3X_vocmip_exp1_r1_201001-201912.nc
```

