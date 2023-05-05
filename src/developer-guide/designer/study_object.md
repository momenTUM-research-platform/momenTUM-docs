# Study Object

The study object is a complex object with key value pairs according to a certain protocol. The protocol is modelled using a class diagram.
Depending on the programming language, it has been implemented as `interface`(TypeScript) and `Struct` (Rust).

## mermaid diagram

```mermaid
    classDiagram
        Study "1" *-- "1..*" Module
        Study "1" *-- "1" Properties

        Module "1" *-- "1" Alert
        Module "1" *-- "1" Time
        Module "1" *-- "1" Graph
        Module "1" --> "0..1" PvtBody
        Module "1" --> "0..1" SurveyBody

        SurveyBody "1" --> "1..*" Section
        Section "1" --> "1..*" Question
        Question "1" --> "0..1" Instruction
        Question --> "0..1" YesNo
        Question --> "0..1" Text
        Question --> "0..1" DateTime
        Question --> "0..1" Slider
        Question --> "0..1" Multi
        Question --> "0..1" File
        Question --> "0..1" Media
        Question --> "0..1" External

        class Study {
            properties: Properties;
            module: Module[];
        }

        class Module {
            name: string;
            submit_text: 
            string;condition: string;
            alerts: Alerts[];
            graph: Graph;
            id: string;
            unlock_after: string[];
            shuffle: boolean;
            body: SurveyBody | PvtBody;
        }

        class Properties {
            study_id: string;
            study_name: string;
            instructions: string;
            banner_url: string;
            support_email: string;
            support_url: string;
            ethics: string;
            pls: string;
            created_by: string;
            empty_msg: string;
            post_url: string;
            conditions: string[];
            cache: boolean;
        }

        class Alert {
            title: string;
            message: string;
            start_offset: number;
            duration: number;
            times: Time[];
            random: boolean;
            random_interval: number;
            sticky: boolean;
            sticky_label: string;
            timeout: boolean;
            timeout_after: number;
        }

        class Time {
            hours: number;
            minutes: number;
        }

        class Graph {
            display: boolean;
            variable: string;
            title: string;
            blurb: string;
            type: 'bar' | 'line';
            max_points: number;
        }

        class PvtBody {
            type: 'pvt';
            trials: number;
            min_waiting: number;
            max_waiting: number;
            show: boolean;
            max_reaction: number;
            exit: boolean;
        }

        class SurveyBody {
            type: 'survey';
            sections: Section[]
        }

        class Section {
            id: string;
            name: string;
            shuffle: boolean;
            questions: Question[];
        }

        class Question {
            id: string;
            text: string;
            body:
                | Instruction
                | Datetime
                | Multi
                | Text
                | Slider
                | Media
                | Yesno
                | External
                | File;
            required: boolean;
            hide_id: string;
            hide_value: boolean;
            hide_if: boolean;
        }
        
        class Instruction {
            type: 'instruction';
        }

        class YesNo {
            type: 'yesno';
            yes_text: string;
            no_text: string;
        }

        class Text {
            type: 'text';
            subtype: 'short' | 'long' | 'numeric';
        }

        class DateTime {
            type: 'datetime';
            subtype: 'date' | 'time' | 'datetime';
        }

        class Slider {
            type: 'slider';
            min: number;
            max: number;
            hint_left: string;
            hint_right: string;
        }

        class Multi {
            type: 'multi';
            radio: boolean;
            modal: boolean;
            options: string[];
            shuffle: boolean;
        }

        class File {
            type: 'file';
            src: string;
            file_name: string;
        }

        class Media {
            type: 'media';
            subtype: 'image' | 'video' | 'audio';
            src: string;
            thumb: string;
        }

        class External {
            type: 'external';
            src: string;
        }

```