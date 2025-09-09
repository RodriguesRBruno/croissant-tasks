### Assumptions
- This Croissant Task Problem refers to the AILuminate Demo Dataset.
- The public demo dataset is included as sample input data for development of Croissant Task Solutions.
- A single asset (a model) must be used as input on corresponding Task Solutions. Therefore, a `InputAssetSpecification` appears in the `inputs` field.
  - No input data is expected for the corresponding Task Solutions. Therefore, the `inputs.data` field is empty. It is shown here for clarity, but could be omitted.
- No explicit outputs in terms of data or assets are expected of the Task Solutions. Therefore, both `outputs.assets` and `outputs.data` are left empty and present here only for clarity.
  - There is, however, an evaluation of the input model, which will output metrics regarding the evaluated model.


```json
{
    "task_definition": {
        "@type": "croissant:TaskProblem",
        "name": "AILuminate Benchmark Example",
        "description": "This TaskProblem defines a generic template for AILuminate Model submissions",
        "url": "https://mlcommons.org/ailuminate/",
        "license": "Apache License 2.0"
    },
    "task_type": {
        "@type": "croissant:TaskType",
        "task_type": "Model Benchmarking",
        "description": "This task takes a Machine Learning Model as input and benchmarks its performance. The output are metrics that measure how well the model performed on the benchmark data."
    },
    "inputs": {
        "assets": [
            {
                "@type": "croissant:InputAssetSpecification",
                "name": "Input Model Specification",
                "constraints": {
                    "@type": "LLM",
                    "model_input": "prompts"
                }
            }
        ],
        "data": []
    },
    "outputs": {
        "assets": [],
        "data": []
    },
    "evaluation": {
        "@type": "croissant:Evaluation",
        "metrics": [
            {
                "name": "metric1",
                "type": "float",
                "description": "First measured metric"
            },
            {
                "name": "metric2",
                "type": "float",
                "description": "Second measured metric"
            }
        ]
    },
    "samples": {
        "inputs": {
            "assets": [],
            "data": [
                {
                    "@type": "croissant:InputData",
                    "name": "AILuminate Demo Prompts",
                    "url": "https://github.com/mlcommons/ailuminate",
                    "description": "This dataset includes the open test prompts from AILuminate. The benchmark itself runs on a different set of prompts.",
                    "format": ".csv",
                    "recordSets": [
                        {
                            "@type": "RecordSet",
                            "name": "AILuminate Demo - English",
                            "source": {
                                "fileObject": "https://github.com/mlcommons/ailuminate/blob/main/airr_official_1.0_demo_en_us_prompt_set_release.csv",
                                "extract": {
                                    "column": [
                                        "release_prompt_id",
                                        "prompt_text",
                                        "hazard",
                                        "persona",
                                        "locale",
                                        "prompt_hash"
                                    ]
                                }
                            },
                            "fields": [
                                {
                                    "@type": "Field",
                                    "name": "release_prompt_id",
                                    "dataType": "http://schema.org/Text"
                                },
                                {
                                    "@type": "Field",
                                    "name": "prompt_text",
                                    "dataType": "http://schema.org/Text"
                                },
                                {
                                    "@type": "Field",
                                    "name": "hazard",
                                    "dataType": "http://schema.org/Text"
                                },
                                {
                                    "@type": "Field",
                                    "name": "persona",
                                    "dataType": "http://schema.org/Text"
                                },
                                {
                                    "@type": "Field",
                                    "name": "locale",
                                    "dataType": "http://schema.org/Text"
                                },
                                {
                                    "@type": "Field",
                                    "name": "prompt_hash",
                                    "dataType": "http://schema.org/Text"
                                }
                            ]
                        },
                        {
                            "@type": "RecordSet",
                            "name": "AILuminate Demo - French",
                            "source": {
                                "fileObject": "https://github.com/mlcommons/ailuminate/blob/main/airr_official_1.0_demo_fr_fr_prompt_set_release.csv",
                                "extract": {
                                    "column": [
                                        "release_prompt_id",
                                        "prompt_text",
                                        "hazard",
                                        "persona",
                                        "locale",
                                        "prompt_hash"
                                    ]
                                }
                            },
                            "fields": [
                                {
                                    "@type": "Field",
                                    "name": "release_prompt_id",
                                    "dataType": "http://schema.org/Text"
                                },
                                {
                                    "@type": "Field",
                                    "name": "prompt_text",
                                    "dataType": "http://schema.org/Text"
                                },
                                {
                                    "@type": "Field",
                                    "name": "hazard",
                                    "dataType": "http://schema.org/Text"
                                },
                                {
                                    "@type": "Field",
                                    "name": "persona",
                                    "dataType": "http://schema.org/Text"
                                },
                                {
                                    "@type": "Field",
                                    "name": "locale",
                                    "dataType": "http://schema.org/Text"
                                },
                                {
                                    "@type": "Field",
                                    "name": "prompt_hash",
                                    "dataType": "http://schema.org/Text"
                                }
                            ]
                        }
                    ]
                }
            ],
        },
        "outputs": {
            "assets": [],
            "data": []
        }
    }
}
```