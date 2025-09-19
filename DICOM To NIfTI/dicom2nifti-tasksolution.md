### Assumptions 
- This Croissant Task Solution is a specific solution the [Task Problem defined in the same directory](./dicom2nifti-taskproblem.md).
- This solution provides an `implementation` to the Task Problem.
  - The present implementation is given in the form of a container image.
- It is assumed this implementation was developed with the sample data inputs and outputs from the Task Problem.
  - Therefore, no input/output data is specified here. 
  - Specific inputs/outputs are part of Task Instances.

  
```json
{
    "task_definition": {
        "@type": "croissant:TaskSolution",
        "name": "DICOM To NIfTI Conversion Implementation XYZ",
        "description": "This TaskSolution represents an implementation for the conversion of medical images from the DICOM Format (.dcm) to NIfTI (.nii.gz). A Task solution includes an implementation, but no concrete values for inputs/outputs.",
        "task_problem_url": "https://github.com/RodriguesRBruno/croissant-tasks/blob/main/DICOM%20To%20NIfTI/dicom2nifti-taskproblem.md"
    },
    "implementation": {
        "@type": "croissant:Implementation",
        "description": "This task consists of a Docker container that does the image conversion",
        "container_image": "docker://docker.io/user/image_repo:tag",
        "url": "https://link.to/source/code/from/docker/image"
    },
    "execution": {
        "@type": "croissant:Execution",
        "hardware_requirements": [
            "1 CPU",
            "8 GB RAM"
        ],
        "dependencies": [
            "Docker"
        ]
    }
}
```