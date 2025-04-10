# Local Chat App (Fixed Version)

This is a fixed version of the Local Chat App that includes all the necessary dependencies correctly configured in package.json.

## Installation Instructions

### 1. Clone the repository

```bash
git clone https://github.com/thenzler/local-chat-app-fixed.git
cd local-chat-app-fixed
```

### 2. Install Node.js dependencies

```bash
npm install
```

### 3. Install Ollama

#### For Windows:
1. Visit [https://ollama.com/download/windows](https://ollama.com/download/windows)
2. Download and run the Windows installer
3. Follow the installation instructions

#### For macOS:
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

#### For Linux:
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

### 4. Install Qdrant (using Docker)

Make sure Docker is installed on your system, then run:

```bash
docker run -d -p 6333:6333 -p 6334:6334 -v ./qdrant_storage:/qdrant/storage qdrant/qdrant
```

### 5. Configure environment variables

```bash
# Copy the example .env file
cp .env.example .env
```

Edit the `.env` file as needed (the default values should work in most cases).

### 6. Download an LLM model for Ollama

Choose one of the following models based on your hardware capabilities:

```bash
# For a small, fast model (1-2 GB)
ollama pull tinyllama

# For a medium-sized model with better quality (4-5 GB)
ollama pull mistral

# For the best results (8-10 GB)
ollama pull llama3

# Localized German model (5-6 GB)
ollama pull orca-mini:3b-de
```

Update your `.env` file to use the model you downloaded:
```
OLLAMA_MODEL=mistral
```

### 7. Create necessary directories

```bash
mkdir -p documents
```

### 8. Add documents to index (optional)

Place your documents (PDF, DOCX, TXT, MD, HTML) in the `documents` directory.

### 9. Index your documents

```bash
npm run index-docs
```

### 10. Start the application

```bash
npm start
```

Access the application by opening your browser and navigating to:
```
http://localhost:3000
```

## Troubleshooting

### Ollama is not starting
1. Make sure you have enough disk space
2. Check if another process is using port 11434
3. Start the service manually: `ollama serve`

### Qdrant is not reachable
1. Check if Docker is running
2. Restart the Qdrant container: `docker restart CONTAINER_ID`

### Indexing fails
1. Check if your documents are in supported formats
2. Make sure documents are readable and not password protected
3. Check console output for specific error messages

### LLM responses are slow
1. Choose a smaller model in the `.env` file
2. Enable GPU acceleration in Ollama if available
3. Increase RAM allocation for Docker (for Qdrant)

## Customization

### Changing the LLM model
Edit the `.env` file and change `OLLAMA_MODEL` to one of your installed models.

### Customizing vector search
- `CHUNK_SIZE`: Size of text chunks (default: 500 characters)
- `CHUNK_OVERLAP`: Overlap between chunks (default: 50 characters)

### Customizing the system prompt
The system prompt defines how the AI should respond. You can customize this in the `.env` file under `SYSTEM_PROMPT`.
