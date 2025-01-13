# SportDatalake

This project is about automating the creation of a data lake for NBAanalytics using AWS services. It includes the set up of the infrastructure needed to store and query NBA-related data. 

## AWS Services used 
- Amazon S3: object storage service that offers industry-leading scalability, data availability, security, and performance. Customers of all sizes and industries can use Amazon S3 to store and protect any amount of data for a range of use cases, such as data lakes, websites, mobile applications, backup and restore, archive, enterprise applications, IoT devices, and big data analytics.  
In this project, it is used as a data lake to store the retreived NBA data (JSON format)
- AWS  Glue:  a serverless data integration service that makes data preparation simpler, faster, and cheaper. You can discover and connect to over 100 diverse data sources, manage your data in a centralized data catalog, and visually create, run, and monitor ETL pipelines to load data into your data lakes.  
In this project, it is used to retreive unprocessed data from the S3 bucket and prepare it in a schema to make it available for analytics by Athena service. 
- Amazon Athena: an interactive query service that is capable of seamlessly using standard Structured Query Language (SQL) to analyze data.
In this project, it is used for SQL quering on the Glue data catalog directly in S3 enabling analytics.

## Prerequisites
- AWS credentials : generate AWS credentials with the right permissions to run the script (S3: s3:CreateBucket, s3:PutObject, s3:DeleteBucket, s3:ListBucket Glue: glue:CreateDatabase, glue:CreateTable, glue:DeleteDatabase, glue:DeleteTable Athena: athena:StartQueryExecution, athena:GetQueryResults)
- Generate for free an NBA API Key from SportsDataIO API (https://sportsdata.io/cart/free-trial)

## Architecture 
![image](https://github.com/user-attachments/assets/61c3abfe-a017-480f-b847-9319aa6270c0)



## Setting up the environment
In the .env file, define environment variables to store your sensitive data:  
&nbsp;&nbsp;&nbsp;&nbsp; SPORTS_DATA_API_KEY=your_sportsdata_api_key  
&nbsp;&nbsp;&nbsp;&nbsp; NBA_ENDPOINT=https://api.sportsdata.io/v3/nba/scores/json/Players  

Add the ".env" to your .gitignore file. 

## Running the script 
In the CLI , type : 
```
python3 setup_nba_data_lake.py
```
## Use AWS CLI and Cloudshell 
Check that all resources have been created successfully :   
- Run Cloudshell from the console  
- To list the s3 bucket created and view its content:  
        'aws s3 ls s3://your_bucket_name' 
- To check the created Glue Table in the database :     
        'aws glue get-tables --database-name your_glue_database_name'

## Results: 

On the console, go to S3 and you will find the Athena's results under the Output location folder defined in the Script:   
![image-2](https://github.com/user-attachments/assets/d4091d79-a6b8-44eb-b165-c64c15b3d71d)

![image-3](https://github.com/user-attachments/assets/c2b3e77a-d1af-4244-9f68-cb3a4790f7d9)

![image-4](https://github.com/user-attachments/assets/a2e68e3b-49e1-49fa-85bd-4219f0e7885d)


## Destroy the platform 
To avoid any billing surprises, don't forget to destroy the created infrastructure.   
Run  the delete_aws_resources script for this purpose:   
```
python3 delete_aws_resources.py
```

## Future Enhancements
Automate data ingestion with AWS Lambda  
Implement a data transformation layer with AWS Glue ETL  
Add advanced analytics and visualizations (AWS QuickSight)  








