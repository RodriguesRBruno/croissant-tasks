
### Assumptions
- This Croissant Task Definition refers to the general task of evaluating hardware in Machine Learning tasks, obtaining some metrics that can be used for benchmarking.
  - The exact tasks used for evaluation, hardware to be evaluated and metrics collected are up to specific solutions to define.


```json
{
    "task_definition": {
        "@type": "croissant:TaskDefinition",
        "name": "Hardware Benchmarking Task",
        "description": "This Task Definition defines the generalized task of benchmarking hardware regarding Machine Learning performance..",
        "url": "https://url/for/generic/hardware/benchmarking/webpage",
        "license": "Apache License 2.0"
    },
    "task_type": {
        "@type": "croissant:TaskType",
        "task_type": "Hardware Benchmarking",
        "description": "This task takes in some hardware as input and benchmarks its performance. The chosen output metrics and machine learning tasks used for for evaluations are left to Solutions to implement."
    },
    "inputs": [
        {
            "@type": "croissant:InputAssetSpecification",
            "name": "Input Model Specification",
            "constraints": {
                "@type": "Hardware",
                "components": "Any"
            }
        }
    ],
    "outputs": []
}
```