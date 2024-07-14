# Episode-3
Episode 3: How Much Does an LLM Cost for My Company?

*Nowadays, every company is looking to include Generative AI in their daily operations, but it is often unclear how much it will cost them. In this episode, we will break down these costs for you. We will assume that a company wants to implement a chatbot with 2 users that answers questions based on specific company data.*

# Introduction

The CEO of Company XYZ is requesting a chatbot that uses sales documents to answer questions such as: "Where does the customer who bought items today live?" or "How many purchase orders were made today for each item?" It seems obvious that a dashboard would be a significantly better option, but the CEO envisions that customers will interact with this chatbot in the future to track their own orders without the need for the current call center department. The data involved includes purchase orders in the form of PDFs. What are we going to do? We are going to explain parts of our architecture such as Amazon Lambda, Amazon RDS, Amazon BedRock, and Amazon Sagemaker, resulting in the total cost of an LLM application.

## LLM Architecture Application
![image](https://github.com/user-attachments/assets/9fbbd370-81ba-4298-be25-a207dfd73be4)
1. **Amazon S3 for PDF Uploads**: Our sales department manually uploads all purchase orders (POs) as PDF files to an Amazon S3 bucket.
2. **Data Extraction and Preprocessing with LangChain**: We utilize the LangChain framework to extract and preprocess data from the PDFs stored in S3.
3. **Text Embedding with Hugging Face Model**: We use the pre-trained 'all-MiniLM-L6-v2' Sentence Transformer model from Hugging Face to generate text embeddings.
4. **Database Storage with Amazon RDS Postgres**: Our database system is Amazon RDS Postgres, enhanced with the pgvector extension for storing and querying vector data.
5. **Lambda Function for Vector Database Retrieval**: A second Lambda function retrieves information from the vector database, leveraging vector embedding techniques to correlate the user’s question with the LLaMa-2-7B model.
6. **Foundation Model Storage with Amazon Bedrock**: We use Amazon Bedrock to store the LLaMa-2-7B foundation model, which has 7 billion parameters.
7. **User Interaction via Application**: The application interfaces with the user, allowing them to pose questions and receive responses generated through the system

## Architecture Cost
Please note that the architecture I describe is not only suitable for Company XYZ but also incorporates two of the most commonly used AI/ML services provided by AWS (Amazon Bedrock and Amazon Sagemaker). While this architecture can be optimized for cost and scalability, I strongly recommend conducting your own research before applying it to your project.

| Service    | Description | Dimension | 
| --------- | ------- | ------- |
| Amazon RDS| Amazon RDS include in May 2023 the use of that pgvector from Postgres. This database will allows us to stored and search embedding. | Instance: db.m3.medium, vCPU: 1, Memory: 3.75 GiB
Utilization: 100% of the Month
Storage Amount: 30GB
Hour Rate: 0.095 USD
Storage pricing (Monthly): 3.45
Monthly Cost for RDS Proxy (Monthly): 21.90
Amazon RDS PostgreSQL instances cost (Monthly): 69.35
Total Cost of Amazon RDS: 94.70|
|           |         |         |
|           |         |         |
|           |         |         |
|           |         |         |
|           |         |         |
|           |         |         |

## Reference

https://github.com/aws-samples/llm-apps-workshop/blob/main/blogs/rag/blog_post.md
https://medium.com/@abonia/deploying-a-rag-application-in-aws-lambda-using-docker-and-ecr-08e246a7c515
https://github.com/aws-samples/rds-postgresql-pgvector?tab=readme-ov-file
https://github.com/aws-samples/rag-with-amazon-bedrock-and-pgvector?tab=readme-ov-file
https://github.com/aws-samples/text-embeddings-pipeline-for-rag
https://community.aws/content/2bi5tqITxIperTzMsD3ohYbPIA4/easy-rag-with-amazon-bedrock-knowledge-base
https://python.langchain.com/v0.2/docs/integrations/llms/bedrock/
https://medium.com/@tahir.rauf/similarity-search-using-langchain-and-bedrock-4140b0ae9c58
