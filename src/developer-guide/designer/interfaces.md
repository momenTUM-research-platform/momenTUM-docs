# Interfaces

The Designer shares an interface with each of the following:
- [Researcher](#researcher)
- [Backend](#backend)
- [Local Disk](#localdisk)

This documentation provides a guide on how to use the Designer application for a researcher and developer. Designer allows researchers to design and manage studies, upload them to a database, create REDCap projects, generate QR codes, collect responses and customize studies. The documentation also covers important information about the backend and local disk usage.

## Researcher

As a researcher, you have the following capabilities with the Designer application:

- Design a Study: You can create a study using the Designer application. Design your study according to your research requirements and specifications.

- Upload and Store Studies: After designing a study, you can upload it to the database for storage. The study will be saved securely in the database for future use.

- Create REDCap Projects: If you have a REDCap account, you can create a REDCap project for your study. This is an advised and suitable approach as REDCap allows you to collect and manage study responses effectively.

- Load Studies from Database: You can load any study from the database using its study ID. This allows you to retrieve and use previously designed studies for further modifications or analysis.

- Generate QR Codes: Designer provides the functionality to generate QR codes for the studies you upload. These QR codes can be used for quick access to the study or sharing it with participants.

- Customize Studies: Designer allows you to customize studies as per your requirements. You have the flexibility to make changes, add or remove components, and tailor the study to fit your research needs.

## Backend

The Designer backend is responsible for managing the storage and retrieval of studies. Here are some important details regarding the backend:

- Study Storage: When you upload a study, it is securely saved in the Designer database. However, if you have a REDCap account, it is advisable to create a REDCap project for your study. This allows you to collect participant responses directly in REDCap, streamlining your data management process.

As a researcher, creating a REDCap account is essential if you wish to use the study designer in Designer. Then, in the actions tab, you have the option of creating a project in your REDCap account, where you can seamlessly integrate your studies with REDCap projects and utilize its extensive data collection and management features.

## Local Disk

Designer utilizes local disk storage for caching and managing studies. Here's how local disk usage works:

- Study Caching: Valid studies designed in the Designer application are stored in the cache memory of the local disk. This caching mechanism ensures quick access and retrieval of studies during the design and modification process when your browser is closed or if you're no longer on the web page.

- Downloading Studies: Additionally, you can download studies as JSON files from Designer. These downloaded studies can be reloaded by selecting the "Load Study" option from the `Actions` tab. However, please note that if the downloaded study is invalid, the loading features will not work properly.

This concludes the documentation for the Designer application. As a researcher, you now have a comprehensive understanding of how to design studies, upload them to the database, create REDCap projects, generate QR codes, customize studies, and manage local disk usage.

We offer a diagram to highlight what we just explained: 

![designer_interfaces_sketch.svg](../../resources/images/designer_interfaces_sketch.svg)
