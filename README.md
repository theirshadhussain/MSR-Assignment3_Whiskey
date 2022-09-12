## Note: 
This is a MSR study as part of the MSR course 2022 at UniKo, CS department, SoftLang Team

## Name of the team: 
Whiskey

## Student names: 
- Aneesa Sulthana Jagaraspalli
- Irshad Hussain Mohammed
- Pavan Kumar Tokachichu

## Underlying paper:
DBLP - https://dblp.org/rec/conf/kbse/KourtzanidisCA20

## Reproduced baseline:
  
### Objective of Reproduction

#### Description : 
Training Microsoft LUIS with utterances of different technologies using NLP  with training datasets larger than in the paper and testing the acquired code chunks from github repositories  on the trained LUIS to find Precision, Recall and F-measure.

#### Input data:  
Used GitHub REST API version 3, [REST API GITHUB](https://developer.github.com/v3/) to fetch input data(commit data) for testing LUIS 

Paper Code Repo: https://github.com/melkor54248/RepoSkillMiner

Our Git Project: [https://github.com/theirshadhussain/MSR-Assignment3_Whiskey](https://github.com/theirshadhussain/MSR-Assignment3_Whiskey)

#### Output data: 
Evaluate Precision, Recall and F-measures for the derived technologies, by conducting a test in LUIS and reporting the results.

The [Excel file](https://github.com/theirshadhussain/MSR-Assignment3_Whiskey/blob/master/Data/metrics_for_Testingdata_LUIS.xlsx) contains calculated metrics on the results obtained.
  
#### Findings of reproduction

#### Process delta:
Our reproduction process differs from the one in paper because:
- While training and testing LUIS, we have used SQL and Pyspark whereas in the paper they have used Linq, Entity Framework, Async Programming, Angular, and React. This is because we wanted to compare the precision, recall, and F-measure values of identification for different technologies especially which have similar syntax.
- We have used the single testing panel instead of the batch testing panel. This is because we wanted to check the results for individual lines of code and analyze them.

#### Output delta :
Our output differs from what is described in the paper as the technologies we chose, produces less accuracy scores.
- Precision for pyspark is higher than for SQL (0.88, 0.64 respectively) 
- Recall for SQL is higher than for pyspark (1, 0.5 respectively)
- f-score for SQL is higher than for pyspark (0.78, 0.64 respectively). 

The metrics for classifying comments and other languages as 'none', also have less scores (precision = 0.42, recall = 0.36, f1 score = 0.39).
##### Note: The reasons for such low scores of the model overall are having similarities between syntaxes and the relevance of comments to the queries. The scores were low despite of increasing the size of training dataset.
Hence the the following Threats to Validity are evident by the results:
- 'Bias in identification of similar technologies from the commit files'
- 'Affect of the programming language present in the commit files on the identification of the technologies'

## MSR study enhancement:

- **Threat** — We have identified two threats to validity:
  - When the technologies being trained have similar syntax the metric scores can be low. 
  - Presence of programming language in the commit file can deviate the metric score of the intents.

- **Traces** — In the paper it is mentioned,
  
  - "We evaluate the precision, recall and f-measure for the derived technologies/frameworks, by conducting a batch test in LUIS and report the results". 
     
     It could be a threat while evaluating as not all repositories are unbiased. 
  - Also, "We have created 98 example utterances for the 5 intents using existing or slightly altered existing samples from the official Microsoft, Angular and React documentation".
     
     In the previous assignment, The Reproduction of paper using same amount of utterance for training resulted in low metric scores. So, having small number of utterances can be the reason

- **Theory** — We think these are threats because:
  -  Training technologies with different syntax may yield high metric values(as in the paper), but when trained with technologies with similar syntax the metric scores were low during the Reproduction of the paper (assignment 2). Hence there is a bias in the identification of technologies and thus the model can misclassify or produce less accurate results.
  -   We know that the commit files contain not just the technologies but also programming languages. The presence of programming languages in the commit files being tested can manipulate the results.

- **Methodology** — We plan to train model with  pyspark and sql repositories having lots of comments and test them in LUIS with code chunks of SQL, Pyspark, comments and also other programming languages (classify as 'none') to get precision, recall and f-score. This is to check if the threat still exists with the large training dataset.

- **Feasibility** — We would like to skip the part of showing the result in the software RepoSkillMiner as it might take more time to code an entire software and concentrate on evaluation of model trained in LUIS.

- **Process** —   We have trained LUIS not only with large utterances of SQL and Pyspark but also with alot of comments. After the training is done, we test using single panel testing instead of batch testing and calculate the precision, recall and f-score for the results. We used SQL, Pyspark to test the model. In addition to that we tested comments, other languages like Java, C, HTML, javascript etc., to check if the output is 'none' . After testing, analysis of results was done to dig the reasons for less scores.

- **Data** — We have trained LUIS with significantly large number (than authors) of  SQL, Pyspark and comments utterances. Apart from this, example codes from different languages were tested to be classified as 'none'.

- **Results** 
In the paper it is stated 'We have created 98 example utterances for the 5 intents using existing or slightly altered existing samples from the official Microsoft, Angular and React documentation'. 
  - They have used 98 utterances for 5 intents but we have used 270 example utterances for 2 intents (90 SQL, 90 for Pyspark,90 for 'none').
 Clearly we have used more utterances to train our intents than in the paper but still we have not got such high precision, recall and f-score metrics as in the paper. 

  This might be because there can be bias in case of some intents being trained together. If the syntax of the languages is  different the results can be accurate.   But in case of languages where the syntax are quite similar, the results are not so accurate. 
 
  Since we performed single test panel testing instead of batch testing like in the paper, we got to observe the lines of code where the result is not correct. 

##### i) SQL test with high metric scores

![SQL accurate results](https://user-images.githubusercontent.com/107684552/189632080-9dafe730-ac0d-418f-b8b0-a5cc21202794.png)

##### ii) Pyspark with less scores (small change in the variable results in 'none' instead of 'pyspark').

![pyspark variable name conflict](https://user-images.githubusercontent.com/107684552/189644420-f9cf87da-61dd-4126-b53c-4d7807126e21.png)

##### iii) Pyspark mostly misclassified as 'none'.

![pyspark none conflict](https://user-images.githubusercontent.com/107684552/189644455-4093e06b-969e-4cc6-8999-cf535ca16241.png)

##### iv) Misclassification of comments.

![comments conflict](https://user-images.githubusercontent.com/107684552/189645666-f23ae60e-039d-4ce4-9882-edc49cdbf8f2.png)

##### v) javascript, C, HTML, CSS, java etc., not classified as 'none' 

![other languages conflict](https://user-images.githubusercontent.com/107684552/189645596-0befc7f8-7084-4871-91bb-a5055b91a6cf.png)

![other languages conflict 1](https://user-images.githubusercontent.com/107684552/189645550-efaa742d-4566-4e36-b90a-70941ed208d9.png)

Hence we came to a conclusion that it is not possible to get such high metrics for all technologies using a small number of example utterances(98 utterances for 5 intents) as in the paper. There is a bias towards certain technologies whose syntax is unique.  
When the commit files (which contain not just the code for technology but also the programming language) are being tested to find out the technologies used, the result always can't be accurate as the model may not be able to classify it as 'none'.

## Implementation
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
- The Technologies used by the authors produced more accurate results than the technologies chosen by us. We have chosen Pyspark and Sql to train LUIS and the reason to choose these two technologies is because these two technologies have a lot of similarities in their syntaxes. We wanted to check if the paper is biased with the technologies chosen by authors. As a result of our Reproduction, we found out that the metrics like Precision, Recall, F-measure were less for model differentiating SQL and Pyspark.This is because there were complex lines of code especially when provided by a Pyspark line of code internally having sql command. 

- We have used single line testing instead of batch testing to check the lines of code individually to better analyze their result and why it has occured. 

- We have used codes of other languages to check if the result is 'none' or not. This is because the commit files contain code with different programming languages along with the technology. We wanted to check if this would affect the result of identifying the technologies as the model should classify other language 'none'.

### Data :

#### Input   : 
For our Reproduction we have assumed the programming language of the commit files is already known and the input to our LUIS model is fetched from these commit files. 

#### Output  : 
The outputs are the metric values calculated on the Identification done by the reproduced LUIS model.
