# Create an HTML tile preview

Create an HTML file that displays a tile preview using Leaflet.

## Usage

``` r
tile_viewer(tiles, zoom, width = NULL, height = NULL, georef = TRUE, ...)
```

## Arguments

- tiles:

  character, directory where tiles are stored.

- zoom:

  character, zoom levels full range. Example format: `"3-7"`.

- width:

  `NULL` (default) for geospatial map tiles. The original image width in
  pixels for non-geographic, simple CRS tiles.

- height:

  `NULL` (default) for geospatial map tiles. The original image height
  in pixels for non-geographic, simple CRS tiles.

- georef:

  logical, for non-geographic tiles only. If `viewer = TRUE`, then the
  Leaflet widget in `preview.html` will add map markers with coordinate
  labels on mouse click to assist with georeferencing of non-geographic
  tiles.

- ...:

  additional optional arguments include `lng` and `lat` for setting the
  view longitude and latitude. These three arguments only apply to
  geographic tiles. Viewer centering is `(0, 0)` by default.

## Value

nothing is returned, but a file is written to disk.

## Details

This function creates a file `preview.html` adjacent to the `tiles` base
directory. When loaded in the browser, this file displays map tiles from
the adjacent folder. For example, if tiles are stored in
`project/tiles`, this function creates `project/preview.html`.

By default,
[`tile()`](https://docs.ropensci.org/tiler/reference/tile.md) creates
this file. The only reasons to call `tile_viewer()` directly after
producing map tiles are: (1) if `viewer = FALSE` was set in the call to
[`tile()`](https://docs.ropensci.org/tiler/reference/tile.md), (2) if
[`tile()`](https://docs.ropensci.org/tiler/reference/tile.md) was called
multiple times, e.g., for different batches of zoom levels, and thus the
most recent call did not use the full zoom range, or (3) `preview.html`
was deleted for some other reason.

If calling this function directly, ensure that the min and max zoom, and
original image pixel dimensions if applicable, match the generated
tiles. These arguments are passed to
`tile_viewer} automatically when called within `tile()`, based on the source file provided to `tile()\`.

## See also

[`view_tiles()`](https://docs.ropensci.org/tiler/reference/view_tiles.md),
[`tile()`](https://docs.ropensci.org/tiler/reference/tile.md)

## Examples

``` r
tile_viewer(file.path(tempdir(), "tiles"), "3-7") # requires existing tiles
```
