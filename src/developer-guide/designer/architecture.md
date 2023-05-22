# Architecture

## React components
```mermaid
    flowchart TD
        App
        Layout
        Graph
        Calendar
        Commit
        CustomNodes
        Download
        Form
        Menu
        Modal
        QR
        Redcap
        Settings
        Upload

        App --> Layout

        Layout --> Menu
        Layout --> Settings
        Layout --> Graph
        Layout --> Calendar
        Layout --> Form

        Menu --> Modal

        Modal --> QR
        Modal --> Download
        Modal --> Upload
        Modal --> Redcap

```