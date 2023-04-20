# Overview

This is a backend documentation for the momenTUM project. The backend's code can be found in the [JSON-maker repository](https://github.com/TUMChronobiology/momenTUM-json-maker).  

This documentation explains the `api` and it's interactions with the `frontend: Designer` for a custom creation of a `Study` and the `Mobile App: momenTUM` for data gathering and storing. 

From the researcher peprspective, the `Designer` is a website used for designing and customizing a study. This is the frontend section. The `api` have several routes that help store the created `Study` and other metadata in a database. During which, it also retrives a `URL` for the location of the study in the database. 
<!-- 
In the creating of a study, the researcher can choose where to store the responses collected from the mobile app. The researcher has the option to create a `REDCap` project for it or can have an external storage space. If they have an external storage space, they would need to set the variable of `post-url` of the study to that location when they are creating the study via the `Designer`.  -->

The `Designer` is a JSON maker for a researchers study. It is a web application that allows users to create surveys and export them as JSON files and return a link for their location and easy access. It also generated a QR-code for the links. The JSON files can then be imported into the MomenTUM app via a link, QR-code or study id.


From the researchers that use the REDCap configuration already set up for storing the records, the `MomenTUM` mobile app sends the collected data by calling an endpoint from the `api`. 

There are two databases used for storage in this project. The `MongoDB` and `REDCap`. The `api` stores a metadata of responses in the `MongoDB` and the actual reponse in the `REDCap`. The metadata of every response is stored in the `Mongodb`, depending on the fact that the study already exists there. Thus, the responses collected by the `Mobile App: momenTUM` is used for creating a metadata that is stored in the `MongoDB` and/or `REDCap` depending on the researchers' preference.



