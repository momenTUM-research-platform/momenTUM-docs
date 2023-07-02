# main

This documentation provides an overview of the `main.rs` file. It explains what the file generally includes, its dependencies, usages, defined types, and additional notes.

## General Contents

The `main.rs` file contains the main entry point of the application. It serves as the starting point for running the program. It includes various dependencies, defines API routes, and provides functions for handling requests and interacting with a database.

## Dependencies

The file has the following dependencies:

- `rocket`: A web framework for building web applications in Rust.
- `mongodb`: A Rust driver for MongoDB, a NoSQL database.
- `redcap`: A module/library for working with RedCap, an electronic data capture tool.
- `rocket_db_pools`: A Rocket fairing for managing database connections.

## Usages

The file is used to define and configure the Rocket web application. It sets up API routes and handlers, connects to the database, and provides functions for handling requests and interacting with data.

## Defined Types

The file defines the following types:

- `DB`: A struct representing the database connection using the connection string specified in Rocket.toml.
- `Result<T>`: A type alias representing a `std::result::Result` with an `Error` as the error type.
- `PotentialStudy`: A type alias representing a potential study in the form of `Result<Json<Study>>`.
- `Key`: A struct representing a study ID and API key.
- `CORS`: A Rocket fairing that adds CORS headers to responses.

## Additional Notes

- The file includes various modules (`error`, `redcap`, `study`, `users`) that contain additional functionality and definitions.
- The `ACTIVE_DB` constant is set based on whether the application is running in debug mode or not.
- Several API routes are defined, such as `status`, `fetch_study`, `save_response`, `create_redcap_project`, and others.
- The `main` function initializes the Rocket application, sets up necessary configurations, attaches fairings, and mounts routes.


## Some specific functions and associated modules

### `fetch_study` Function
```rust
#[get("/api/v1/studies/<study_id>")]
pub async fn fetch_study(db: Connection<DB>, mut study_id: String) -> PotentialStudy {
    // ...
}
```
- This function is an API route handler for fetching a study by its ID.
- It takes a database connection (`db`) and a study ID as input.
- The function uses the `Connection<DB>` type to access the database and perform operations.
- It retrieves the study from the database based on the provided study ID.
- The retrieved study is returned as a `Json<Study>` wrapped in a `Result` (as `PotentialStudy`).

### `save_response` Function
```rust
#[post("/api/v1/response", data = "<submission>")]
pub async fn save_response(submission: Form<Response>, db: Connection<DB>) -> Result<()> {
    // ...
}
```
- This function is an API route handler for saving a response.
- It takes a `Form<Response>` and a database connection (`db`) as input.
- The `Form<Response>` represents the data contained in the request body, which is deserialized into a `Response` struct.
- The function uses the `Connection<DB>` type to access the database and perform operations.
- It imports the response data into the database by calling the `import_response` function from the `redcap` module.

### `create_redcap_project` Function
```rust
#[post("/api/v1/redcap/<username>", data = "<study>")]
pub async fn create_redcap_project(
    db: Connection<DB>,
    study: Json<Study>,
    username: &str,
) -> Result<&'static str> {
    // ...
}
```
- This function is an API route handler for creating a RedCap project.
- It takes a database connection (`db`), a `Json<Study>` containing the study data, and a `username` as input.
- The `Json<Study>` represents the study data provided in the request body, which is deserialized into a `Study` struct.
- The function uses the `Connection<DB>` type to access the database and perform operations.
- It creates a RedCap project based on the study data by calling functions from the `redcap` module.
- The created project's API key is stored in the database, and various RedCap configurations are performed.

### Associated Modules
- The `error`, `redcap`, `study`, and `users` modules are included in the `main.rs` file.
- These modules provide additional functionality and definitions used by the API route handlers and other functions.
- You can explore these modules by referring to their respective implementation files (`error.rs`, `redcap.rs`, `study.rs`, `users.rs`).

Please note that the code snippets provided are only partial and may not include the complete implementation of the functions. For a comprehensive understanding of the implementation, you should refer to the complete source code of the associated modules and functions within the `main.rs` file.