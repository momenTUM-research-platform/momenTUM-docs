# API

The Backend implements a set of **HTTP Routes**.
They serve as API endpoints that can be used by other applications to interact with the backend.
The following routes are defined:

Certainly! Here are the examples for each route without explicitly mentioning the "Route" and HTTP method:

1. **GET /api/docs/<path..>**

   - Example:
     ```
     GET /api/docs/index.html
     ```
   - Description: Retrieves the documentation file named `index.html` from the `/docs/` directory.

2. **GET /api/v1/status**

   - Example:
     ```
     GET /api/v1/status
     ```
   - Description: Retrieves the status of the V1 API.

3. **GET /api/v1/studies/<study_id>**

   - Example:
     ```
     GET /api/v1/studies/12345
     ```
   - Description: Retrieves the study with the ID `12345`.

4. **POST /api/v1/studies/<study_id>**

   - Example:
     ```
     GET /api/v1/studies/12345
     ```
   - Description: Updates the study with the ID `12345`.

5. **GET /api/v1/studies**

   - Example:
     ```
     GET /api/v1/studies
     ```
   - Description: Retrieves a list of all studies.

6. **GET /api/v1/studies/all/<study_id>**

   - Example:
     ```
     GET /api/v1/studies/all/12345
     ```
   - Description: Retrieves all studies associated with the study ID `12345`.

7. **GET /api/v1/response/<study_id>/<user_id>**

   - Example:
     ```
     GET /api/v1/response/12345/67890
     ```
   - Description: Retrieves the response for the study with ID `12345` and the user with ID `67890`.

8. **POST /api/v1/study**

   - Example:
     ```
     POST /api/v1/study
     Body: {
         "data": { /* Potential study data */ 
        }
     }
     ```
   - Description: Creates a new study with the provided data.

9. **POST /api/v1/response**

   - Example:
     ```
     POST /api/v1/response
     Body: {
         "data": { /* Submission data */ 
        }
     }
     ```
   - Description: Submits a response to a study.

10. **POST /api/v1/log**

    - Example:
      ```
      POST /api/v1/log
      Body: {
            "data": { /* Submission data */ }
      }
      ```
    - Description: Saves a submission as a log.

11. **POST /api/v1/redcap/<username>**

    - Example:
      ```
      POST /api/v1/redcap/johndoe
      Body: {
          "data": { /* Study data */ 
        }
      }
      ```
    - Description: Creates a new REDCap project, imports metadata and user information, and associates it with the specified username.

12. **POST /api/v1/user**
    - Example:
      ```
      POST /api/v1/user
      Body: {
          "data": { /* New user data */ 
        }
      }
      ```
    - Description: Adds a new user to the system.

Please note that the examples provided assume a base URL of `https://make.momentumresearch.eu/` and may need to be modified based on your specific implementation.
