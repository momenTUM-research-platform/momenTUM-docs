# Component Overview

- Pages
    - Home
    - Progress
    - Settings
    - Pvt
    - Scanner
    - Survey
- Services
    - [barcode](#barcode-service)
    - [loading](#loading-service)
    - [notification](#notification-service)
    - [storage](#storage-service)
    - [study-task](#study-task-service)
    - [survey-cache](#survey-cache-service)
    - [survey-data](#survey-data-service)
    - [uuid](#uuid-service)

# Barcode service

- Methods
    - startScan
    - checkPermission
    - didUserGrantPermission
    - stopScan

# Loading service

- Methods
    - dismiss
    - present

- Attributes
    - isLoading
    - isCaching

# Notification service

- Injections (constructor params)
    - storage
    - studyTasksService

- Methods
    - createChannel
    - deleteChannel
    - listChannels
    - fireQueuedEvents
    - addListenerOnClick
    - showLocalNotifications
    - scheduleNotification
    - cancelAll
    - getPending
    - requestPermissions
    - setNext30Notifications

# Storage service

- Injections (constructor params)
    - storage

- Methods
    - init
    - set
    - get
    - keys
    - removeItem
    - clear

# Study-task service

- Injections (constructor params)
    - storageService
    - loadingService

- Methods
    - generateStudyTasks
    - getAllTasks
    - getTaskDisplayList
    - checkTaskIsUnlocked

# Survey-cache service

- Attributes
    - win
    - mediaToCache
    - videoThumbnailsToCache
    - localMediaURLs
    - localThumbnailURLs
    - mediaCount
    - mediaDownloadedCount

- Injections (constructor params)
    - file
    - storage
    - loadingService

- Methods
    - downloadFile
    - getMediaURLs
    - cacheAllMedia
    - downloadAllMedia
    - checkIfFinished
    - updateMediaURLsInStudy

# Survey-data service

- Injections (constructor params)
    - httpClient
    - storage
    - platform
    - uuidService
    - studyTasksService

- Methods
    - getRemoteData
    - getFromLocalStorage
    - saveToLocalStorage
    - sendSurveyDataToServer
    - logPageVisitToServer
    - uploadPendingData
    - attemptHttpPost

# uuid service

- Methods
    - generateUUID

## Survey Page

- Injections (constructor parameters)
    - route
    - storage
    - domSanitizer
    - navController
    - studyTasksService
    - surveyDataService
    - toastController
    - ngZone
- Attributes
    - submit_text
    - current_section
    - num_sections
    - current_section_name
    - study
    - survey
    - questions
    - tasks
    - task_id
    - task_index
    - module_index
    - module_name

- Methods
    - ngOnInit
    - back
    - setUpQuestionVariables
    - setAnswer
    - changeCheckStatus
    - openExternalFile
    - toggleDynamicQuestions
    - submit
    - showToast
    - shuffle