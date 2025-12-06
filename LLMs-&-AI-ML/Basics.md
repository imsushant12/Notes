
## RAG (Retrieval-Augmented Generation) — Notes
RAG is a method where, before generating an answer, the system retrieves relevant documents from an external knowledge base and combines them with the user’s query to guide the model's response.

### Main Components
1. **Retrieval**: 
   Search and fetch the most relevant documents or document chunks based on the user’s query.

2. **Augmentation**: 
   Combine the user’s query and the retrieved documents into a single expanded prompt.

3. **Generation**: 
   Pass the augmented prompt to a Large Language Model (LLM) which then generates the final answer.

**Why RAG is Useful**:
- Answers are based on real, up-to-date documents.
- Reduces the need for retraining or fine-tuning the model.
- Improves trustworthiness and relevance of answers.
- Cost-effective for dynamic and large datasets.

**Key Point**: RAG does not teach the model new information permanently; it temporarily augments the model’s knowledge during each query.

#### RAG Diagram:
```
[ User Query ]
        ↓
[ Retriever → Find Best Documents/Chunks ]
        ↓
[ Augmentor → Merge Query + Retrieved Documents ]
        ↓
[ LLM → Generate Final Answer ]
        ↓
[ Output to User ]
```

## Vector Embeddings — Short Notes
Vector Embedding is the process of converting text into a fixed-size numerical vector that captures the semantic meaning of the text.
- Machines work better with numbers than text.
- Embeddings allow machines to measure similarity between texts mathematically.
- Essential for search, retrieval, and matching user queries to documents.

### How are Embeddings Created?
- Text is broken down into tokens (smallest units like words or subwords).
- These tokens are passed through an embedding model (trained neural network).
- The model outputs a vector (list of numbers) representing the meaning of the text.
- Similar meanings create vectors that are mathematically closer together.

### Properties of Vector Embeddings:
- **Semantic closeness**: Similar texts have similar vectors.
- **Fixed size**: Each embedding has a consistent number of dimensions (e.g., 512, 1536).
- **Math-friendly**: We can apply similarity measures like cosine similarity or dot product.

#### Example:
| Text | Vector Embedding (Simplified) |
|:---|:---|
| "Install SLES 15" | [0.23, -0.44, 0.89, ...] |
| "Setting up SUSE Linux" | [0.20, -0.45, 0.87, ...] |
| "Cloud Deployment" | [-0.67, 0.12, 0.05, ...] |

- First two texts are similar → vectors are close.
- Third text is different → vector is far.

### How Embeddings Internally Work
- Text → Tokenization (breaking into pieces)
- Tokens → Processed through a neural network (embedding model)
- Neural network learns context and relationships during training
- Output → A dense vector capturing the "meaning" of the text
- No need to know deep math, but basic flow is important.

#### Vector Embedding Flow Diagram:
```
[ Text Input ]
      ↓
[ Tokenizer → Break Text into Tokens ]
      ↓
[ Embedding Model → Converts Tokens into Vector ]
      ↓
[ Numeric Vector Representation ]
```

## Vector Store  
A Vector Store is a system that saves and retrieves vector embeddings efficiently.
- Stores embeddings created from text, images, or other data.
- Allows similarity search i.e. finding vectors close to a given query vector.
- Focus is mainly on basic storage and retrieval.
- Examples: FAISS (basic usage), Chroma.

#### Vector Store Diagram:
```
[ Text Chunks ]
     ↓
[ Generate Embeddings ]
     ↓
[ Vector Store ]
     ↓
[ Search for Similar Embeddings ]
     ↓
[ Retrieve Relevant Documents ]
```

## Vector Database
A Vector Database is a full-fledged database system built specifically to manage vector data at scale.
- Not only stores and retrieves vectors but also **indexes**, **scales**, **replicates**, and **manages** them like a traditional database.
- Provides **high availability**, **security**, **persistence**, **backup**, and **APIs**.
- Supports large-scale deployments and production-grade applications.
- Examples: Pinecone, Milvus, Weaviate.

### Why Needed Beyond Vector Store:
- Large production systems need automatic scaling, failure recovery, multi-user access, secure connections, and backup.
- Vector databases handle these needs automatically.

#### Vector Database Diagram:
```
[ Text Chunks ]
     ↓
[ Generate Embeddings ]
     ↓
[ Vector Database (Pinecone, Milvus, etc.) ]
     ↓
[ Auto-Indexing, Replication, Scaling ]
     ↓
[ Search for Similar Embeddings ]
     ↓
[ Retrieve Relevant Documents ]
```


## Chunking
Chunking means breaking a large document into smaller parts (chunks) so they can be processed, embedded, and searched easily.

### Why Chunking?
- **LLM Context Limit**:  
  LLMs have a token limit (example: 4k, 8k, 32k tokens).  
  A huge document can't fit, so it must be broken.

- **Efficient Retrieval**:  
  It's easier to find a highly relevant small chunk than to search the whole document.

- **Better Precision in Answers**:  
  The model focuses only on the relevant part instead of getting distracted by unrelated information.


### How is Chunk Size Decided?
Chunk size depends on:

