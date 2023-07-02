# users

The `User` struct represents an authenticated user with email and password hash. It implements the `FromRequest` trait, allowing it to be used as a request guard in Rocket applications.

## Usage

To use the `User` struct as a request guard, you need to follow these steps:

1. Extract the Authorization header from the request, which should contain a base64 encoded string of the email and password.
2. Compare the password hash in the database with the hash of the password provided in the Authorization header.
3. If the password hashes match, return the `User` struct containing the email and password hash.
4. If the authentication fails at any step, return an appropriate error response.

## Implementation Details

### Dependencies

The following external crates are used in the implementation:

- `base64` for base64 encoding and decoding.
- `mongodb` for interacting with the MongoDB database.
- `rocket` for the Rocket web framework.
- `rocket_db_pools` for managing database connections.
- `serde` for serialization and deserialization of the `User` struct.
- `sha2` for hashing the password.

Make sure to include these dependencies in your project's `Cargo.toml` file.

### User Struct

The `User` struct represents an authenticated user and has the following fields:

- `email`: A string representing the user's email.
- `password_hash`: A string representing the hash of the user's password.

### FromRequest Implementation

The `User` struct implements the `FromRequest` trait, allowing it to be used as a request guard. The `from_request` function is called during request processing and performs the following steps:

1. Retrieves the Authorization header from the request.
2. Validates the format of the Authorization header.
3. Decodes the base64 encoded string in the Authorization header.
4. Extracts the email and password from the decoded string.
5. Hashes the password using a salt value and the SHA256 algorithm.
6. Searches for the user in the database using the email and password hash.
7. Returns the user if authentication is successful or an appropriate error response otherwise.

### Conversion to Document

The `From<User> for Option<Document>` implementation allows converting a `User` struct into a MongoDB `Document` for database operations. It creates a document with the `email` and `password_hash` fields populated.

## Example

```rust
use rocket::Request;

#[rocket::get("/private")]
async fn private_route(user: User) -> String {
    format!("Welcome, {}!", user.email)
}

#[rocket::launch]
fn rocket() -> _ {
    rocket::build()
        .mount("/", routes![private_route])
}
```

In the example above, the `private_route` handler is guarded by the `User` request guard. Only authenticated users will be able to access the route. The `User` struct can be accessed in the handler function, and the email can be used to personalize the response.

## Notes

- The `VERY_STRONG_SALT` value used to salt the password hashing should be replaced with a secure salt value in a real-world application.
- The database connection configuration and setup are not shown in this code snippet. Make sure to establish a valid database connection before using the `User` request guard.