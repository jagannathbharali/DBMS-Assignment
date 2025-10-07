### **DBMS Assignment: Natural Language to SQL Generation**

* **Submitted By:** JAGANNATH BHARALI
* **Roll Number:** 230710007017

---

### ## 1. Project Overview

This project presents a sophisticated system that translates natural language questions into executable SQL queries. The core of this system is an advanced **ML-Based Seq2Seq architecture (V13)**, which allows users to interact with a database using plain English.

The system successfully fulfills all **V1 to V10 requirements**, demonstrating its capability to handle a wide spectrum of query complexities, including:

* **Basic Queries:** Single-table lookups (V1) and multi-condition filtering with `AND`/`OR` (V2).
* **Core SQL Operations:** Aggregations like `COUNT` and `AVG` (V3), sorting with `ORDER BY` (V4), and grouping with `GROUP BY` (V5).
* **Advanced Logic:** Multi-table `JOIN` operations (V6), comparative queries (V8), and nested subqueries (V10).
* **Robustness:** Handling of synonyms (V7) and specific data types like time/date (V9) to accurately interpret user intent.

---

### ## 2. Methodology and Technical Evolution

The project's methodology evolved significantly from its initial conception, overcoming key technical challenges to arrive at a robust and powerful final implementation.

#### ### Initial Approach and Challenges

The initial plan involved using regular expressions or a hosted model from a platform like Hugging Face. This approach was abandoned due to two major hurdles:

1.  **Model Instability:** Many community-hosted models proved unreliable, frequently leading to persistent **`RepositoryNotFound`** errors as models became unavailable or were removed.
2.  **Environmental Issues:** The Google Colab environment consistently failed to connect to the Hugging Face Hub. Furthermore, the Hugging Face Inference API was also unstable, with required model endpoints often returning **`404 Not Found`** errors.

#### ### Final Implementation: Google Gemini API

To overcome these issues, the project pivoted to using **Google's Gemini API**, a more integrated and reliable solution. This was chosen for several key reasons:

* **Reliability:** reliability: As a native Google service within the Colab environment, the Gemini API provides stable network access, eliminating all previous connection problems.
* **State-of-the-Art Performance:** The **Gemini 1.5 Flash** model is a powerful, instruction-tuned LLM that excels at reasoning and code generation, making it ideal for high-accuracy Text-to-SQL tasks.
* **Contextual Understanding:** The model's accuracy is significantly enhanced through **prompt engineering**. By providing the database schema as `CREATE TABLE` statements within the prompt, the AI gains the precise context needed to generate queries that match the specific table and column names. 

---

### ## 3. System Architecture and Workflow

The system operates on a simple yet powerful workflow:

1.  **Schema Definition:** The database structure is defined using standard `CREATE TABLE` statements.
2.  **Prompt Engineering:** A detailed prompt is constructed, containing both the user's natural language question and the complete database schema.
3.  **API Call:** This structured prompt is sent to the Gemini API. 🧠
4.  **SQL Generation:** The Gemini model analyzes the request and the provided schema to generate a corresponding, syntactically correct SQL query.
5.  **Output:** The final SQL query is displayed to the user.

---

### ## 4. User Guide and Interactive Demonstration

#### ### How to Run the Project

**1. API Key Information (Important)**

For your convenience, a Google AI API key is already saved in this notebook's Secrets Manager. **You can run all cells directly without any additional setup.**

* **Optional: To Use Your Own API Key**
    1.  Go to **Google AI Studio** and create a new API key.
    2.  In this notebook, click the **key icon (🔑)** on the left sidebar to open "Secrets."
    3.  Add a new secret with the name **`GOOGLE_API_KEY`** and paste your key as the value. Ensure 'Notebook access' is enabled.

**2. Execute the Cells in Order**

Run the primary project cells sequentially. This will:
* Install necessary libraries.
* Configure the Gemini API connection.
* Define the database schema and run all test cases to validate the V1-V10 requirements.

#### ### Interactive Custom Schema Tester

Execute the final cell in the notebook to launch a powerful interactive tool. This feature allows you to:

* **Input any custom database schema** using `CREATE TABLE` statements.
* **Ask questions in natural language** about your schema.
