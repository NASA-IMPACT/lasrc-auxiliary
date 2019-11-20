## lasrc-auxiliary
The `lasrc` processing code requires [auxiliary data](https://github.com/developmentseed/espa-surface-reflectance/tree/master/lasrc#downloads) to run.
This `lasrc` auxiliary data also requires [periodic updates](https://github.com/developmentseed/espa-surface-reflectance/tree/master/lasrc#auxiliary-data-updates) to run.

To build the image contaning the scripts for downloading the base data on a shared EFS mount point run
```shell
$ docker build --tag lasrc_aux_download ./download_aux
```
You can then tag this `lasrc_aux_download` image as `350996086543.dkr.ecr.us-west-2.amazonaws.com/lasrc_aux_download` and push it to ECR.

To build the image contaning the scripts for updating this data on a shared EFS mount point run

```shell
$ docker build --tag lasrc_aux_update ./update_aux
```
You can then tag this `lasrc_aux_update` image as `350996086543.dkr.ecr.us-west-2.amazonaws.com/lasrc_aux_update` and push it to ECR.


