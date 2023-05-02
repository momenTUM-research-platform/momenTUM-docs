# Study File

The study file is modelled using a class diagram.
Depending on the programming language, it has been implemented as `interface`(TypeScript) and `Struct`(Rust).
The chart was created using [lucid.app](https://lucid.app)
> [edit chart](https://lucid.app/lucidchart/0254693e-6e79-4ecf-889b-467fbcc3ad28/edit?viewport_loc=-1386%2C-525%2C6983%2C3993%2CHWEp-vi-RSFO&invitationId=inv_775f17bc-cc7b-4de3-9402-f161610e2cef)

![study-interface-class-diag](../../resources/images/momentum%20study%20interface.svg)

## mermaid diagram

```mermaid
    classDiagram
        Study "1" *-- "1..*" Module
        Study *-- Properties

        Module *-- Alert
        Module *-- Time
        Module *-- Graph
        Module --> PvtBody
        Module --> SurveyBody

        SurveyBody --> Section
        Section --> Question
        Question --> Instruction
        Question --> YesNo
        Question --> Text
        Question --> DateTime
        Question --> Slider
        Question --> Multi
        Question --> File
        Question --> Media
        Question --> External

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
            type:
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