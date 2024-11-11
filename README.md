# SQL Query Generation using Transformers
## Introduction
Relational databases are essential for managing structured data across various fields. However, writing SQL queries can be challenging for users without technical backgrounds. Recent advances in Natural Language Processing (NLP) have led to solutions where language models can translate natural language instructions into SQL queries. This project employs Hugging Face’s `sqlcoder-7b-2` model to simplify SQL query generation, lowering the entry barrier for users in database interaction.

## Problem Statement
The goal of this project is to provide an NLP-based tool that:
1. Converts natural language questions into SQL queries.
2. Ensures generated queries are efficient and compatible with the database schema.

## Methodology

### Imports and Model Setup
Key tools and libraries used:
- **torch**: Manages tensor operations and GPU-based model loading.
- **transformers**: Loads the `sqlcoder-7b-2` model, enabling SQL query generation.
- **bitsandbytes**: Supports model quantization, optimizing memory usage for devices with limited resources.

Based on GPU memory availability, the model loads in either `float16` precision or `8-bit` mode, balancing performance and memory efficiency.

### Prompt Creation
The model is guided by a structured prompt, which includes:
- **Task description**: An instruction to generate an SQL query.
- **Additional rules**: Logical instructions, such as revenue and cost calculations.
- **Database schema**: The schema defines table structures and relationships, helping the model interpret user queries accurately.

### Function to Generate SQL Queries
The function `generate_query(question)` performs the following steps:
1. **Prompt Update**: The base prompt is updated with the specific user question.
2. **Tokenization**: `AutoTokenizer` processes the prompt.
3. **Model Prediction**:
   ```python
   generated_ids = model.generate(inputs, num_return_sequences=1, max_new_tokens=400)
  Result
The model accurately interpreted natural language questions, generating valid SQL statements for database operations such as aggregations and joins. Generated queries were validated against the database schema to ensure compatibility and accuracy.

Conclusion
This project demonstrates that models like sqlcoder-7b-2 can efficiently translate natural language queries into SQL statements, enabling non-technical users to interact with databases easily. Future improvements could focus on refining model responses for complex queries and enhancing prompt accuracy. Adding error-checking mechanisms would further improve the tool's reliability.

License
