<h1 align="center">AWS Project 1</h1>


# Project Description: Implementation and Analysis of Animal Control Data
* This project will include establishing a full-fledged data solution architecture leveraging AWS services to the rate of animals Lost in the year 2024 and include the feature of an Average count of Lost animals apart from the existing architectural support.

## Project Title: AWS Data Analytic Platform for the City of Vancouver - Part 1
* The project was to build an enduring apparatus that could efficiently store, clean, transform data, as well as source for the same. It keeps high standards of data security and management in the large datasets, despite maintaining a high level of flexibility, scalability. It also affords real-time analytical results through its enhanced graphical illustration tools.
## Project Objective:
* To calculate the rate of animals lost in the year 2024 using the "Animal Inventory Lost and Found" dataset from the City of Vancouver’s open data portal. Additionally, a new feature has been incorporated to support and enhance the analysis.
* Data Sourse : The data is sourced from external datasets. For example, the dataset for animal control inventory lost and found is accessed via an open data portal. This involves identifying and accessing relevant datasets that will be used for analysis.
![Screenshot (46)](https://github.com/user-attachments/assets/832d41ce-08ab-4401-8094-a26619606ccd)





  
## Methodology:
* The process of DAP designing and implementation is as follows.
### 1. Data Ingestion
Key analytical questions driving the project include:
- 1.	What is the rate of animals found Lost in the year 2024 and add an Average for count of Lost animals feature additionally to support your analysis.
- First we need to create a bucket in S3 and put the raw data inside it which we get from City of Vancouver.
![Screenshot (93)](https://github.com/user-attachments/assets/2cd6ca71-6e1f-4de6-8c2a-b62b818b8fe9)



- Raw, transformed and curated Data have been created in a new bucket in Aws at respective folder locations. Now let us push the dataset into the raw folder generated on the bucket described earlier.
![Screenshot (94)](https://github.com/user-attachments/assets/e244320b-af6a-414b-b380-713fe48dcf5a)
- Figure 3
![Screenshot (95)](https://github.com/user-attachments/assets/5dda5694-8004-412e-a73b-cf80f050f3b7)







### 2. Data Profiling
Shown below is the data profiling and cleaning which we perform to store the new transformed data in the new transformed bucket
![Screenshot (100)](https://github.com/user-attachments/assets/d73598cd-7547-4f5e-8479-cf92aa214784)




After ingestion we are going to focus on data profiling which will indicate to the summary of our data set any missing value or any relation that we can explore. To accomplish this first it will be necessary to develop a new transform bucket for all of this information. Then we have to navigate to AWS Glue Data brew, there we will have to create a new dataset wherein the data profiling will be run to get all the profiling data required for cleaning the data. 
![Screenshot (102)](https://github.com/user-attachments/assets/22d9f9b1-ab05-4189-8161-8f51c4eb2fb9)

- Result of profiling from the dataset

![Screenshot (103)](https://github.com/user-attachments/assets/9072be27-6191-4bce-a4d0-22eeda933407)



### 3. Data Cleaning
- When we complete doing the profiling there are certain irregularities we have to correct and can easily discern from the results of profiling.
 We make a project from the dataset and in this project all type of rules of data cleaning should be applied to make out data and to generate a new recipe.
![Screenshot (104)](https://github.com/user-attachments/assets/df42c33b-6993-4113-b65a-5bb6da65001a)



After creating a recipe for your data you need to create a job and run it.
Inside the job you need to specify the type of output and where to store it.
We use 2 types of output one is for user in a csv format which is user friendly and second is in Parquet format which is system friendly.

![Screenshot (105)](https://github.com/user-attachments/assets/0a7cc76c-95e8-49f2-b56f-e3119abd5f2e)



Cleaned system data
![Screenshot (136)](https://github.com/user-attachments/assets/626c41a2-7c1a-40d4-8f27-ee49b3589eda)


New cleaned data for user folders

![Screenshot (138)](https://github.com/user-attachments/assets/e3dd039e-36c9-4972-9e65-1e44e35566cb)



### 4. Data Pipeline Design
- AWS Glue is used to create the data pipeline, automating the ETL process.
- Finally, after carrying out the data profiling and data cleaning steps; we have our final transformed data which have no null or invalid value in it. Now we are ready in the next step of our descriptive analysis part where our task first is to find out in percentage how many Animals are lost and secondly to look them individually on the basis of type.
Count of Animals Lost = (Lost_count/right_Total_state_count)*100
We find that it is necessary to obtain the percentage of count of animals lost. Now let it be our turn to design our Day 2 ETL pipeline to help answer this question.
- Draw.io diagram for the whole process until the ETL pipeline implementation

![Screenshot (168)](https://github.com/user-attachments/assets/8dc1ad07-0af5-46c5-8f8d-818c223de1a4)



* Now we need to go to AWS Glue and start building our visual ETL pipeline
1.	Extract the parking tickets data from cleaned data folder in S3 bucket.
2.	Transformed the schema of the table by Dropping Extra Column from the table.
3.	Then we have divided the pipeline in 2 parts: one with the filtered data & another  one with total data.
4.	Then we put a filter transformation in which we filter out the count of animals that were lost
5.	Then we transform it by aggregating the Lost animals and then grouping it by the area of missing.
6.	Then we rename the aggregated column as “Lost_Count” to make it more suitable for our analysis.
7.	On the other hand we aggregate the total number of animals lost and found.
8.	Then we rename the aggregate column as “Total_State_Count” to make it more suitable for our analysis.
9.	Then we again rename the join key by adding the right_ as a prefix before joining.
10.	Then we merge the data sets as an outer join to include all the cells.
11.	Then we transform the data to calculate the % of count of animals lost count (Lost_Count / Total_State_Count)* 100.
12.	Now we load the data for separate types one for user in csv format and one for system in Parquet format.
13.	Then we save and run the pipeline.

- The data pipeline is designed to facilitate the smooth flow and transformation of data throughout the system.

![Screenshot (169)](https://github.com/user-attachments/assets/0f786cba-05a4-4bc8-ba40-70ca6750235f)


- The job for storing the ETL pipeline result

![Screenshot (170)](https://github.com/user-attachments/assets/e3a40110-ab14-49aa-9aa5-93b56e051e32)



### 5. Exploratory Analysis
- In the exploratory analysis we are calculating the average of Count of animals that were found Lost.
Let’s go through the steps for the exploratory analysis.
- Step 1: Data Ingestion
Same as the one we did above for descriptive analysis.
- Step 2: Data Profiling
Same as descriptive analysis
- Step 3: Data Cleaning
This step is like what we did for out descriptive analysis.
- Step 4: Data Pipeline Design
So after doing data profiling and data cleaning the final transformed data which is cleaned does not contain any null or invalid values. Now we can go to our descriptive analysis part where we have to know how many parking tickets have been committed and also individually based on their types.
Average =(Lost_count/Total_Animal_Count)/ 2
Now we need to create the alterations for our ETL pipeline to answer this question.
- Draw.io diagram for the whole process until the ETL pipeline implementation

![Screenshot (171)](https://github.com/user-attachments/assets/a608587a-92b0-49f1-aa5d-f8e3635200c5)



- The average we got after running the pipeline is 0.5
Below is the ETL Visual Pipeline:
- Second ETL pipeline implementation

![Screenshot (172)](https://github.com/user-attachments/assets/1c9a3445-2ab8-4cd5-a031-79310a95a8ab)


- Second job for storing the ETL pipeline result

![Screenshot (173)](https://github.com/user-attachments/assets/b36cba74-38a1-42ef-8c32-2725c9375b1a)

- Result: The calculated average of animal loss counts relative to the total inventory was 0.5
### Conclusion
- The project successfully implemented descriptive and exploratory analyses using AWS services, including S3, Glue DataBrew, and Glue ETL pipelines. The calculations provide insights into the rate of animal losses and facilitate further datadriven decisionmaking for animal inventory management.

### DAP Estimated Cost
-The AWS Pricing Calculator gives an accurate estimate of cost of a number of AWS services out of the many available. Or if you want to observe a scenario for a single user the cost computed for a monthly operation is approximately $1.43
![Screenshot (78)](https://github.com/user-attachments/assets/0d4a4185-f850-444c-9eba-bad042fa78b7)










