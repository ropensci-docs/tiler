# View map tiles with Leaflet

View map tiles in the browser using leaflet.

## Usage

``` r
view_tiles(tiles)
```

## Arguments

- tiles:

  character, directory where tiles are stored.

## Value

nothing is returned, but the default browser is launched.

## Details

This function opens `preview.html` in a web browser. This file displays
map tiles in a Leaflet widget. The file is created when
[`tile()`](https://docs.ropensci.org/tiler/reference/tile.md) is called
to generate the map tiles, unless `viewer = FALSE`. Alternatively, it is
created (or re-created) subsequent to tile creation using
[`tile_viewer()`](https://docs.ropensci.org/tiler/reference/tile_viewer.md).

## See also

[`tile_viewer()`](https://docs.ropensci.org/tiler/reference/tile_viewer.md),
[`tile()`](https://docs.ropensci.org/tiler/reference/tile.md)

## Examples

``` r
# launches browser; requires an existing tile set
if (FALSE) view_tiles(file.path(tempdir(), "tiles")) # \dontrun{}
```
