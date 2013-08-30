This [custom buildpack](https://github.com/JasonSanford/heroku-buildpack-python-geos) is used to include the GEOS binaries necessary for Shapely. To force deployment to use a custom buildpack, add the following heroku config.

    heroku config:set BUILDPACK_URL=git://github.com/JasonSanford/heroku-buildpack-python-geos.git

I *think* this buildpack will download/unpack the GEOS binaries each time you deploy which is not ideal. We should probably conditionally download these in the future.

Additionally, the `LIBRARY_PATH` must be updated so that Shapely can locate the necessary binaries.

    heroku config:set LIBRARY_PATH=/app/.heroku/vendor/lib:vendor/geos/geos/lib:vendor/proj/proj/lib:vendor/gdal/gdal/lib
    heroku config:set LD_LIBRARY_PATH=/app/.heroku/vendor/lib:vendor/geos/geos/lib:vendor/proj/proj/lib:vendor/gdal/gdal/lib

