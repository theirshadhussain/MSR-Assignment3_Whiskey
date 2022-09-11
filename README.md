# Identifying-GitHub-Expertise-Using-NLP
## Note: 
This is a reproduction project as part of the MSR course 2022 at UniKo, CS department, SoftLang Team

## Name of the team: 
Whiskey

## Student names: 
- Aneesa Sulthana Jagaraspalli
- Irshad Hussain Mohammed
- Pavan Kumar Tokachichu

## Objective of Reproduction

### Description : 
Training Microsoft LUIS with utterances of different technologies using NLP and  testing the acquired code chunks from github repositories  on the trained LUIS to find Precision, Recall and F-measure.

### Input data:  
Used GitHub REST API version 3, [REST API GITHUB](https://developer.github.com/v3/) to fetch input data(commit data) for testing LUIS 

Paper Code Repo: https://github.com/melkor54248/RepoSkillMiner

Our Git Project: https://github.com/theirshadhussain/Identifying-GitHub-Expertise-Using-NLP

### Output data: 
Evaluate Precision, Recall and F-measures for the derived technologies, by conducting a test in LUIS and reporting the results.

The [Excel](https://github.com/theirshadhussain/Identifying-GitHub-Expertise-Using-NLP/blob/master/Data/metrics_for_Testingdata_LUIS.xlsx) file contains calculated metrics on the results obtained.
## Findings of reproduction

### Process delta:
Our reproduction process differs from the process followed in the paper in the following ways:
- The first part of this paper is to identify programming language of commit files. We have directly considered files in Python Language as no metrics were provided in the paper to validate.
- While training and testing LUIS, we have used SQL and Pyspark whereas in the paper they have used Linq, Entity Framework, Async Programming, Angular, and React. This is because we wanted to compare the precision, recall, and F-measure values for different technologies and validate this part of the paper.
- We have used the single testing panel instead of the batch testing panel. This is because we wanted to check the individual lines of code where we get high intent score and analyze them.

### Output delta :
Our output metrics are a little different (for SQL) from the output of the paper. In the case of Pyspark, the output metrics (precision, recall, and F-measure) are very similar to the ones in the paper. In the case of SQL, the difference in precision values is quite low whereas the difference in recall and f-measure is significant. This might be because in the case of SQL we have got some False Negative cases i.e., SQL code was shown as Pyspark or none. This might be because of a little similarity in both the technologies’ code syntaxes. However, we can overcome this by broadening the training data. In the paper, just 98 example utterances have been created for 5 technologies. By this, we have analyzed that in the case of training technologies whose syntaxes are a bit different, training with a few utterances can work fine. But, in the case of training similar technologies together, we need to consider more example utterances.

## Implementation of Reproduction
### Hardware Requirements :
- x86 64-bit CPU (Intel / AMD architecture)
- 4 GB RAM
- 1 GB free Disk space

### Software Requirements :
- Windows 7 or 10
- Mac OS X 10.11 or higher, 64-bit
- Linux: RHEL 6/7, 64-bit (almost all libraries also work in Ubuntu)
- Browser to access Microsoft Azure (Chrome, Bing, Firefox, Safari)

### Validation :
The Technologies used by the authors produced more accurate results than the technologies chosen by us. We have chosen Pyspark and Sql to train LUIS and the reason to chose these two technologies is because these two technologies have a lot of similarities in their syntaxes. We wanted to check if the paper is biased with the technologies chosen by authors. As a result of our Reproduction, we found out that the metrics like Precision, Recall, F-measure were less for model differntiating SQL and Pyspark.This is because there were complex lines of code especially when provided by a Pyspark line of code internally having sql command.

### Data :

#### Input   : 
For our Reproduction we have assumed the programming language of the commit files is already known and the input to our LUIS model is fetched from these commit files. 

#### Output  : 
The outputs are the metric values calculated on the Identification done by the reproduced LUIS model.
