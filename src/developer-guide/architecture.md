# Architecture

The momentum platform consists of [5 subsystems](#subsystems). 3 of them are developed by us, the momentum team and have their own documenation chapter in this book. For a visual representation of the whole momentum platform, see the [sketch](#sketch). Detailed documentation of each interface can be found in the respective docs of each subsystem.

## Subsystems

### [Designer](./designer/overview.md)

Used by researcher to create momentum studies.

### [Backend](./backend/overview.md)

Handles the interaction with the momentum server.

### [Mobile app](./mobile-app/overview.md)

Used by study participants to complete tasks. Tasks are defined in momentum studies.

### [REDCap instance](https://www.project-redcap.org/)

Used by researchers to monitor and download the collected data.

### [MongoDB instance](https://www.mongodb.com/de-de)

Backend data storage. Mainly used for mappings between studies and REDCap projects.

## Sketch

![architecture-sketch](../resources/images/architecture-sketch.svg)