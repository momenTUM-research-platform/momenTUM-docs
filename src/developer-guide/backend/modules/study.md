# study

The definitive reference implementation of the study format can be found in study.rs.

To illustrate the type safety, consider the following code snippet in Rust:

 ```Rust
 #[post("/api/v1/study", data = "<potential_study>")]
 pub async fn create_study(
     user: User,
     db: Connection<DB>,
     potential_study: Result<Json<Study>, json::Error<'_>>
 ) -> Result<String> {
     let mut study = potential_study.map_err(|e| error::Error::StudyParsing(e.to_string()))?;
     study._id = Some(ObjectId::new());
     study.timestamp = Some(DateTime::now().timestamp_millis());
     let result = db
         .database(ACTIVE_DB)
         .collection::<Study>("studies")
         .insert_one(&*study, None)
         .await?;

     Ok(result.inserted_id.to_string())
 }
 ```

In this code, we define an endpoint route using the `#[post]` attribute, indicating that a study may be included in the request body.

The `create_study` function serves as the handler for the route, accepting three arguments. Firstly, a user object is automatically parsed from the request and validated by a Request Guard implemented in `users.rs`. This ensures that only authenticated users can access this endpoint.

The second argument is a database connection, which is also automatically injected by a Request Guard. Rocket provides a built-in guard that connects to a MongoDB database. The connection is configured as follows:

 ``` Rust
 #[derive(Database)]
 #[database("mongodb")]
 pub struct DB(mongodb::Client);
 ```

 To access the database in development, you can use MongoDB compass, which is a GUI for MongoDB.
 Once installed, you can connect to the database by using the following connection string: url = "mongodb://tuspl22-redcap-db.srv.mwn.de/momenTUM?retryWrites=true&w=majority".
 Make sure to be connected to the TUM VPN.

 Lastly, we have the study itself, which is parsed from the request body and validated by Rocket.
 In this case, we want the guard to return us a `Result`, which is a fundamental type in Rust and can either be `Ok` or `Err`.

 If the study is valid, the Result will be `Ok` and contain the parsed study.
 If the study is invalid, the Result will be `Err` and contain an error message about what exactly is wrong with the study.

 In our case, we want to return an error message to the user, if the study is invalid, so we map the `Err` case to our own error type.
 Then, we return it by using the `?` operator, which is a very convenient way to propagate errors in Rust.

 Now we can be sure that we have a valid study, so we can insert it into the database.

 This operation also returns a `Result`, which we can use to return an error message to the user, if the database operation fails.

 If everything went well, we return the ID of the newly created study to the user.
