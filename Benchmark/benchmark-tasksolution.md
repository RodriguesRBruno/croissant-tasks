### Assumptions
- This Croissant Task Solution refers to the AILuminate Demo Dataset.
  - This solution also corresponds to the Task Problem present in this repository

- A single asset (a model) is used as input. There is no input data.
- There are no explicit outputs in terms of data or assets.
- There is, however, an evaluation of the input model, which will output metrics regarding the evaluated model.
  - For the Task Solution, the evaluation metrics have values.

```json
{
    "task_definition": {
        "@type": "croissant:TaskSolution",
        "name": "AILuminate Benchmark Example",
        "description": "This Task Solution defines a specific AILuminate Model submission",
        "task_problem_url": "https://github.com/RodriguesRBruno/croissant-tasks-dicom-2-nifti/blob/main/benchmark/benchmark-taskproblem.md",
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
                "@type": "InputAsset",
                "name": "Input Model",
                "url": "https://link/to/model"
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