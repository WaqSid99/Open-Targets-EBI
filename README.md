# Open-Targets-EBI
Parse a large dataset from EBI Open Targets to perform ETL


In this readme file I will describe my understanding of the task, assumptions made, explain the steps I took, and problem faced along with future improvements 

## Understanding of the task

In this task, I was required to perform ETL (Extract-Transform-Load) on a large json dataset. 

The “extract” step of the process required downloading EVA datasets along with the diseases and targets dataset. The EVA dataset contained json format data with each json object containing details of a target-disease pair. For this task, ‘score’ field was required which descried the strength between the target and disease. 

The “transform” step involved extracting the required fields from the main dataset, perform statistical operations required and returning at a table with required fields

The “transform” step involved converting the table into json format and exporting it.

For this assignment, the ETL performed was on a relatively small scale and it gave me an understanding of what actual process might look like.

## Assumptions made 
