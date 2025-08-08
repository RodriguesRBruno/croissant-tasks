# Croissant Tasks - DICOM To NIFTI Conversion
This repository provides two standardized Croissant Task examples for a hypothetical case of DICOM to NIfTI conversion. The task represents a conversion of a directory of DICOM files (`.dcm`) into a single NIfTI format image (`.nii.gz`). The provided files were written based on the [Croissant Task Format discussions](https://docs.google.com/document/d/1cQ2nQvP4WXyd2AaOmVZoO_URn7whv09PWeLeScrFzEQ/edit?usp=sharing). The files in this repository are still works in progress.

# Assumptions
The files were written assuming **separate files** for the [Croissant Task Problem](./dicom2nifti-taskproblem.md) and [Croissant Task Solution](./dicom2nifti-tasksolution.md). This choice was made thinking of a practical use case scenario. Someone can define a Croissant Task Problem and share it with a large community, from which other users can run the data processing task and generate their own Croissant Task Problem solutions. Data from the Solutions should conform to the specification of the Croissant Task Problem, even though each Solution will have distinct data.

# Notes and Questions
Each one of the Task [Problem](./dicom2nifti-taskproblem.md) and [Solution](./dicom2nifti-tasksolution.md) files includes some notes regarding assumptions made when writing them, and questions that came up in the writing process.