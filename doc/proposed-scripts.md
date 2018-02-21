# Proposed scripts to process OSM Changes

`define_aoi_for_diffs.py <osm_pbf_url> <cmf_root>`

* Creates a directory with the below structure beneath the Crash Move Folder:

<pre>
.
`-- GIS
    `-- 1_Original_Data
        `-- 101_osm
            `-- region
                |-- baseline
                |-- previous
                |-- latest
                `-- updates
</pre>

Where `region` is derived from the downloaded OSM PBF file

* Downloads the OSM PBF file from the given URL to the `baseline` directory
* Creates a cron job under `/etc/cron.d` to run the `generate_diffs_for_aoi.py` script

`generate_diffs_for_aoi.py <osm_pbf_url> <cmf_root>`

* Downloads the latest OSM PBF file from the given URL to the `latest` directory
* Creates an incremental difference file by comparing the `latest` and `previous` PBF files
  and stores this in the `updates` directory with an appropriate name and
  timestamp.
* Creates a cumulative difference file by comparing the `latest` and `baseline` PBF files
  and stores this in the `updates` directory with an appropriate name and
  timestamp.
