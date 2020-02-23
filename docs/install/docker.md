# Docker

There are two ways to use the CSV importer with Docker.

## Run as a web server

This is the easiest way to run the CSV importer. Simply use the following run command to launch the CSV importer.

```
docker run \
--rm \
-e FIREFLY_III_ACCESS_TOKEN= \
-e FIREFLY_III_URI= \
-p 8081:80 \
-e WEB_SERVER=false \
jc5x/csv-importer:develop

```

By running this script, you will start a web server on port 8081 that will allow you to import data. You should append the command with your Personal Access Token and Firefly III URL.

Here are some tricks to make it easier for yourself:

### Use pre-defined script

Use [run-hosted.sh](https://github.com/firefly-iii/csv-importer-docker/blob/master/run-hosted.sh) to make it easier to manage your Personal Access Token.

### Append "-d"

Change `docker run` to `docker run -d` to make sure the image runs in the background.

## Run inline

This command will launch the CSV importer which will then try to import whatever it finds in the current directory. This is fully automated. It works by mounting a directory of your choice to `/import` and importing all CSV files found inside of it.	

```
docker run \
--rm \
-v $PWD:/import \
-e FIREFLY_III_ACCESS_TOKEN= \
-e FIREFLY_III_URI= \
-e WEB_SERVER=false \
jc5x/csv-importer:develop
```

This can also be made easier for yourself:

### Use pre-defined script

Use [run-inline.sh](https://github.com/firefly-iii/csv-importer-docker/blob/master/run-inline.sh) to make it easier to manage your Personal Access Token. You can also customize the directory that the script will use as well.
