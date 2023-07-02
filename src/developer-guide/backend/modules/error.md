# error

The `error.rs` file contains the implementation of an error handling mechanism for a Rocket web framework application. It defines an `Error` enum and provides a `Responder` implementation for it.

## Dependencies

This file depends on the following external crates:

- `rocket` (version `0.5.0-rc.2`)
- `thiserror` (version `1.0`)

Make sure to include these dependencies in your project's `Cargo.toml` file.

## Error Enum

The `Error` enum represents various error cases that can occur during the execution of the application. It includes the following error variants:

- `StudyNotFound`: Indicates that a study was not found.
- `AuthMalformed`: Indicates that the authorization header is malformed, and provides an additional error message.
- `AuthNoEmail`: Indicates that no email was provided for authentication.
- `AuthNoPassword`: Indicates that no password was provided for authentication.
- `AuthIncorrect`: Indicates that the provided email or password is incorrect.
- `NotAdmin`: Indicates that the user is not an admin.
- `NoCorrespondingAPIKey`: Indicates that no corresponding API key for a REDCap project was found.
- `RedcapAuthenication`: Indicates a REDCap authentication error.
- `Redcap`: Represents a generic REDCap error, along with an associated error message.
- `DB`: Represents a database error, wrapped by the `mongodb::error::Error` type.
- `Request`: Represents a request error, wrapped by the `reqwest::Error` type.
- `ResponseDeserialization`: Represents a response deserialization error, wrapped by the `serde_json::Error` type.
- `StudyParsing`: Represents a study parsing error, along with an associated error message.
- `RecordNotFoundInDB`: Indicates that a record was not found in the database.
- `InvalidResponseData`: Indicates that the response data is invalid.

## Responder Implementation

The `Responder` implementation for the `Error` enum allows these error types to be converted into appropriate HTTP responses. The `respond_to` method is implemented for the `Error` type, taking a Rocket `Request` as an argument.

Inside the `respond_to` method, the appropriate response is selected based on the error variant using a `match` statement. Each error variant corresponds to a specific HTTP status code and response message.

The selected response is then returned using the `respond_to` method provided by the `response` module of the Rocket crate.

Note that some error variants use the `Custom` response type to provide a custom status code and message.

## Example Usage

```rust
use rocket::Request;

// Some function that returns a String, either Error or something else

#[post("/add", data = "<something>")]
pub async fn add_something(
    something: Json<Something>
) -> Result<&'static str> {
    // ...

    if is_admin_user {
        // ...
        Ok("Inserted new Something")
    } else {
        Err(Error::NotAdmin)
    }
}

// Function that returns an error
fn some_function() -> Result<()> {
    // ...
    Err(Error::NotAdmin)
}

```

In the example above, the `some_function` can return an `Error` instance, which will be handled by the `Responder` implementation in this file. 

The `add_something` function is a Rocket route handler that accepts JSON data and returns a `Result` with a specific error type `Error`. If the user is not an admin, it returns an Err with the `NotAdmin` error variant.