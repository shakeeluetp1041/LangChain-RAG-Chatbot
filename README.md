# YouTube Video RAG Chatbot

A Retrieval-Augmented Generation (RAG) chatbot that answers questions about YouTube videos using their transcripts.

##  How It Works

    YouTube Video
          ↓
    Load Transcript
          ↓
    Text Splitting
          ↓
    Embeddings
          ↓
    FAISS Vector Store
          ↓
    User Question
          ↓
    Similarity Search
          ↓
    Relevant Documents
          ↓
    Prompt + Context
          ↓
    Qwen 2.5 LLM
          ↓
    Answer

##  Tech Stack

- Python
- LangChain
- Hugging Face
- Qwen/Qwen2.5-7B-Instruct
- FAISS
- YouTube Transcripts
- RAG

##  LangChain Pipeline

    parallel_chain = RunnableParallel({
        "context": retriever | RunnableLambda(format_docs),
        "question": RunnablePassthrough()
    })

    main_chain = parallel_chain | prompt | model | parser

The system retrieves the most relevant transcript chunks, adds them to the prompt, and sends the context with the user's question to the LLM.

##  Model

    repo_id = "Qwen/Qwen2.5-7B-Instruct"
    task = "text-generation"
    provider = "featherless-ai"

The model is accessed through Hugging Face and converted into a LangChain chat model using `ChatHuggingFace`.

##  Installation

    git clone <repository-url>
    cd <project-folder>

    pip install -r requirements.txt

Create a `.env` file:

    HUGGINGFACEHUB_API_TOKEN=put_the_API_token_here

## Usage

After setting up the transcript, vector store, retriever, prompt, and model:

    main_chain.invoke("Can you summarize the video?")

You can also ask questions such as:

- What is the main topic of the video?
- Explain the key points.
- What did the speaker say about X?
- Give me a short summary.

##  Project Structure

    Langchain_models/
    ├── YoutubeRAGChatbot.py
    ├── requirements.txt
    ├── .env(Add this fileand add API token)
    └── README.md

##  Features

- YouTube transcript-based question answering
- Semantic similarity search
- FAISS vector database
- Hugging Face LLM integration
- LangChain RAG pipeline
- Context-aware answers



##  Conclusion

This project demonstrates how LangChain, FAISS, embeddings, and Hugging Face LLMs can be combined to build a practical YouTube Video RAG chatbot.