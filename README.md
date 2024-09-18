
# RAG PDF Q&A CLI Application

This project implements a Retrieval-Augmented Generation (RAG) model using a combination of document retrieval with TF-IDF and text generation with GPT-2 to answer questions based on content extracted from PDF files. It allows users to query the content of PDFs and receive AI-generated answers.

## Features

- **PDF Text Extraction**: Extract text from PDFs using the PyPDF2 library.
- **TF-IDF Based Document Retrieval**: Retrieve the most relevant sentences or paragraphs from the extracted content using the TF-IDF vectorizer.
- **GPT-2 Text Generation**: Generate answers to user questions by conditioning GPT-2 on the relevant document snippets.
- **Summarization**: Summarize the context before generating an answer to improve response quality.
- **Interactive CLI**: Users can input questions, and the application will respond with generated answers based on the PDF content.
- **Caching for Efficiency**: Queries are cached to avoid redundant computations.

## Requirements

- Python 3.7+
- Install the required dependencies by running:

```bash
pip install -r requirements.txt
```

### Dependencies:

- `transformers`: For the GPT-2 text generation and BART summarization.
- `scikit-learn`: For the TF-IDF vectorizer and cosine similarity calculations.
- `PyPDF2`: For extracting text from PDF files.
- `nltk`: For stopword removal and text preprocessing.

## Installation

1. Clone the repository:

```bash
git clone https://github.com/ayesh-merenchige/ChatWithPDF_RAGapp.git
cd ChatWithPDF_RAGapp
```

2. Install required libraries:

```bash
pip install -r requirements.txt
```

3. Download NLTK stopwords and wordnet data:

```bash
python -m nltk.downloader stopwords
python -m nltk.downloader wordnet
```

## Usage

### Preparing PDFs

- Place your PDF files in a `data/` folder, or update the PDF paths directly in the code.

### Running the Application

To start the application, simply run cells in Basic_RAG_app.ipynb file:

You will be prompted to enter a question based on the PDF content, and the model will provide an answer based on the most relevant information extracted from the PDFs.

### Example

```bash
Extracting text from data/data1.pdf...
Preprocessing text...
Initializing RAG model...

RAG model is ready. You can now ask questions about the PDF content.
Type 'quit' to exit the application.

Enter your question: What is the main idea of this document?
Answer:
The main idea of this document is that...

Enter your question: quit
Thank you for using the RAG CLI Application!
```

## How It Works

1. **Text Extraction**:
   - The `PyPDF2` library extracts text from each page of the PDF file.
   
2. **Preprocessing**:
   - The text is tokenized into sentences, lowercased, stopwords removed, and lemmatized using `nltk`.

3. **TF-IDF Vectorization**:
   - Each document (sentence or paragraph) is vectorized using `TfidfVectorizer` from `scikit-learn`.

4. **Document Retrieval**:
   - For a given query, the TF-IDF vectorizer computes the cosine similarity between the query and the documents, retrieving the top-k most relevant documents.

5. **Text Generation**:
   - The GPT-2 model generates answers based on the context (retrieved documents).

6. **Summarization**:
   - The BART summarization model is used to condense the context before generating the final answer.

## Customization

### Adjusting the Number of Retrieved Documents:

In the code, you can modify the number of documents retrieved (default is 2) by changing the `top_k` parameter:

```python
rag = RAG(documents, top_k=3)
```

### Adjusting the GPT-2 Output Length:

You can adjust the length of the generated answers by modifying the `max_length` parameter in the `generate_answer` function:

```python
response = self.generator(prompt, max_length=150, num_return_sequences=1)
```

## File Structure

```bash
.
├── data/
│   ├── data.pdf
├── Basic_RAG_app.ipynb
├── requirements.txt
└── README.md
```

- `data/`: Contains the PDF files to be processed.
- `Basic_RAG_app.ipynb`: Main script for running the RAG PDF Q&A application.
- `requirements.txt`: Lists all required Python dependencies.

## Requirements.txt

```txt
transformers==4.28.0
scikit-learn==1.0.2
PyPDF2==3.0.1
nltk==3.7
```

## Contributing

1. Fork the repository.
2. Create a new branch (`git checkout -b feature/new-feature`).
3. Commit your changes (`git commit -am 'Add new feature'`).
4. Push to the branch (`git push origin feature/new-feature`).
5. Create a new Pull Request.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.
