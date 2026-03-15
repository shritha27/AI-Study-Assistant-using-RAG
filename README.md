# AI Study Assistant (RAG-Based Question Answering System)

## 1. Problem Statement

Students often deal with large volumes of study material such as lecture notes, textbooks, and documentation. Finding specific information quickly can be difficult and time-consuming. Traditional keyword search methods are not always effective because they rely on exact word matching rather than understanding the meaning of the query.
The goal of this project is to build an **AI-powered study assistant** that can answer questions directly from provided study materials. The assistant should retrieve relevant information from the document and generate answers based on the retrieved context.
This project implements a **Retrieval-Augmented Question Answering system** that allows users to ask natural language questions and receive answers derived from their study notes.



## 2. System Architecture

The AI Study Assistant works by combining semantic search with a question answering model.
The system performs the following tasks:
1. Load study material from a text file.
2. Split the text into smaller chunks for better processing.
3. Convert text chunks into vector embeddings.
4. Store the embeddings in a FAISS vector database.
5. Accept a question from the user.
6. Retrieve the most relevant chunks using similarity search.
7. Pass the retrieved context and the question to a QA model.
8. Return the extracted answer to the user.

The system follows a **Retrieval-Augmented Generation (RAG)** pipeline:<br>

User Question <br>
↓ <br>
Similarity Search (FAISS) <br>
↓ <br>
Retrieve Relevant Text Chunks <br>
↓ <br>
Provide Context + Question to QA Model <br>
↓ <br>
Generate Answer



## 3. Embedding and Retrieval Approach

### Embedding
The system converts text chunks into vector representations using a sentence embedding model. These embeddings capture the semantic meaning of the text rather than just keywords.

Embedding allows the system to understand queries like:
"What is machine learning?"

and retrieve relevant content even if the document contains slightly different wording.

### Vector Database
The embeddings are stored using **FAISS (Facebook AI Similarity Search)**. FAISS enables efficient similarity search over large vector datasets.

### Retrieval Process
When a user asks a question:
1. The question is converted into an embedding vector.
2. FAISS compares the query embedding with stored document embeddings.
3. The system retrieves the top-k most similar chunks.
4. These chunks are used as context for answering the question.

This ensures the model only processes relevant information.



## 4. Prompt Design

The QA model receives two inputs:
1. The **user's question**
2. The **retrieved context**

Example prompt:

Question:
What is machine learning?

Context:
Machine learning is a branch of artificial intelligence that enables systems to learn patterns from data without explicit programming.

Answer:
Machine learning is a branch of artificial intelligence that enables systems to learn patterns from data and improve performance without being explicitly programmed.

In this model, the prompt consists of the user’s question and the retrieved document context. The QA model processes both inputs and extracts the answer from the provided context, ensuring the response is grounded in the study material.The prompt is designed to ensure that the model generates answers **only from the provided context**, preventing hallucinations.



## 5. Example Failure Case

Failure Case:
If the user asks a particular question that does not match with loaded dataset, then the model may generate incorrect or incomplete answers.

Example Question:
"What are the types of neural networks?"

Problem:
If the dataset does not include detailed information about neural networks, the retriever may return unrelated chunks.

Result:
The QA model may produce an incomplete or vague answer.

Reason:
The system relies heavily on the **quality of retrieved context**. If relevant content is not retrieved, the model cannot produce accurate answers.



## 6. Reflection

This project demonstrates the implementation of a **basic Retrieval-Augmented Question Answering system** using modern NLP tools. 

Key learnings from this project include:

- Understanding how embeddings represent semantic meaning  
- Learning how vector databases enable fast similarity search  
- Implementing a simple RAG pipeline  
- Combining retrieval systems with transformer-based models






