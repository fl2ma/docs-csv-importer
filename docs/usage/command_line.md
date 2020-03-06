# Uploading files

On this page you'll find instructions on how to use the import tool's command line.

This page assumes you're self-hosting the CSV import tool, although these commands also work when using Docker.

## Importing a single file.

Use the following command to import a single file:

```bash
php artisan csv:import file.csv file.json
```

Replace `file.csv` with the path to your CSV file, and the JSON file should point (obviously) to your JSON file.

## Importing a directory

Use the following command to import a full directory:

```bash
php artisan csv:auto-import /path/to/your/files
```

In this directory, each file that must be imported is expected to have the extension `csv`, and the accompanying configuration file must have the same file name, except for the extension: that has to be `json`. So `my-file.csv` MUST be accompanied by `my-file.json` for this command to work.