| Factor | Explanation |
|:---:|:---:|
| LLM context limit | Choose a size much smaller than the model's max token limit (ex: if limit is 8k tokens, chunks could be 300–500 tokens). |
| Nature of the content | Technical documents (like SUSE docs) may need smaller chunks, storybooks may allow bigger chunks. |
| Search quality | Smaller chunks = more specific, but may lose context. Larger chunks = more context, but less specific retrieval. |

**Typical range**:  
- 300–800 tokens per chunk  
- (depends on experimentation)

### What is Chunk Overlap?  
Chunk overlap means some content is repeated between adjacent chunks.

**Why needed**?
- Important ideas sometimes sit **between two sentences**.
- If you split strictly at fixed sizes, you may **cut an idea in half**.
- Overlapping helps preserve context across chunks.

**Example**:
If Chunk 1 ends at sentence 5 and Chunk 2 starts from sentence 5 again (overlapping 1 sentence), you maintain continuity.

## Chunking Techniques:
| Technique | Description |
|:---:|:---:|
| Fixed-size Chunking | Divide after fixed number of tokens/characters (simple, fast).|
| Semantic Chunking | Split intelligently at sentence or paragraph boundaries using NLP (better but complex).|
| Adaptive Chunking | Adjust chunk size dynamically based on content meaning (advanced systems use this).|

## Context Window
It is the amount of text (tokens or words) that the model can "see" or process at once when making predictions or generating outputs. Essentially, it’s the portion of text around a particular token or word that the model uses to understand and predict the next token or word in a sequence.

### Key Points About Context Window
1. **Fixed-Length**:
   - In most models, the context window is fixed-length, meaning the model can only look at a specific number of tokens (words or subwords) in the input sequence, no matter how long the text is.
   - For example, if a model has a context window of 512 tokens, it will only process 512 tokens at a time, even if the input text is longer. For longer text, the model may lose information from the earlier parts of the text.

2. **Sliding Window**:
   - If the input text exceeds the context window size, a sliding window approach may be used, where the model processes the text in overlapping chunks.
   - For instance, in the case of a window size of 512 tokens, the model may process tokens 1–512 in one pass, then tokens 256–768 in the next pass, and so on.

3. **Contextual Understanding**:
   - The context window helps the model understand relationships between tokens (words, subwords) in a given span of text. The more tokens the model considers, the better it can understand long-range dependencies and nuances in the text.
   - For example, in sentence generation or translation tasks, the model needs to understand not only the immediate surrounding words but also the broader context in which those words occur.

4. **Limitations**:
   - The context window size directly affects the model’s capacity to capture long-range dependencies. If the context window is too small, the model may struggle to maintain coherent understanding over long passages of text (e.g., losing track of earlier parts of a conversation or document).
   - For example, earlier versions of models like GPT-2 had a smaller context window (e.g., 512 tokens), which meant they couldn't maintain context over very long texts. However, more advanced models like GPT-3 have a larger context window (e.g., 2048 tokens or more), allowing them to process longer inputs.

5. **Context Window in Transformers**:
   - In transformer-based models (like GPT, BERT, etc.), the context window refers to the number of tokens the model can attend to when calculating attention. These models use self-attention mechanisms, where each token in the input can potentially "attend" to every other token within the context window.
   - The size of the context window impacts the computational complexity because each token attends to every other token, and the complexity grows quadratically with the size of the context window.

## AI Guardrails
They are rules, techniques, and safety measures that are put in place to make sure an AI system behaves properly — meaning it acts **safe**, **ethical**, **useful**, and **aligned** with what humans want.

Without guardrails, AI can:
- Generate toxic, offensive, or biased outputs
- Hallucinate facts (make things up)
- Give unsafe advice (like medical or legal advice incorrectly)
- Be manipulated by attackers (prompt injection)
- Violate privacy or ethics


## Vector Search Algorithms
Vector Search is the process of finding the most similar vectors to the query vector.

### Two Main Types of Vector Search:
| Type | Description | Example Usage |
|:----:|:-----------:|:-------------:|
| Exact Search | Finds exact nearest neighbors (100% accurate). | Small datasets, high-accuracy needs. |
| Approximate Search (ANN) | Finds almost nearest neighbors (fast and good enough). | Large datasets, real-time needs. |

### How Similarity is Measured?
- **Cosine Similarity**: Measures **angle** between two vectors. (Smaller angle = more similar.)
- **L2 Distance (Euclidean)**: Measures **straight-line distance** between points.

### Popular ANN Algorithms:
| Algorithm | How it Works | Advantages |
|:---------:|:------------:|:----------:|
| HNSW (Hierarchical Navigable Small World) | Builds a graph where vectors are connected based on closeness. | Very fast search, used in production systems. |
| FAISS (Facebook AI Similarity Search) | Combines different techniques like graphs and quantization. | Extremely optimized, used by Meta, Hugging Face. |
| ScaNN (by Google) | Optimized for large-scale search with low memory. | Useful for very very large datasets. |

### Step-by-Step of Vector Search:
1. User types a query.
2. Embed the query into a vector (same model used as for documents).
3. Perform ANN search using:
   - HNSW, FAISS, or others.
4. Get Top-K most similar chunks (example: top 5 chunks).
5. Pass these retrieved chunks + user query → LLM for final answer generation.

