# llama_7b_pdf
This is reference from multiple file and code, other updated version have high computation. So, have to stop with it.

The only drawback is the token size is small so small pdf can only be processed.


### High-Level Documentation

This code defines a **Streamlit application** for interacting with PDF documents through a conversational AI model. Using `langchain`, `FAISS`, and `streamlit_chat`, it enables the app to handle user-uploaded PDFs, create embeddings for document data, and generate conversational responses to user queries about the content.

---

#### 1. **Dependencies and Imports**
   - **Streamlit (`st`)**: Used for creating the web-based UI components.
   - **Langchain**:
      - `PyMuPDFLoader`: Loads PDF files and processes them into data.
      - `HuggingFaceEmbeddings`: Generates embeddings for document data using the Hugging Face `sentence-transformers/all-MiniLM-L6-v2` model.
      - `FAISS`: An efficient library for creating vector databases.
      - `ConversationalRetrievalChain`: Builds a conversational chain for retrieval-based Q&A.
   - **Loadllm**: A custom module to load the language model.
   - **Streamlit Chat (`message`)**: Manages and displays chat history.

#### 2. **FileIngestor Class**
   The main class `FileIngestor` encapsulates PDF processing, embedding creation, conversational chain setup, and handling user queries.

   - **Initialization (`__init__`)**:
      - Takes an `uploaded_file` (PDF file) as input.
   
   - **File Processing and Ingestion (`handlefileandingest`)**:
      - **Temporary File Creation**: The uploaded PDF is temporarily stored using Python’s `tempfile` module.
      - **Document Loading**: The PDF is loaded and parsed into a document structure using `PyMuPDFLoader`.
      - **Embedding Creation**: Embeddings are generated for document data using a pre-trained Hugging Face transformer model.
      - **Vector Store Initialization**: The embeddings are stored in a FAISS vector store, which is saved locally for future retrieval.
   
   - **Language Model and Conversational Chain**:
      - **Load Language Model**: A language model is loaded using `Loadllm`.
      - **Conversational Chain**: A retrieval-based conversational chain is created to handle interactive Q&A on the document data.
      - **Conversational Chat (`conversational_chat`)**:
         - Takes a `query` and retrieves a response based on the context of the document.
         - Updates `st.session_state` with query history to maintain conversation flow.

#### 3. **Streamlit Interface**
   - **Chat History Initialization**:
      - `st.session_state` variables (`history`, `generated`, `past`) manage chat state across user interactions.
   
   - **Chat Containers**:
      - **Response Container**: Displays the AI-generated responses.
      - **User Input Container**: Houses the form where users input their questions.

   - **Chat Interface (`st.form` and Display)**:
      - A form is used for user input, allowing queries to be submitted.
      - Once the query is processed, both the user’s input and the AI’s response are added to the chat history, providing a continuous conversation experience.
   
   - **Chat Display**:
      - Iterates through `st.session_state` to render each exchange as a message bubble, creating a familiar chat-like interface.

#### 4. **Session State Management**
   - Streamlit’s `st.session_state` is used extensively to maintain chat history across different query submissions.
   - This allows the chat interface to persist the conversation context, making the experience interactive and conversationally cohesive.

---

### Summary
This code enables users to interact with PDF documents in a conversational manner, leveraging embeddings and a retrieval-based language model chain. It provides a user-friendly chat interface, managed entirely in Streamlit, which allows for smooth Q&A over uploaded PDF content.


Download model from : https://huggingface.co/TheBloke/Llama-2-7B-Chat-GGUF/tree/main

Run :  streamlit run app.py

![Screenshot (67)](https://github.com/Anshuldogra001/llama_7b_pdf/assets/96309140/78d2904a-0039-4168-8863-bbe443fde313)
