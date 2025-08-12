# DICOM to NIfTI - Croissant Task Solution

The purpose of this file is to define the Data Preparation Task of converting medical images from DICOM to NIfTI in a more speficic sense. This includes concrete definitions of outputs/inputs. A more general description of the Task (for arbitrary inputs/outputs) is shown in the [Task Problem file](./dicom2nifti-taskproblem.md).
  
```json
{
    "task_definition": {
        "@type": "croissant:TaskSolution",
        "name": "DICOM To NIfTI Conversion of Dataset XYZ",
        "description": "This TaskSolution represents a conversion of medical images from the DICOM Format (.dcm) to NIfTI (.nii.gz).",
        "task_problem_url": "https://github.com/RodriguesRBruno/croissant-tasks-dicom-2-nifti/blob/main/dicom2nifti-taskproblem.md"
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
    ],
    "output_data": [
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
```

Some notes/questions I had while writing this example:
- I purposedly left out some fields from the input/output data when compared to the [Task Problem file](./dicom2nifti-taskproblem.md). For example, there is no link to implementation of file validation here. I feel those are a part of the Task Problem. If the Task Solution ran and had valid output, then the output must conform to the Problem's validation practices, so repeating validation here feels unnecessary.
  - Of course, the Task Problem is referenced in the `task_definition` portion of this, so the validation can still be verified.
- I attempted to represent hypothetical input/output concrete data as RecordSets.
  - This was my first time using Croissant RecordSets so I image there must be some mistakes! :) I hope the general idea is clear.
- How to represent the output/input in instances where the data is private? Should there simply be no source listed in the RecordSet?
- I left the `execution` field out of the Solution entirely, but maybe it can be included to keep some records about any given execution? For example, the usage of resources such as memory and even time (ie execution time)
- Where level of reproducibility are we aiming for when elaborating a Task Solution definition?
  - Same output (within some error margin for stochastic processes) with same input, regardless of whatever happens in between?
  - Similar execution times and resource usage?
  - Other?