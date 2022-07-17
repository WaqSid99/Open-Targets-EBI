# Open-Targets-EBI
Parse a large dataset from EBI Open Targets to perform ETL


In this readme file I will describe my understanding of the task, assumptions made, problem faced and future improvements 

## Understanding of the task

In this task, I was required to perform ETL (Extract-Transform-Load) on a large json dataset. 

The “extract” step of the process required downloading EVA datasets along with the diseases and targets dataset. The EVA dataset contained json format data with each json object containing details of a target-disease pair. For this task, ‘score’ field was required which descried the strength between the target and disease. 

The “transform” step involved extracting the required fields from the main dataset, perform statistical operations required and returning a table with required fields

The “transform” step involved converting the table into json format and exporting it.

For this assignment, the ETL performed was on a relatively small scale and it gave me an understanding of what the actual process might look like.

## Assumptions made 

1-	In the `evidence/sourceId=eva/` directory there were 200 datasets available all with same format, so I was not sure whether to perform the task on a single dataset or combine and work on them all together. So, I assumed to work on a single dataset, but the given operation can apply to rest of the other datasets as from my observation they all have the same format


## Problems Faced

The only issue I faced was when I tried to download the diseases and targets datasets, the ftp server wouldn’t connect and returned a “ConnectResetError Connection reset by peer”. I tried finding a solution online, but I couldn’t get any help. When I started working on this assignment, I only downloaded the eva dataset and one dataset from disease and target directory each. But later I realised that to “add the `target.approvedSymbol` and `disease.name` fields to the table”, I needed to download the entire disease and target directory (this is my understanding I could be wrong). On the final day, I tried multiple time to reconnect, but it won’t work for some reason. For this reason I was not able to add the fields. Below I describe how I would have approached this step:
1.	Download all disease and target dataset in separate folders
2.	Combine all disease json files into one
3.	Repeat step 2 for target json files
4.	Import disease json file into pandas dataframe table and extract only diseaseId and name
5.	Import target json file into pandas dataframe table and extract only targetId and approved.symbol
6.	Apply pandas dataframe merge function on the main dataframe and disease dataframe: main_df.merge(disease_df,on=’diseaseId’). This would add the disease id and name for only those diseases found in the main dataframe
7.	Repeat step 6 for target dataset: main_df.merge(target_df,on=’targetId’)


## Future Improvement 

While I believe my code does the work, I do feel there is much room for improvement. 

The transform function which finds the target:disease pair takes O(n2) worst case runtime and can be time consuming when working with large dataset. I tried various methods like using hashmaps, graphs to reduce runtime but couldn’t figure anything. I also looked into using pandas merge function somehow to find pairs but that didn’t work either. My implementation is reliant on pandas dataframe so maybe a different implementation method would result in better efficiency. I would be interested to know about it.

I could have used multiprocessing to make the process faster especially considering the large size of the evidence eva dataset. Unfortunately, I don’t have much experience working with multiprocessing/threading in python so I didn’t attempt that, but I can definitely see its application for this task.

Although while working on this assignment I ran some manual tests on side, I believe I could have added some standard python test cases. I understand testing is a crucial part of software development cycle, but I was unable to do so due to lack of time.



![image](https://user-images.githubusercontent.com/60627299/179427437-6e7ec7e3-d4c1-437f-a391-aea836f60548.png)
