# Options

Options for tiler package.

## Usage

``` r
tiler_options(...)
```

## Arguments

- ...:

  a list of options.

## Value

The function prints all set options if called with no arguments. When
setting options, nothing is returned.

## Details

On Windows systems, if the system paths for `python.exe` and
`OSGeo4W.bat` are not added to the system PATH variable, they must be
provided by the user after loading the package. It is recommended to add
these to the system path so they do not need to be specified for every R
session.

As long as you are using OSGeo4W, you can ignore the Python path
specification and do not even need to install it on your system
separately; OSGeo4W will use its own built-in version.

The recommended way to have GDAL available to Python in Windows is to
install [OSGeo4W](https://trac.osgeo.org/osgeo4w/). This is commonly
installed along with [QGIS](https://qgis.org/download/).

By default, `tiler_options()` is set on package load with
`osgeo4w = "OSGeo4W.bat"`. It is expected that the user has added the
path to this file to the system PATH variable in Windows. For example,
if it is installed to `C:/OSGeo4W64/OSGeo4W.bat`, add `C:/OSGeo4W64` to
your PATH. If you do want to specify the path in the R session using
`tiler_options()`, provide the full path including the filename. See the
example.

None of this applies to other systems. As long as the system
requirements, Python and GDAL, are installed, then
[`tile()`](https://docs.ropensci.org/tiler/reference/tile.md) should
generate tiles without getting or setting any `tiler_options()`.

## Examples

``` r
tiler_options()
#> $python
#>            python3 
#> "/usr/bin/python3" 
#> 
#> $osgeo4w
#> [1] ""
#> 
tiler_options(osgeo4w = "C:/OSGeo4W64/OSGeo4W.bat")
```
