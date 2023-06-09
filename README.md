# Drupal Algolia Demo
Spinning a local drupal instance to test the Algolia Drupal module integration.

`localhost:8080`

## Instalation
### 1. Build and run the Containers via composer
Create a `.env` file. Use `example.env` as a reference.
```sh
docker-compose up
```
### 2. Run the install command
Installs a Drupal sample environment (demo_unami)including the Algolia module for Drupal `search_api_algolia`. it doesn't include any Algolia indices configurations.
```sh
docker-compose exec drupal /opt/drupal/sync_scripts/install.sh
```
### 3. Load the Algolia configuration (DEMO)
If you want to load the Algolia demo (config and db), run the following command. This script will load your secret API admin key to your Drupal instance.
```sh
docker-compose exec drupal /opt/drupal/sync_scripts/imports.sh
```
Your default username `admin` and `admin123` password.
## Executing Queues
You can manually trigger cron by running.
```sh
docker-compose exec drupal drush cron
```
## Exporting DB and Config Files (Updating DEMO)
This export command will generate a DB snapshot and export your configuration file. Use this process to securely remove your Algolia API key from both your DB and configuration files.

```sh
docker-compose exec drupal /opt/drupal/sync_scripts/export.sh
```

## Importing DB and current Config (Reload DEMO)
If you want to discard your current changes you can re-import the database snapshot and then re-import the config code changes from the `config_scripts/config` folder run:
```sh
docker-compose exec drupal /opt/drupal/sync_scripts/import.sh
```

## Indexing changes via Drush
To perform a full indexation via drush run:
```sh
docker-compose exec drupal drush search-api:index
```