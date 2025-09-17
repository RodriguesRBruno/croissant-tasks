### Assumptions
- This Croissant Task Instance refers to a hypothetical MLPerf benchmark submission.
- This hypothetical submission is defined by the hardware used, which refer to specific CPU and GPU models.
  - The associated metrics obtained when benchmarking this hardware are also included.

```json
{
    "task_definition": {
        "@type": "croissant:TaskSolution",
        "name": "MLPerf Benchmarking Example",
        "description": "This Task Definition defines the generalized task of benchmarking hardware regarding Machine Learning performance..",
        "task_definition_url": "https://github.com/RodriguesRBruno/croissant-tasks/blob/main/Hardware%20Benchmark/hwbenchmark-taskdefinition.md",
        "task_solution_url": "https://github.com/RodriguesRBruno/croissant-tasks/blob/main/Hardware%20Benchmark/hwbenchmark-tasksolution.md",
        "license": "Apache License 2.0"
    },
    "inputs": [
        {
            "@type": "croissant:HardwareInput",
            "name": "CPU of Some Model",
            "clock_speed": "XXX MHz",
            "another_spec":"another_value"
        },
        {
            "@type": "croissant:HardwareInput",
            "name": "GPU of Some Model",
            "vram": "XXX GB",
            "yet_another_spec":"yet_another_value"
        }
    ],
    "outputs": [],
    "evaluation": {
        "@type": "croissant:Evaluation",
        "metrics": [
            {
                "name": "metric1",
                "type": "float",
                "description": "First measured metric",
                "value": "1"
            },
            {
                "name": "metric2",
                "type": "float",
                "description": "Second measured metric",
                "value": "2"
            }
        ]
    }
}
```