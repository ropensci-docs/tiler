# Create map tiles

Create geographic and non-geographic map tiles from a file.

## Usage

``` r
tile(
  file,
  tiles,
  zoom,
  crs = NULL,
  resume = FALSE,
  viewer = TRUE,
  georef = TRUE,
  ...
)
```

## Arguments

- file:

  character, input file.

- tiles:

  character, output directory for generated tiles.

- zoom:

  character, zoom levels. Example format: `"3-7"`. See details.

- crs:

  character, Proj4 string. Use this to force set the CRS of a loaded
  raster object from `file` in cases where the CRS is missing but known,
  to avoid defaulting to non-geographic tiling.

- resume:

  logical, only generate missing tiles.

- viewer:

  logical, also create `preview.html` adjacent to `tiles` directory for
  previewing tiles in the browser using Leaflet.

- georef:

  logical, for non-geographic tiles only. If `viewer = TRUE`, then the
  Leaflet widget in `preview.html` will add map markers with coordinate
  labels on mouse click to assist with georeferencing of non-geographic
  tiles.

- ...:

  additional arguments for projected maps: reprojection method or any
  arguments to
  [`raster::RGB()`](https://rspatial.github.io/terra/reference/RGB.html),
  e.g. `col` and `colNA`. See details. Other additional arguments `lng`
  and `lat` can also be passed to the tile previewer. See
  [`tile_viewer()`](https://docs.ropensci.org/tiler/reference/tile_viewer.md)
  for details.

## Value

nothing is returned but tiles are written to disk.

## Details

This function supports both geographic and non-geographic tile
generation. When `file` is a simple image file such as `png`, `tile()`
generates non-geographic, simple CRS tiles. Files that can be loaded by
the `raster` package yield geographic tiles as long as `file` has
projection information. If the raster object's Proj4 string is `NA`, it
falls back on non-geographic tile generation and a warning is thrown.

Choice of appropriate zoom levels for non-geographic image files may
depend on the size of the image. A `zoom` value may be partially ignored
for image files under certain conditions. For instance using the example
`map.png` below, when passing strictly `zoom = n` where `n` is less than
3, this still generates tiles for zoom `n` up through 3.

### Supported file types

Supported simple CRS/non-geographic image file types include `png`,
`jpg` and `bmp`. For projected map data, supported file types include
three types readable by the `raster` package: `grd`, `tif`, and `nc`
(requires `ncdf4`). Other currently unsupported file types passed to
`file` throw an error.

### Raster file inputs

If a map file loadable by `raster` is a single-layer raster object, tile
coloring is applied. To override default coloring of data and `noData`
pixels, pass the additional arguments `col` and `colNA` to `...`.
Multi-layer raster objects are rejected with an error message. The only
exception is a three- or four-band raster, which is assumed to represent
red, green, blue and alpha channels, respectively. In this case,
processing will continue but coloring arguments are ignored as
unnecessary.  
  
Prior to tiling, a geographically-projected raster layer is reprojected
to EPSG:4326 only if it has some other projection. The only reprojection
argument available through `...` is `method`, which can be `"bilinear"`
(default) or`"ngb"`. If complete control over reprojection is required,
this should be done prior to passing the rasterized file to the `tile`
function. Then no reprojection is performed by `tile()`. When `file`
consists of RGB or RGBA bands, `method` is ignored if provided and
reprojection uses nearest neighbor.  
  
It is recommended to avoid using a projected 4-band RGBA raster file.
However, the alpha channel appears to be ignored anyway. `gdal2tiles`
gives an internal warning. Instead, create your RGBA raster file in
unprojected form and it should pass through to `gdal2tiles` without any
issues. Three-band RGB raster files are unaffected by reprojection.

### Tiles and Leaflet

`gdal2tiles` generates TMS tiles. If expecting XYZ, for example when
using with Leaflet, you can change the end of the URL to your hosted
tiles from `{z}/{x}/{y}.png` to `{z}/{x}/{-y}.png`.  
  
This function is supported by two different versions of `gdal2tiles`.
There is the standard version, which generates geospatial tiles in TMS
format. The other version of
`gdal2tiles} handles basic image files like a matrix of rows and columns, using a simple Cartesian coordinate system based on pixel dimensions of the image file. See the Leaflet JS library and `leaflet\`
package documentation for working with custom tiles in Leaflet.

## See also

[`view_tiles()`](https://docs.ropensci.org/tiler/reference/view_tiles.md),
[`tile_viewer()`](https://docs.ropensci.org/tiler/reference/tile_viewer.md)

## Examples

``` r
# non-geographic/simple CRS
x <- system.file("maps/map.png", package = "tiler")
tiles <- file.path(tempdir(), "tiles")
tile(x, tiles, "2-3")
#> Creating tiles. Please wait...
#> Creating tile viewer...
#> Complete.

if (FALSE) { # \dontrun{
# unprojected map
x <- system.file("maps/map_wgs84.tif", package = "tiler")
tile(x, tiles, 0)

# projected map
x <- system.file("maps/map_albers.tif", package = "tiler")
tile(x, tiles, 0)
} # }
```
