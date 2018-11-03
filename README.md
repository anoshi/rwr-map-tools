# rwr-map-tools

bash scripts and tools for managing levels created for [Running With Rifles](http://www.runningwithrifles.com)

## Usage
`im7_process_all.sh [--alpha alpha_layers] [--terrain terrain_layers] [--fx fx_layers]`

* Layers must be specified in order from lowest to highest
* If no arguments are passed, the script will prompt for input
  * This can save some effort on the command line in cases where the *alpha* and *terrain* layers are similarly named and ordered, for example

## Example
In the following example:
1. The user has [ImageMagick](https://www.imagemagick.org) version 7 installed and configured appropriately
1. This repository has been cloned into the user's home folder as *rwr-map-tools*
1. The user's current working directory contains the map files to be processed (e.g. *Resources/media/packages/<mod_name>/maps/<map_name>*)
1. The user has run the Running With Rifles export tool after altering and saving the *objects.svg* file in [Inkscape](https://www.inkscape.org) (v0.92 or above)
1. Shorthand flags (*-a*, *-t*, *-f*) are used to save some keystrokes

`~/rwr-map-tools/im7_process_all.sh -a sand grass asphalt road -t rocky_mountain grass sand road -f none alpha_dirtroad blood none_a`

## Output
The following block shows the output of the script, including some built-in sanity and best-effort checks when arguments are not passed or insufficient

`~/rwr-map-tools/im7_process_all.sh -a grass sand asphalt road -f alpha_dirt none none_a`
```
1) Process splat files: extract alpha channel, convert to 8-bit greyscale, and apply some gaussian blur

DONE: _rwr_alpha_grass.png
DONE: _rwr_alpha_sand.png
DONE: _rwr_alpha_asphalt.png
DONE: _rwr_alpha_road.png

2) One-pass terrain optimisation: merge generated terrain splat files into one (max: 4)

Use the same layer names and order for this task? grass sand asphalt road [YES/no]? 
Building terrain5_combined_alpha.png from terrain5_alpha_grass.png, terrain5_alpha_sand.png, terrain5_alpha_asphalt.png, and terrain5_alpha_road.png

TERRAIN: DONE

3) Combine effects layers

Fewer than four effect files found. Adding effect_none.png at start of list

Processing effects layers: effect_none.png effect_alpha_dirt.png effect_none.png effect_none_a.png

EFFECTS: DONE

4) Create heightmap from to 513x513 pixels, 8-bit greyscale
5) Convert map_view to 512x512, output initial map.png
6) Prepare map view
 i] Convert heightmap to 8-bit greyscale
 ii] isoline
 iii] water
 iv] blur woods
7) Combine map views
 i] isolines and water
 ii] decoration
 iii] woods
 iv] asphalt
 v] roads
 vi] bases
 vii] dirt roads
No dirt roads. Skipping
 vii] objects

map.png has been created

Finished!

```
