### Assumptions
- This Croissant Task Instance refers to the AILuminate Demo Dataset.
  - This solution also corresponds to the Task Problem present in this repository
- A single asset (a model) is used as input. There is no input data.
- There are no explicit outputs in terms of data or assets.
- There is, however, an evaluation of the input model, which will output metrics regarding the evaluated model.
  - For the Task Solution, the evaluation metrics have values.

```json
{
    "task_definition": {
        "@type": "croissant:TaskInstance",
        "name": "AILuminate Benchmark Submission",
        "description": "This TaskInstance implements a submission to the AILuminate benchmark",
        "url": "https://mlcommons.org/ailuminate/",
        "task_definition_url": "https://github.com/RodriguesRBruno/croissant-tasks/blob/main/Benchmark/benchmark-taskdefinition.md",
        "task_solution_url": "https://github.com/RodriguesRBruno/croissant-tasks/blob/main/Benchmark/benchmark-tasksolution.md",
        "license": "Apache License 2.0"
    },
    "inputs": [
        {
            "@type": "InputAsset",
            "name": "Input Model",
            "url": "https://link/to/model"
        }
    ],
    "evaluation": {
        "@type": "croissant:Evaluation",
        "metrics": [
            {
                "name": "metric1",
                "type": "float",
                "description": "First measured metric",
                "value": "3.14159265359"
            },
            {
                "name": "metric2",
                "type": "float",
                "description": "Second measured metric",
                "value": "2.71828"
            }
        ]
    }
}
```