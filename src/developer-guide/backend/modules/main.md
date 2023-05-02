# main

This is a Rust program that defines a web API using the Rocket framework. The API provides endpoints for accessing studies and submitting responses.

The program defines a MongoDB database and a DB struct that represents a connection to this database. The `#[database("mongodb")]` attribute macro specifies that the DB struct should use the MongoDB database.

The `ACTIVE_DB` is set to the database if the `debug_assertions` is true or false.

The `Key` struct represents an API key used to access a study. The Study struct represents a study stored in the database.

The program defines the following endpoints:

- `docs_assets`: serves static files from the /docs/ directory.
- `status`: returns a static string indicating that the API is live.
- `fetch_study`: retrieves a study from the database by ID or by study_id property. Returns the study as JSON or an error if the study is not found.
- `get_study_by_post`: legacy support for retrieving studies using POST requests.
all_studies: retrieves all studies from the database. Returns the studies as JSON.
- `all_studies_of_study_id`: retrieves all studies with a given study_id property from the database. Returns the studies as JSON.
- `create_study`: inserts a new study into the database. Expects a Study object in the request body. Returns the ID of the newly created study.
- `save_response`: saves a response to a study in the database. Expects a Response object in the request body.
- `save_log`: saves a log message to the database. Expects a Log object in the request body.
- `create_redcap_project`: creates a new REDCap project and saves the API key to the database. Expects a Study object in the request body and a username parameter in the URL.

