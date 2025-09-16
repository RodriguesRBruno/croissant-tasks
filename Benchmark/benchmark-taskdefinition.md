
### Assumptions
- This Croissant Task Definition refers to the general task of evaluating LLMs, obtaining some metrics that can be used for benchmarking.
  - The exact LLM specifications and metrics collected are left up to solutions


```json
{
    "task_definition": {
        "@type": "croissant:TaskDefinition",
        "name": "Model Benchmarking Task",
        "description": "This Task Definition defines the generalized task of benchmarking LLMs.",
        "url": "https://url/for/generic/benchmarking/webpage",
        "license": "Apache License 2.0"
    },
    "task_type": {
        "@type": "croissant:TaskType",
        "task_type": "Model Benchmarking",
        "description": "This task takes a LLM as input and benchmarks its performance. The chosen output metrics and sample data for evaluations are left to Solutions to implement."
    },
    "inputs": [
        {
            "@type": "croissant:InputAssetSpecification",
            "name": "Input Model Specification",
            "constraints": {
                "@type": "LLM",
                "model_input": "prompts"
            }
        }
    ],
    "outputs": []
}
```