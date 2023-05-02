# Architecture

The momentum platform consists of [5 subsystems](#subsystems). 3 of them are developed by us, the momentum team and have their own documenation chapter in this book. For a visual representation of the whole momentum platform, see the [sketch](#sketch). Detailed documentation of each interface can be found in the respective docs of each subsystem.

## Subsystems

### [Backend](./backend/overview.md)

Handles the interaction with the momentum server. Go to the chapter for its documentation.
> [link to the Backend chapter](./backend/overview.md)

### [Designer](./designer/overview.md)

Used by researcher to create momentum studies. Go to the chapter for its documentation.
> [link to the Designer chapter](./designer/overview.md)


### [Mobile App](./mobile-app/overview.md)

Used by study participants to complete tasks. Tasks are defined in momentum studies. Go to the chapter for its documentation.
> [link to the Mobile App chapter](./designer/overview.md)

### REDCap instance

Used by researchers to monitor and download the collected data. Go to their website for more information.
> [link to the REDCap website](https://www.project-redcap.org/)

### MongoDB instance

Backend data storage. Mainly used for mappings between studies and REDCap projects. Go to their website for more information.
> [link to the MongoDB website](https://www.mongodb.com/de-de)

## Sketch

![architecture-sketch](../resources/images/architecture-sketch.svg)