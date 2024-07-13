# Episode-3
Episode 3: How Much Does an LLM Cost for My Company?

*Nowadays, every company is looking to include Generative AI in their daily operations, but it is often unclear how much it will cost them. In this episode, we will break down these costs for you. We will assume that a company wants to implement a chatbot with 2 users that answers questions based on specific company data.*

# Introduction

The CEO of Company XYZ is requesting a chatbot that uses sales documents to answer questions such as: "Where does the customer who bought items today live?" or "How many purchase orders were made today for each item?" It seems obvious that a dashboard would be a significantly better option, but the CEO envisions that customers will interact with this chatbot in the future to track their own orders without the need for the current call center department. The data involved includes purchase orders in the form of PDFs. What are we going to do? We are going to explain parts of our architecture such as Amazon Lambda, Amazon RDS, Amazon BedRock, and Amazon Sagemaker, resulting in the total cost of an LLM application.

## LLM Architecture Application
![image](https://github.com/user-attachments/assets/9fbbd370-81ba-4298-be25-a207dfd73be4)
1. We are using Amazon S3 bucket to upload all the pdf files that exist. The current process is fully manually so each POs would be upload by the sales department.
2. Using the LangChain framework to extract and pre-process data from the S3.
3. We are using the Pre-Trained Sentence Tranformer Model for text embedding from Hugging Face (Open Source) 'all-MiniLM-L6-v2'.
4. For DBS we are using an Amazon RDS Postgres with pgvector.
5. The function of our second lambda is to retrieve information from de vector database using a vector embedding technique to extract the relation between the question and LLaMa-2-7B.
6. The function of Amazon Bedrock is to store Foundation Model LLaMa-2 with 7 billion parameter.
7. The user represent the question and the response that he is receiving, it coul be and application.

