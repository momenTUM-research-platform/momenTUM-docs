# Study Object

The study object is a JSON object with key value pairs according to a certain schema. The schema is modelled using a class diagram.

## mermaid diagram

```mermaid
    classDiagram
        Study "1" -- "1..*" Module
        Study "1" -- "1" Properties

        Module "1" -- "1" Alerts
        Module "1" -- "1" Graph
        Module "1" -- "0..1" PvtBody
        Module "1" -- "0..1" SurveyBody
        Alerts "1" -- "1..*" Time

        SurveyBody "1" -- "1..*" Section
        Section "1" -- "1..*" Question
        Question "1" -- "0..1" Instruction
        Question -- "0..1" YesNo
        Question -- "0..1" Text
        Question -- "0..1" DateTime
        Question -- "0..1" Slider
        Question -- "0..1" Multi
        Question -- "0..1" File
        Question -- "0..1" Media
        Question -- "0..1" External

        class Study {
            <<interface>>
            properties: Properties,
            modules: Module[],
        }

        class Module {
            <<interface>>
            type: 'pvt' | 'survey',
            name: string,
            submit_text: string,
            condition: string,
            alerts: Alerts,
            graph: Graph,
            id: string,
            unlock_after: string[],
            shuffle: boolean,
            body: SurveyBody | PvtBody,
        }

        class Properties {
            <<interface>>
            study_id: string,
            study_name: string,
            instructions: string,
            banner_url: string,
            support_email: string,
            support_url: string,
            ethics: string,
            pls: string,
            created_by: string,
            empty_msg: string,
            post_url: string,
            conditions: string[],
            cache: boolean,
        }

        class Alerts {
            <<interface>>
            title: string,
            message: string,
            start_offset: number,
            duration: number,
            times: Time[],
            random: boolean,
            random_interval: number,
            sticky: boolean,
            sticky_label: string,
            timeout: boolean,
            timeout_after: number,
        }

        class Time {
            <<interface>>
            hours: number,
            minutes: number,
        }

        class Graph {
            <<interface>>
            display: boolean,
            variable: string,
            title: string,
            blurb: string,
            type: 'bar' | 'line',
            max_points: number,
        }

        class PvtBody {
            <<interface>>
            type: 'pvt',
            trials: number,
            min_waiting: number,
            max_waiting: number,
            show: boolean,
            max_reaction: number,
            exit: boolean,
        }

        class SurveyBody {
            <<interface>>
            type: 'survey',
            sections: Section[],
        }

        class Section {
            <<interface>>
            id: string,
            name: string,
            shuffle: boolean,
            questions: Question[],
        }

        class Question {
            <<interface>>
            id: string,
            text: string,
            body:
                | Instruction
                | DateTime
                | Multi
                | Text
                | Slider
                | Media
                | YesNo
                | External
                | File,
            required: boolean,
            hide_id: string,
            hide_value: boolean,
            hide_if: boolean,
        }

        class Instruction {
            <<interface>>
            type: 'instruction',
        }

        class YesNo {
            <<interface>>
            type: 'yesno',
            yes_text: string,
            no_text: string,
        }

        class Text {
            <<interface>>
            type: 'text',
            subtype: 'short' | 'long' | 'numeric',
        }

        class DateTime {
            <<interface>>
            type: 'datetime',
            subtype: 'date' | 'time' | 'datetime',
        }

        class Slider {
            <<interface>>
            type: 'slider',
            min: number,
            max: number,
            hint_left: string,
            hint_right: string,
        }

        class Multi {
            <<interface>>
            type: 'multi',
            radio: boolean,
            modal: boolean,
            options: string[],
            shuffle: boolean,
        }

        class File {
            <<interface>>
            type: 'file',
            src: string,
            file_name: string,
        }

        class Media {
            <<interface>>
            type: 'media',
            subtype: 'image' | 'video' | 'audio',
            src: string,
            thumb: string,
        }

        class External {
            <<interface>>
            type: 'external',
            src: string,
        }

```
