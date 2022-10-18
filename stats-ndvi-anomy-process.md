#  DE Africa stats-ndvi-anomaly-process Argo workflow

## stats-ndvi-anomaly-process workflow
The workflow template for the stats-ndvi-anomaly-process workflow is contained in the https://github.com/digitalearthafrica/datakube-apps/tree/main/deployments/processing-data/argo-workflows/argo-workflow-templates/


## DE Africa ndvi-anomaly code
The code base on the ndvi-anomaly repo provides all the methods necessary for running the NDVI anomalies pipeline using AWS's Kubernetes platform. https://github.com/digitalearthafrica/ndvi-anomalies



# Running the stats-ndvi-anomaly-process Argo workflow 

### These workflows include several important parameters that can be modified to control the analysis:

   * The `image-tag` number is the version number of the docker image i.e. the number [here](https://github.com/digitalearthafrica/ndvi-anomalies/blob/main/docker/version.txt)

    * The `result-bucket` is the location where the output geotiffs will be stored. This is `deafrica-services` if running the full production run, `deafrica-data-staging-af` if testing in production workspace, and `deafrica-data-dev-af` if running in the dev environment.
    * The `product-name` is "ndvi_anomaly" 

    * The `product-cfg` is the _raw_ github https link to the plugin configuration yaml, i.e. this file [here](https://raw.githubusercontent.com/digitalearthafrica/ndvi-anomalies/main/production/ndvi_tools/config/ndvi_anomaly.yaml)

    * `product-version` is usually just `1-0-0`, unless re-running the product with an updated version.

    * `temporal-range` is the time range that gets passed to `odc-stats save tasks`; for the NDVI anomaly this 
    will _always_ take the format `<YYYY>-<MM>--P1M`, e.g. `2022-01-P1M` to run an anomaly for January 2022

    * `geojson-extent` defines a region of tiles to run. There are only two option: either "testing_extent" which covers 111 tiles covering a region from Ghana to Tunisia, use this extent if running a large scale test.  The other option is "africa_land_extent" which will run all tiles over the land mass of Africa (ocean tiles are excluded).

    * `parallel-processing` refers to the number of pods K8s will scale too. For testing, set this to `1` and a single machine will run - this makes it easy to inspect logs etc.  For the full scale production runs a good number is `480` (40 machines will run 480 tiles in parallel).

    * The other parameters (`input-products`, `queue`, `resolution` etc.) should mostly stay as their defaults.
    
    * Hit the `submit` button when you're happy with the inputs and the code will be deployed.
