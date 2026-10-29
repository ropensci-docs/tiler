# tiler: Create Geographic and Non-Geographic Map Tiles

Creates geographic map tiles from geospatial map files or non-geographic
map tiles from simple image files. This package provides a tile
generator function for creating map tile sets for use with packages such
as 'leaflet'. In addition to generating map tiles based on a common
raster layer source, it also handles the non-geographic edge case,
producing map tiles from arbitrary images. These map tiles, which have a
non-geographic, simple coordinate reference system (CRS), can also be
used with 'leaflet' when applying the simple CRS option. Map tiles can
be created from an input file with any of the following extensions: tif,
grd and nc for spatial maps and png, jpg and bmp for basic images. This
package requires 'Python' and the 'gdal' library for 'Python'. 'Windows'
users are recommended to install 'OSGeo4W'
(<https://trac.osgeo.org/osgeo4w/>) as an easy way to obtain the
required 'gdal' support for 'Python'.

## See also

Useful links:

- <https://docs.ropensci.org/tiler/>

- <https://github.com/ropensci/tiler>

- Report bugs at <https://github.com/ropensci/tiler/issues>

## Author

**Maintainer**: Matthew Leonawicz <rpkgs@pm.me>
([ORCID](https://orcid.org/0000-0001-9452-2771))

Other contributors:

- Alex M Chubaty <achubaty@for-cast.ca>
  ([ORCID](https://orcid.org/0000-0001-7146-8135)) \[contributor\]
