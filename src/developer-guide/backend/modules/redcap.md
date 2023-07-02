# redcap


 The API also contains an endpoint for importing studies into REDCap.

 ``` Rust

 #[post("/api/v1/redcap/<username>", data = "<study>")]
 pub async fn create_redcap_project(
     db: Connection<DB>,
     study: Json<Study>,
     username: &str,
 ) -> Result<&'static str> {
     let study = study.0;
     let api_key = redcap::create_project(&study).await?;
     ... // Saving the API key to the database
     redcap::import_metadata(&study, api_key.clone()).await?;
     redcap::enable_repeating_instruments(&study, api_key.clone()).await?;
     redcap::import_user(username, api_key.clone()).await?;

     Ok("...")
 }
 ```

 As you can see, this endpoint receives a database connection and a study guaranteed to be valid, as well a a redcap username that will be the owner of the new project.

 There are five main steps:

 1. Create a new project in REDCap with a SUPER_API_KEY, which is stored in a .env file
 2. Save the returned project API key in the database
 3. Import the metadata of the study into the new project. This includes mapping our modules to RedCap instruments.
 4. Enable repeating instruments, so that we can add multiple instances of the same instrument to a single record (Often modules are done once per day).
 5. Then we add the specified user as a project admin, so that they can access the project.
