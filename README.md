# osm-changesets

The **OSM Change Toolset** provides tools for acquiring OSM data, and enabling a
field team to update their copy to reflect the latest OSM data without the need
for them to download the whole OSM data file again.

### OSM Change Toolset

* Tool **0 - Get OSM files for country**. This tool simply enables the MapAction support base to download OSM data from the geofabrik server
   (as a master PBF file). The script called by this tool is for doing this is `0_get_OSM_files.py`.
   This doesn't really do anything that you can't do by downloading the file yourself with a web browser.

* Tool **1 - Create Difference File**. This tool is intended to be run by Support Base when a field team is deployed and they have limited internet bandwidth. It takes as input two OSM .PBF format files, one of which should be the OSM data that the field team deployed with and the other should be the latest version of the OSM data. The tool will create a file that represents only the difference between those two input files, which should hopefully be much smaller than either of the actual input files themselves and which can therefore be more easily transferred to the Field Team. The Python script called by this tool is `1_create_difference_SB.py`.

* Tool **2 - Append Difference File**. This is effectively the reverse of Tool 1 and is intended to be run by the Field Team. It will take the original OSM .PBF file from the start of the deployment, and the difference file provided by Support Base. It will output a new .PBF file that reflects all the changes and is therefore up-to-date. The python script called by this tool is `2_append_differnce_FT.py`.

### Under the hood

The tools rely on various non-ArcGIS tools which are installed in known locations on the MapAction laptops. You won't need to worry about these for running on the laptops, but for other uses you will need to know about them.

For the change toolset, you will need java installed and [Osmosis](http://wiki.openstreetmap.org/wiki/Osmosis#Latest_stable_version)

On **Windows** this should be placed at `C:\osmosis`.

On **\*nix** this can be anywhere, and either added to your `PATH` environment
variable or passed on the CLI with `-o`.
