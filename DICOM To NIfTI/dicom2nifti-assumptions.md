### Task Problem
- The [Croissant Task Problem](./dicom2nifti-taskproblem.jsonld) refers to the general problem of converting a Medical image from DICOM format (.dcm) to NIfTI format (.nii.gz).
- The Problem is a Data Preparation Task and requests the implementation of a conversion algorithm.
- Sample input (`cr:input`) and output (`cr:output`) data are provided.
- The `cr:implementation` field provides a specification (`cr:ImplementationSpec`) of the desired solution. Corresponding task solutions must conform to this spec.
- The `cr:evaluation` field provides an evaluation subtask, which evaluates the accuracy (i.e how many of the provided outputs did the solution generate from the provided inputs) of a given transformation.
  - Since `cr:evaluation` defines a subtask, it also has input, output and implementation fields. 
    - The implementation is a concrete field
    - The input makes reference to the NIfTI file output from the task (i.e it the evaluation takes in the output of a given Task Solution in order to evaluate it)
    - The output is a `cr:OutputSpec`, as it is generated for each implemented `TaskSolution` corresponding o this problem (i.e it is expected that different solutions would have different accuracy scores)


### Task Solution
- The [Croissant Task Solution](./dicom2nifti-tasksolution.jsonld) is a specific solution the [Task Problem defined in the same directory](./dicom2nifti-taskproblem.jsonld).
- The solution provides the fields that were defined as Specs in the Task Problem.
  - The solutions `cr:implementation` is a concrete implementation of a DICOM to NIfTi conversion program.
    - The present implementation is given in the form of a container image.
  - The `cr:evaluation` evaluation field present in the solution is a sub-Task Solution corresponding to the evaluation Task Problem.
    - It follows the same schema (using `sc:isBasedOn`), but provides a link to a concrete result file.
    - For this example, this file should store a single float, the accuracy score.
- The `cr:execution` field is added with information about the execution environment where this solution was ran and the evaluation metrics were collected.


### Task Execution
- The [Croissant Task Execution](./dicom2nifti-taskexecution.jsonld) represents a specific run of the [Task Solution defined in the same directory](./dicom2nifti-tasksolution.jsonld)
  - This run uses its own inputs and outputs, which are different form the sample data from the Task Problem. They must conform to the schemas given in the corresponding [Task Problem](./dicom2nifti-taskproblem.jsonld).
- The Execution also has its own `cr:execution` information.
- It also has its own Evaluation metrics.