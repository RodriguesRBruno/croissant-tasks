
### Assumptions
- This Croissant Task Solution refers to MLPerf benchmark.
- Specific hardware may be taken in as input.
  - For this toy example, it could be a CPU and/or GPU
- Specific machine learning models with specific data are run using this hardware. Metrics are then evaluated and used to benchmark the hardware.
  - Submissions to the benchmark will correspond to Task Instances.

```json
{
    "task_definition": {
        "@type": "croissant:TaskSolution",
        "name": "MLPerf Benchmarking Example",
        "description": "This Task Definition defines the generalized task of benchmarking hardware regarding Machine Learning performance.",
        "task_definition_url": "https://github.com/RodriguesRBruno/croissant-tasks/blob/main/Hardware%20Benchmark/hwbenchmark-taskdefinition.md",
        "license": "Apache License 2.0"
    },
    "inputs": [
        {
            "@type": "croissant:InputAssetSpecification",
            "name": "Input Model Specification",
            "constraints": {
                "@type": "Hardware",
                "components": "CPU, GPU"
            }
        }
    ],
    "outputs": [],
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
    }
}
```