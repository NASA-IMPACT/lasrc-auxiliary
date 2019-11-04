## lasrc-auxiliary
The `lasrc` portion of the  processing code requires [auxiliary data](https://github.com/developmentseed/espa-surface-reflectance/tree/master/lasrc#downloads) to run.  To build the image contaning the scripts for downloading this data to a shared EFS mount point run

```shell
$ docker build --tag lasrc_aux_download ./download_aux
```
You can then tag this `lasrc_aux_download` image as `552819999234.dkr.ecr.us-east-1.amazonaws.com/lasrc_aux_download` and push it to ECR.

The `lasrc` auxiliary data also requires [periodic updates](https://github.com/developmentseed/espa-surface-reflectance/tree/master/lasrc#auxiliary-data-updates). To run these updates as a task you must first obtain an app key with the instructions [here](https://ladsweb.modaps.eosdis.nasa.gov/tools-and-services/data-download-scripts/#appkeys).

Assuming you have a stack deployed following guide in
[hlslandsat](https://github.com/developmentseed/hlslandsat) but with a cloudformation output `LaSRCAuxDownloadTaskDefinitionArn` you can run:

```shell
./run_lasrc_aux_download_task.sh yourstackname
```

To build the image contaning the scripts for updating this data on a shared EFS mount point run

```shell
$ docker build --tag lasrc_aux_update ./update_aux
```
You can then tag this `lasrc_aux_update` image as `552819999234.dkr.ecr.us-east-1.amazonaws.com/lasrc_aux_update` and push it to ECR.

After building and tagging the images, follow the steps outlined [here]https://docs.aws.amazon.com/AmazonECR/latest/userguide/ECR_AWSCLI.html) to push them to ECR.

To run these tasks on the ECS cluster where the task defintions were deployed ...

Use the app key obtained above to set an environment variable with
```shell
$ export LAADS_TOKEN=yourappkey
```

Once you have set your `LAADS_TOKEN` to run the ECS task to download the daily updated auxiliary data run
```shell
$ ./run_lasrc_aux_update_task.sh yourstackname
```
This will start a task to download the Lasrc auxiliary data updates and fuse them with the exisiting auxiliary data on EFS.  Once your auxiliary data is up to date you can run Lasrc for your updated time period.
