### Task Problem
- The Croissant Task Problem refers to the general problem of converting a Medical image from DICOM format (.dcm) to NIfTI format (.nii.gz).
- The Problem is a Data Preparation Task. The format for input and output data are specified.
- The `task_definition.url` field  points to some webpage that has information regarding the task
  - Could be a GitHub repo with source code, a website with information on the task, something else entirely.
- The `requested_assets` field indicates an `implementation` is requested and it should be submitted as a Docker container.
- The `reference_assets` field includes concrete data, of `datasets.input` and `datasets.output`. In a real use case, this should be compose of small dataset(s) that may be used for other developers while building their solution for testing, validation, etc.
  - The sample data is used to implement and debug the corresponding solutions.

### Task Solution
- The Croissant Task Solution is a specific solution the [Task Problem defined in the same directory](./dicom2nifti-taskproblem.md).
- The solution provides an `implementation` to the Task Problem.
  - The present implementation is given in the form of a container image.
- It is assumed this implementation was developed with the sample data inputs and outputs from the Task Problem.
  - Therefore, no input/output data is specified here. 
  - Specific inputs/outputs are part of Task Instances.
- Hardware and software requirements are present, but optional.


### Task Instance
- The Croissant Task Instance represents a specific run of the [Task Solution defined in the same directory](./dicom2nifti-tasksolution.md)
  - The run uses the input data defined in `inputs` and produces the outputs defined in `outputs`.
  - The inputs and outputs must conform to the schemas given in the corresponding [Task Problem](./dicom2nifti-taskproblem.md)