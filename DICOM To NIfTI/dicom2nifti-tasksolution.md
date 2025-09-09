### Assumptions 
- This Croissant Task Problem refers to the general problem of converting a Medical image from DICOM format (.dcm) to NIfTI format (.nii.gz).
- This is a Data Preparation Task. The format for input and output data are specified.
  - Concrete data must be supplied with the corresponding Task Solutions.
- The implementation is left open and should be part of corresponding Task Solutions.
  - The scope of the implementation is left open. It could be as simple as a single Python function or, ideally, something more easily reproducible, such as a Docker image.
- The `task_definition.url` field  points to some webpage that has information regarding the task
  - Could be a GitHub repo with source code, a website with information on the task, something else entirely.
- The evaluation field is omitted entirely, as this is a Data Preparation task.
- The `sample_data` field also includes concrete data, in the form of `sample_input` and `sample_output`. In a real use case, this should be compose of small dataset(s) that may be used for other developers while building their solution for testing, validation, etc.

  
```json
{
    "task_definition": {
        "@type": "croissant:TaskSolution",
        "name": "DICOM To NIfTI Conversion of Dataset XYZ",
        "description": "This TaskSolution represents a conversion of medical images from the DICOM Format (.dcm) to NIfTI (.nii.gz). A Task solution includes concrete values for input data, output data and implementation.",
        "task_problem_url": "https://github.com/RodriguesRBruno/croissant-tasks-dicom-2-nifti/blob/main/dicom-to-nifti/dicom2nifti-taskproblem.md"
    },
    "task_type": {
        "@type": "croissant:TaskType",
        "task_type": "Data Processing",
        "description": "This is a data processing task"
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
    },
    "inputs": {
        "assets": [],
        "data": [
            {
                "@type": "croissant:InputData",
                "name": "DICOM Image Directory",
                "description": "A directory containing a single series of DICOM images.",
                "format": "DICOM Images (.dcm)",
                "recordSets": [
                    {
                        "@type": "RecordSet",
                        "name": "ImageRecords",
                        "description": "Records of input DICOM images",
                        "field": [
                            {
                                "@type": "Field",
                                "name": "image_id",
                                "description": "Unique identifier for the image.",
                                "dataType": "http://schema.org/Text"
                            },
                            {
                                "@type": "Field",
                                "name": "filename",
                                "description": "Filename of the image.",
                                "dataType": "http://schema.org/Text",
                                "source": {
                                    "@type": "Extract",
                                    "fileSet": [
                                        {
                                            "@type": "FileSet",
                                            "name": "ImageFiles",
                                            "containedIn": "directory/with/input/dicom/images",
                                            "encodingFormat": ".dcm"
                                        }
                                    ],
                                    "extract": {
                                        "column": "filename"
                                    }
                                }
                            },
                            {
                                "@type": "Field",
                                "name": "image_content",
                                "description": "The raw image data.",
                                "dataType": "http://schema.org/ImageObject",
                                "source": {
                                    "@type": "Extract",
                                    "fileSet": [
                                        {
                                            "@type": "FileSet",
                                            "name": "ImageFiles"
                                        }
                                    ],
                                    "extract": {
                                        "column": "content"
                                    }
                                }
                            }
                        ]
                    }
                ]
            }
        ]
    },
    "outputs": {
        "assets": [],
        "data": [
            {
                "@type": "croissant:OutputData",
                "name": "NIfTI image",
                "description": "A NIfTI compressed image is generated from all the input DICOM images.",
                "format": "Compressed NIfTI (.nii.gz)",
                "recordSets": [
                    {
                        "@type": "RecordSet",
                        "name": "ImageRecords",
                        "description": "Records of the output NIfTI File",
                        "field": [
                            {
                                "@type": "Field",
                                "name": "image_id",
                                "description": "Unique identifier for the image.",
                                "dataType": "http://schema.org/Text"
                            },
                            {
                                "@type": "Field",
                                "name": "filename",
                                "description": "Filename of the image.",
                                "dataType": "http://schema.org/Text",
                                "source": {
                                    "@type": "Extract",
                                    "fileSet": [
                                        {
                                            "@type": "FileSet",
                                            "name": "ImageFiles",
                                            "containedIn": "path/to/output/nifti/file",
                                            "encodingFormat": ".nii.gz"
                                        }
                                    ],
                                    "extract": {
                                        "column": "filename"
                                    }
                                }
                            },
                            {
                                "@type": "Field",
                                "name": "image_content",
                                "description": "The raw image data.",
                                "dataType": "http://schema.org/ImageObject",
                                "source": {
                                    "@type": "Extract",
                                    "fileSet": [
                                        {
                                            "@type": "FileSet",
                                            "name": "ImageFiles"
                                        }
                                    ],
                                    "extract": {
                                        "column": "content"
                                    }
                                }
                            }
                        ]
                    }
                ]
            },
            {
                "@type": "croissant:OutputData",
                "name": "Execution metadata",
                "description": "A CSV file containing metadata about an execution",
                "format": ".csv",
                "recordSets": [
                    {
                        "@type": "RecordSet",
                        "name": "csv_records",
                        "source": {
                            "fileObject": "nifti_conversion_csv",
                            "extract": {
                                "column": [
                                    "field_1",
                                    "field_2",
                                    "field_3"
                                ]
                            }
                        },
                        "fields": [
                            {
                                "@type": "Field",
                                "name": "field_1",
                                "dataType": "sc:Text"
                            },
                            {
                                "@type": "Field",
                                "name": "field_2",
                                "dataType": "sc:Integer"
                            },
                            {
                                "@type": "Field",
                                "name": "field_3",
                                "dataType": "sc:Text"
                            }
                        ]
                    }
                ]
            }
        ]
    }
}
```
### Notes
- I purposedly left out some fields from the input/output data when compared to the [Task Problem file](./dicom2nifti-taskproblem.md). For example, there is no link to implementation of file validation here. I feel those are a part of the Task Problem. If the Task Solution ran and had valid output, then the output must conform to the Problem's validation practices, so repeating validation here feels unnecessary.
  - Of course, the Task Problem is referenced in the `task_definition` portion of this, so the validation can still be verified.
- I attempted to represent hypothetical input/output concrete data as RecordSets.
  - This was my first time using Croissant RecordSets so I image there must be some mistakes! :) I hope the general idea is clear.


### Questions
- How to specificy an "OR" logic for dependencies? In the Medical world, many users do not support Docker due to security concerns (the Docker Daemon requires root access), but rather Apptainer (formerly known as Singularity). In this sense, the true container dependency could be Docker OR Apptainer, not necessarily both.
- How to represent the output/input in instances where the data is private? Should there simply be no source listed in the RecordSet?
- What level of reproducibility are we aiming for when elaborating a Task Solution definition?
  - Same output (within some error margin for stochastic processes) with same input, regardless of whatever happens in between?
  - Similar execution times and resource usage?
  - Other?