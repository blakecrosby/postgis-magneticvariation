# postgis-magneticvariation
A PostgreSQL/PostGIS table of magnetic variation values.

# Data Source
Data was sourced from The World Magnetic Model found at: https://www.ngdc.noaa.gov/geomag/WMM/. WMM2020 was used (valid until 20225).

NOTE: This data set includes values for (-60,-179) to (60,179) only.

# Schema
The PostGIS table (called 'magvar') contains  the following schema:
```
    id integer NOT NULL
    location public.geometry(Point,4326)
    year integer
    variation double precision
```
NOTE: This table uses the `geometry` type with SRID 4326. Not the (new) `geography` type. 

The value 'variation' is either positive (east variation) or negative (west variation)

## Indicies
Two indicies are cerated, one on `year` and a gist index on `location`.

# Example

```SELECT variation FROM magvar WHERE year = 2022 ORDER BY location <-> ST_GeometryFromText('POINT(-79.3 43.6)',4326) LIMIT 1```

will return:

