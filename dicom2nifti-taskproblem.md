# DICOM to NIfTI - Croissant Task Problem

The purpose of this file is to define the Data Preparation Task of converting medical images from DICOM to NIfTI in a more general sense. I attempted to describe the inputs/outputs in a general sense, as the [Task Solution](./dicom2nifti-tasksolution.md) should have these defined in a concrete way.

```json
{
    "task_definition": {
        "@type": "croissant:TaskProblem",
        "name": "DICOM To NIfTI Conversion",
        "description": "This TaskProblem defines the generalized task of converting medical images from the DICOM Format (.dcm) to NIfTI (.nii.gz)",
        "url": "https://some/url/for/code/repo",
        "license": "Apache License 2.0",
    },
    "task_type": {
        "@type": "croissant:TaskType",
        "task_type": "Data Processing",
        "description": "This is a data processing task"
    },
    "input_data": [
        {
            "@type": "croissant:InputData",
            "name": "DICOM Image Directory",
            "description": "A directory containing DICOM images. Ideally, all images should be part of a single image series.",
            "format": "DICOM Images (.dcm)",
            "validation": "https://some/url/for/code/that/validates/input/is/valid/dicom"
        }
    ],
    "output_data": [
        {
            "@type": "croissant:OutputData",
            "name": "NIfTI image",
            "description": "A NIfTI compressed image is generated from all the input DICOM images.",
            "format": "Compressed NIfTI (.nii.gz)",
            "validation": "https://some/url/for/code/that/validates/output/is/valid/nifti"
        },
        {
            "@type": "croissant:OutputData",
            "name": "Execution metadata",
            "description": "A CSV file containing metadata about an execution",
            "format": ".csv",
            "validation": "https://some/url/for/code/that/validates/this/csv/is/formatted/correctly"
        }
    ],
    "implementation": {
        "@type": "croissant:Implementation",
        "description": "This task consists of a Python function that does the image conversion",
        "container_image": "docker://docker.io/user/image_repo:tag"
    },
    "execution": {
        "@type": "croissant:Execution",
        "hardware_requirements": [
            "CPU",
            "8 GB RAM"
        ],
        "dependencies": [
            "Docker"
        ]
    }
}
```

Some notes/questions I had while writing this example:
- Are URLs for implementation absolutely required?
  - If an implementation is private, how to specify it in this format?
- I assumed we can provide a Container image with the execution code. This seems more easily reproducible than listing some source for the execution code + required dependencies.
- Is pointing to external code for input/output validation the best way to do this? Maybe they could be included in the execution docker image? 
  - If we point to external code, the validation checks are more transparent to users (ie they can just click a link and see the code), while them being baked into the Container image would be more opaque (download image and manually check the code inside). On the other hand, having it all in the Container makes execution much simpler (just run the container).
  - Maybe we can do both in some sense? The task definition URL could point to a repo that implements everything and has the Dockerfile (or equivalent if a different container runtime is specified) that generates the execution image.
- How to specificy an "OR" logic for dependencies? In the Medical world, many users do not support Docker due to security concerns (the Docker Daemon requires root access), but rather Apptainer (formerly known as Singularity). In this sense, the true container dependency could be Docker OR Apptainer, not necessarily both.
- The evaluation field is omitted entirely, as this is a Data Preparation task, not a model evaluation.
- Some metadata could be included in the format. For example, for discoverability purposes, there could be a specific field listing the data formats used for input/output, areas of study where this type of transformation is applicable and so on. Where would this fit best?