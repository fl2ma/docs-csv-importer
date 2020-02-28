# Docker

There are a few ways to use the CSV importer with Docker.

There are some *gotchas* when it comes to Docker and IP addresses, so please check out the instructions at the bottom of the page.

## Run as a web server

This is the easiest way to run the CSV importer. Simply use the following run command to launch the CSV importer.

```bash
docker run \
--rm \
-e FIREFLY_III_ACCESS_TOKEN= \
-e FIREFLY_III_URI= \
-p 8081:80 \
jc5x/csv-importer:develop

```

By running this script, you will start a web server on port 8081 that will allow you to import data. You should append the command with your Personal Access Token and Firefly III URL.

Here are some tricks to make it easier for yourself:

### Use pre-defined script

Use [run-hosted.sh](https://github.com/firefly-iii/csv-importer-docker/blob/master/run-hosted.sh) to make it easier to manage your Personal Access Token.

### Append "-d"

Change `docker run` to `docker run -d` to make sure the image runs in the background.

## Run inline

This command will launch the CSV importer which will then try to import whatever it finds in the current directory. This is fully automated. It works by mounting the current directory to `/import` and importing all CSV files found inside of it.

```bash
docker run \
--rm \
-v $PWD:/import \
-e FIREFLY_III_ACCESS_TOKEN= \
-e FIREFLY_III_URI= \
-e WEB_SERVER=false \
jc5x/csv-importer:develop
```

In order for this to work, each CSV file must be accompanied by a JSON configuration file. So `import-file.csv` must be accompanied by `import-file.json`.

This can also be made easier for yourself:

### Use pre-defined script

Use [run-inline.sh](https://github.com/firefly-iii/csv-importer-docker/blob/master/run-inline.sh) to make it easier to manage your Personal Access Token. You can also customize the directory that the script will use as well.

## Docker and IP addresses

If you run the CSV Importer, the IP address you need to contact Firefly III isn't 127.0.0.1, even when you run Firefly III on the same machine. Docker uses an internal network. There's a good chance your Firefly III installation has an IP address that starts with 172.17. You can find out the internal IP address of Firefly III using this command:

```bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' CONTAINER
```

Instead of `CONTAINER`, use the container ID of your Firefly III installation.

If your Firefly III installation is online, you can also use the web address. If you want to, you can generate a Personal Access Token on the [demo site](https://demo.firefly-iii.org/) and use the demo site as a test. Keep in mind that the demo site is public to everybody so everyone will see what you import.

### Example scripts for a full setup

```bash
# run a basic MariaDB instance.
docker run --name mariadb -e MYSQL_ROOT_PASSWORD=super_secret -e MYSQL_DATABASE=fireflyiii -d mariadb:latest

# get the IP of the MariaDB instance:
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' mariadb

# run a basic Firefly III instance (update the IP of the database if necessary)
docker run -d \
--name fireflyiii \
-v firefly_iii_export:/var/www/firefly-iii/storage/export \
-v firefly_iii_upload:/var/www/firefly-iii/storage/upload \
-p 80:80 \
-e APP_KEY=123456789012345678901234567890aa \
-e DB_HOST=172.17.0.2 \
-e DB_CONNECTION=mysql \
-e DB_PORT=3306 \
-e DB_DATABASE=fireflyiii \
-e DB_USERNAME=root \
-e DB_PASSWORD=super_secret \
jc5x/firefly-iii:latest

# Chase the log files to see when Firefly III is ready to go:
docker logs -f $(docker container ls -a -f name=fireflyiii --format="{{.ID}}")

# get Firefly III IP address:
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' $(docker container ls -a -f name=fireflyiii --format="{{.ID}}")

# Adapt run-inline.sh and run it using your personal access token
# You can find it here: https://github.com/firefly-iii/csv-importer-docker/blob/master/run-inline.sh

./run-inline.sh

```
