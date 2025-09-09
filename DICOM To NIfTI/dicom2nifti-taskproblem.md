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
    "inputs": {
        "assets": [],
        "data": [
            {
                "@type": "croissant:InputDataSpecification",
                "name": "DICOM Image Directory",
                "description": "A directory containing DICOM images. Ideally, all images should be part of a single image series.",
                "constraints": {
                    "@type": "DICOM Images",
                    "format": ".dcm",
                    "validation": "https://some/url/for/code/that/validates/input/is/valid/dicom"
                }
            }
        ]
    },
    "outputs": {
        "assets": [],
        "data": [
            {
                "@type": "croissant:OutputDataSpecification",
                "name": "NIfTI image",
                "description": "A NIfTI compressed image is generated from all the input DICOM images.",
                "constraints": {
                    "@type": "NIfTI Image",
                    "format": ".nii.gz",
                    "validation": "https://some/url/for/code/that/validates/output/is/valid/nifti"
                }
            },
            {
                "@type": "croissant:OutputDataSpecification",
                "name": "Execution metadata",
                "description": "A CSV file containing metadata about an execution",
                "constraints": {
                    "@type": "CSV File",
                    "format": ".csv",
                    "fields": [
                        {
                            "@type": "Field",
                            "name": "field_1",
                            "dataType": "http://schema.org/Text"
                        },
                        {
                            "@type": "Field",
                            "name": "field_2",
                            "dataType": "http://schema.org/Integer"
                        },
                        {
                            "@type": "Field",
                            "name": "field_3",
                            "dataType": "http://schema.org/Float"
                        }
                    ]
                }
            }
        ]
    },
    "samples": {
        "inputs": {
            "assets": [],
            "data": [
                {
                    "@type": "croissant:InputData",
                    "name": "Sample DICOM Image Directory",
                    "description": "A sample directory containing a single series of DICOM images. May be used for the development of Implementations in a Croissant Task Solution for this problem.",
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
                                                "containedIn": "/sample/directory/with/input/dicom/images",
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
                    "name": "Sample NIfTI image",
                    "description": "A sample NIfTI compressed image. May be used to validate Implementations in Croissant Task Solutions corresponding to this problem.",
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
                                                "containedIn": "path/to/sample/output/nifti/file",
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
                                    "dataType": "http://schema.org/Text"
                                },
                                {
                                    "@type": "Field",
                                    "name": "field_2",
                                    "dataType": "http://schema.org/Integer"
                                },
                                {
                                    "@type": "Field",
                                    "name": "field_3",
                                    "dataType": "http://schema.org/Float"
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    }
}
```