# Stockbase
Developed a Retrieval-Augmented Generation (RAG)-based chatbot leveraging AWS services to deliver document-specific, context-aware responses for enterprise knowledge bases, customer support, and research assistance.
![RAG Chatbot Context-Aware Document Retrieval and Response System](https://github.com/user-attachments/assets/76686827-6849-49d1-86db-736f11147990)

Report 
Introduction
In today's world of Generative AI (GenAI), there is a growing need for smarter chatbots that can provide more accurate and context-aware answers. People expect chatbots to not just understand their questions but to give precise answers tailored to their specific needs.
Retrieval-Augmented Generation (RAG) is a powerful solution that makes chatbots smarter. It combines two technologies:
1.	Retrieval: Finds and uses information from specific documents or knowledge bases.
2.	Generative AI: Uses advanced AI models to create accurate responses.
RAG helps chatbots answer questions based on specific documents, like company rules or user manuals, without the need to retrain or fine-tune the AI model. This makes responses highly accurate and relevant, which is perfect for businesses that need reliable chatbots.
This project is about a RAG-based chatbot that uses several AWS tools to deliver fast, accurate, and document-specific answers. The system uses services like:
•	AWS Amplify: For the web interface where users interact with the chatbot.
•	AWS Lambda: To handle tasks like processing queries and creating embeddings (a way to store information).
•	DynamoDB: To store document data and embeddings.
•	OpenSearch: To find the most relevant document data for a user’s query.
•	Bedrock: A service that generates responses based on the retrieved data.
The chatbot is designed to be easy to use, scalable (can handle growing users), and efficient, making it a great solution for businesses needing intelligent chatbots.

1. Architecture Diagram
Below is the architecture diagram for the chatbot, showcasing the interaction between services:
![image](https://github.com/user-attachments/assets/f578d68a-9a70-4c27-86a1-c1fe2202b0c5)

 
Description:
•	Frontend: AWS Amplify is used for hosting and deploying the frontend web interface, allowing users to interact with the chatbot.
•	API Gateway: Acts as a POST gateway to facilitate communication between the frontend and backend.
•	Lambda Functions:
o	Vector Database: Converts documents stored in S3 into vector embeddings using the amazon.titan-embed-text-v1 model from AWS Bedrock.
o	RAG Chatbot: Handles user queries, retrieves context from DynamoDB, and communicates with the Claude v2 LLM model in Bedrock to generate responses.
•	DynamoDB: Stores vector embeddings along with the original text in a KnowledgeBase table.
•	OpenSearch: Retrieves relevant embeddings based on the user’s query for similarity search.
•	AWS Bedrock (Claude v2): Uses retrieved embeddings and user queries to generate contextual answers.
•	AWS CloudWatch: Monitors and logs activity for debugging and performance tracking.


3.	Estimation of the Cost
 ![image](https://github.com/user-attachments/assets/205c479f-205d-443a-996c-d0dc2ca142de)

The total estimated cost for deploying the RAG-based chatbot using AWS services is $513.12 for a 12-month period. This includes an upfront cost of $180 and a monthly recurring cost of approximately $27.76. The main contributors to the cost are DynamoDB provisioned capacity, which accounts for the upfront cost and a monthly charge of $27.39, and Titan Lite (Bedrock), which costs $0.35 per month, totaling $4.20 annually. Other services like S3 Standard storage incur minimal costs of $0.02 per month, amounting to $0.24 annually, while services such as AWS Lambda, API Gateway, and AWS Amplify are estimated to have no charges under the specified configuration. These estimates are based on the AWS Pricing Calculator and do not include taxes. Actual costs may vary depending on usage patterns and additional configurations.

4. Deployment Process
The RAG chatbot is designed to use information from specific documents stored in an S3 bucket. Here’s how it works in simple terms:
1.	Preparing the Documents:
o	Documents are uploaded to an S3 bucket.
o	A Lambda function (called "vectordatabase") processes these documents and turns them into "vector embeddings."
o	These embeddings (a way to store document data for easy searching) are saved in a DynamoDB table along with the original text.
2.	Searching for Relevant Information:
o	DynamoDB holds all the data, but to find the most relevant information for a user’s question, AWS OpenSearch is used.
o	OpenSearch compares the user’s question with the embeddings to find the best match.
3.	Generating an Answer:
o	Once the right information is found, it is sent to AWS Bedrock along with the user’s question.
o	Bedrock uses the Claude AI model to create an answer based on the user’s question and the matching document.
4.	User Interaction:
o	The chatbot’s web interface is hosted on AWS Amplify, where users can type their questions.
o	API Gateway sends these questions to a Lambda function that handles the entire process of searching, processing, and generating a response.
o	The chatbot then gives the answer back to the user.
Step-by-Step Flow:
1.	A user enters a question on the chatbot’s webpage.
2.	The question is sent to a Lambda function through API Gateway.
3.	The question and the matching document context are sent to Bedrock for processing.
4.	Bedrock uses Claude AI to generate an answer based on the document.
5.	The answer is sent back to the user.
This design ensures that the chatbot answers are accurate and based only on the provided documents, making it highly reliable for specific tasks.

The following images shows the deployment of the website and the webpage:
 
 

5. Functionality of the Web Application
Features:
1.	Document Integration:
o	Users can upload documents to an S3 bucket.
o	These documents are converted into vector embeddings and stored in DynamoDB for easy searching.
2.	Smart Querying:
o	Users ask questions through a web app hosted on AWS Amplify.
o	The chatbot uses OpenSearch to find the most relevant information from the uploaded documents.
3.	Contextual Responses:
o	AWS Bedrock, with the Claude v2 model, generates responses based on the document content instead of general AI knowledge.
4.	Fast Performance:
o	API Gateway ensures smooth and quick communication between the frontend and backend.
________________________________________
User Flow:
1.	The user types a question into the web app.
2.	The question is sent to the RAGChatbot Lambda function via API Gateway.
3.	The Lambda function retrieves related information from DynamoDB using OpenSearch.
4.	Claude v2 in AWS Bedrock creates a response based on the retrieved information and the user’s question.
5.	The chatbot returns the response to the user through the web app.
________________________________________
Use Case Examples:
•	Enterprise Knowledge Base: Automatically answer questions about company documents or policies.
•	Customer Support: Provide personalized and accurate answers for customers using specific product manuals or guides.
•	Research Assistance: Quickly find and retrieve relevant details from large data sets or reports.
This makes the web app highly effective for answering questions based on specific documents in real-time.

