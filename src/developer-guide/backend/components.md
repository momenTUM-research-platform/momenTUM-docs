# Components

## Routes
These are `Routes` that the backend provi. They define the endpoints that a researcher or a participant can use to interact with the backend and the website. The following routes are defined:

`GET`
- `/api/docs/<path..>`: This route is used to retrieve the documentation for the API. The <path..> parameter is used to specify the path to the documentation file.
- `/api/v1/status`: This route is used to retrieve the status of the API.
- `/api/v1/studies/<study_id>`: This route is used to retrieve a specific study by its ID.
- `/api/v1/studies`: This route is used to retrieve a list of all studies.
- `/api/v1/studies/all/<study_id>`: This route is used to retrieve all the data associated with a specific study.


`POST`
- `/api/v1/studies/<study_id>`: This route is used to update a specific study by its ID.
    ### Body
    ```
        {
           
        }
    ```
- `/api/v1/study`: This route is used to create a new study.
    ### Body
    ```
        {
            "data": <potential_study>
        }
    ```
- `/api/v1/response`: This route is used to submit a response to a study.
    ### Body
    ```
        {
            "data": <submission>
        }
    ```
- `/api/v1/log`: This route is used to log a submission.
    ### Body
    ```
        {
            "data": <submission>
        }
    ```
- `/api/v1/redcap/<username>`: This route is used to import a study from REDCap.
    ### Body
    ```
        {
            "data": <study>
        }
    ```
- `/api/v1/user`: This route is used to create a new user.
    ### Body
    ```
        {
            "data": <new_user>
        }
    ```
These routes define the different endpoints that a a researcher or a participant can use to interact with the API. 

The HTTP methods used for these routes are GET and POST. GET is used to retrieve data from the server, while POST is used to submit data to the server.

By using these routes, the different components of the web application can work together to provide a complete functionality. The routes define the different parts of the application that can be accessed by the a researcher or a participant, and the components work together to provide the desired functionality.