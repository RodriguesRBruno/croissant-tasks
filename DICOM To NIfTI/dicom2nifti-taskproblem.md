# DICOM to NIfTI - Croissant Task Problem

The purpose of this file is to define the Data Preparation Task of converting medical images from DICOM to NIfTI in a more general sense. I attempted to describe the inputs/outputs in a general sense, as the [Task Solution](./dicom2nifti-tasksolution.md) should have these defined in a concrete way. Some notes and questions that arose while creating this example are included at the end of this Markdown file.

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
    "input_data_spec": [
        {
            "@type": "croissant:InputData",
            "name": "DICOM Image Directory",
            "description": "A directory containing DICOM images. Ideally, all images should be part of a single image series.",
            "format": "DICOM Images (.dcm)",
            "validation": "https://some/url/for/code/that/validates/input/is/valid/dicom"
        }
    ],
    "output_data_spec": [
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
    "sample_data": {
        "sample_input": [
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
        ],
        "sample_output": [
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
- Implementation URL points to some webpage that has information regarding the task
  - Could be a GitHub repo with source code, a website with information on the task, something else entirely.
- The evaluation field is omitted entirely, as this is a Data Preparation task, not a model evaluation.
- Assumed the Croissant Task Problem, at least in this example, does NOT have a concrete implementation of the Data Transformation. The implementation must be included in the corresponding Croissant Task solutions.
  - However, Implementations will be bound by the input data and output data specifications.
- Here, the fields `input_data_spec` and `output_data_spec` were used to signal that these are just specifications of the input/output data format, **NOT** actual input and output data.
  - The corresponding [Croissant Task Solution](./dicom2nifti-tasksolution.md) includes concrete data
  - The `sample_data` field also includes concrete data, in the form of `sample_input` and `sample_output`. In a real use case, this should be compose of small dataset(s) that may be used for other developers while building their solution for testing, validation, etc.

### Questions
- How to specificy an "OR" logic for dependencies? In the Medical world, many users do not support Docker due to security concerns (the Docker Daemon requires root access), but rather Apptainer (formerly known as Singularity). In this sense, the true container dependency could be Docker OR Apptainer, not necessarily both.
- Some metadata could be included in the format. For example, for discoverability purposes, there could be a specific field listing the data formats used for input/output, areas of study where this type of transformation is applicable and so on. Where would this fit best?