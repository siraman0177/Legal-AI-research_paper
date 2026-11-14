# LegalGPT: Chunking Strategies in RAG for Legal Assistance

A research project exploring how document chunking strategies influence
retrieval and answer quality in a Retrieval-Augmented Generation (RAG)
system for Indian legal documents.

The project compares **fixed-size, semantic, and recursive chunking**
using a common retrieval and generation pipeline. It evaluates the
generated answers across multiple open-source large language models
(LLMs).

## Research Paper

**Title:** *LegalGPT: Chunking Strategies in Retrieval Augmented
Generation for Legal Assistance*

The research paper is included in this repository as
[`my_reseach_paper.pdf`](my_reseach_paper.pdf).

## Project Overview

Legal documents are lengthy and structurally complex. Splitting them
into chunks before embedding and retrieval can affect which information
is retrieved and how well an LLM answers a legal query.

This project investigates that effect using Indian statutory documents
as the knowledge base and a benchmark of 500 legal queries selected from
a dataset of 24,607 query-response pairs.

## Methodology

The system follows a Retrieval-Augmented Generation workflow:

1.  **Document collection** -- Use Indian statutory legal documents as
    the knowledge base.
2.  **Chunking** -- Create separate corpora using three chunking
    strategies.
3.  **Embedding generation** -- Generate 3,072-dimensional embeddings
    with OpenAI `text-embedding-3-large`.
4.  **Vector indexing** -- Store and index embeddings in Qdrant.
5.  **Retrieval** -- Retrieve the top five contextually similar chunks
    using cosine similarity.
6.  **Answer generation** -- Pass the query and retrieved context to an
    LLM running through Ollama.
7.  **Evaluation** -- Compare generated answers using the selected
    evaluation metrics.

## Chunking Strategies Compared

  -----------------------------------------------------------------------
  Strategy                            Description
  ----------------------------------- -----------------------------------
  Fixed-size                          Splits documents into consecutive
                                      chunks of a predefined size.

  Semantic                            Splits text around natural and
                                      semantically meaningful boundaries
                                      to preserve context.

  Recursive                           Splits documents hierarchically,
                                      using structural boundaries and
                                      smaller segments when needed.
  -----------------------------------------------------------------------

Each strategy is indexed separately so that retrieval results can be
compared.

## Models and Evaluation

### LLMs evaluated

-   Llama 3 8B
-   Llama 3.1 8B
-   Gemma 3 12B
-   Mistral 7B

The paper specifies a generation temperature of **0.2** and a top-five
retrieval configuration.

### Evaluation metrics

-   **Precision** -- Measures the relevance of retrieved information.
-   **Semantic Similarity** -- Measures semantic alignment between
    generated and reference answers.
-   **ROUGE-1** -- Measures unigram overlap.
-   **ROUGE-L** -- Measures longest-common-subsequence overlap.

Mean, median, and standard deviation are used to examine performance and
variability.

## Key Findings

The experiments indicate that:

-   No single chunking strategy performs best across every evaluated
    model and metric.
-   Semantic chunking performs strongly for some model configurations.
-   Fixed-size chunking shows comparatively stable performance across
    models.
-   Recursive chunking performs strongly for some model configurations,
    including Mistral 7B.
-   Chunking strategy can influence the relevance of retrieved context
    and the quality of generated answers.

The results suggest that chunking should be selected with the target
language model and evaluation objective in mind.

## Technology Stack

-   **Language:** Python
-   **Embeddings:** OpenAI `text-embedding-3-large`
-   **Vector database:** Qdrant
-   **LLM runtime:** Ollama
-   **LLMs:** Llama 3, Llama 3.1, Gemma 3, Mistral
-   **Evaluation:** Precision, semantic similarity, ROUGE-1, ROUGE-L
-   **Research artifacts:** Jupyter Notebooks, JSONL dataset,
    legal-document PDFs

## Repository Structure

``` text
Legal-AI-research_paper/
├── Acts/                  # Indian statutory legal documents
├── generator.ipynb        # Generation and evaluation workflow
├── knowledgebase.ipynb    # Document processing, chunking and indexing
├── queries_500.jsonl      # Evaluation query dataset
├── my_reseach_paper.pdf  # Research paper
└── README.md
```

## Running the Project

The implementation is organized in Jupyter notebooks:

1.  Review `knowledgebase.ipynb` for document processing, chunking,
    embedding generation, and vector indexing.
2.  Review `generator.ipynb` for retrieval, answer generation, and
    evaluation.
3.  Configure the required OpenAI API access, Qdrant database, and
    Ollama models before running the relevant notebook cells.

> **Note:** The notebooks may require environment-specific configuration
> and dependencies. Check the notebook setup cells before execution.

## Scope and Disclaimer

This project is a research and reference system for exploring
legal-document retrieval and question answering. It is **not a
substitute for a qualified legal professional**, and its generated
responses should not be treated as legal advice.

## Author

**Aman Singh Patel**\
B.Tech -- Artificial Intelligence and Machine Learning\
Pranveer Singh Institute of Technology (PSIT), Kanpur

[GitHub](https://github.com/siraman0177) ·
[LinkedIn](https://www.linkedin.com/in/aman-singh-patel-0b3a2127b/)

------------------------------------------------------------------------

If you find this project useful, consider starring the repository.
