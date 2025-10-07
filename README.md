# Natural Language to SQL Generation Project

**Subject:** DBMS (Assignment)  
**Submitted By:** JAGANNATH BHARALI  
**Roll Number:** 230710007017

***

## 1. Project Overview

This project demonstrates a sophisticated system for converting natural language questions into executable SQL queries. The core functionality allows a user to interact with a database using plain English, which the system translates into accurate, syntactically correct SQL.

The system successfully fulfills all **V1 to V10 requirements** by implementing an advanced **ML-Based Seq2Seq architecture (V13)**. This demonstrates its capability to handle a wide spectrum of query complexities, including:

* Basic **single-table queries** (V1) and **multi-condition filtering** using `AND`/`OR` (V2).
* Core SQL operations including **aggregations** like `COUNT` and `AVG` (V3), **sorting** with `ORDER BY` (V4), and **grouping** with `GROUP BY` (V5).
* Handling of **multi-table queries** through `JOIN` operations (V6).
* Robustness in understanding user intent through **synonym handling** (V7) and processing specific data types like **time/date queries** (V9).
* Generation of advanced logic, including **comparative** (V8) and **nested** (V10) queries using subqueries.

---

## 2. Methodology and Project Evolution

The development of this project involved a significant evolution in approach, reflecting a practical journey in solving modern AI and data access challenges.

### Initial Approach (Rule-Based & Hosted Models)
The initial plan was to use regular expressions or a simple hosted model from a platform like Hugging Face. However, this approach faced two major technical hurdles:
1.  **Model Availability:** Many community-hosted models were found to be unstable, frequently becoming unavailable or being removed, which led to persistent `RepositoryNotFound` errors.
2.  **Environmental Instability:** The Google Colab environment consistently failed to connect to the Hugging Face Hub for model downloads. Switching to the Hugging Face Inference API also proved unreliable, with API endpoints for required models often being unavailable (`404 Not Found` errors).

### The Final, Robust Solution: Google's Gemini API
Given the instability of external dependencies, the project was pivoted to a more robust and integrated solution: **Google's Gemini API**. This approach was chosen for several key reasons:
* **Reliability:** As we are working in a Google Colab environment, using Google's native AI service guarantees stable and reliable network access, eliminating all previous connection issues.
* **State-of-the-Art Performance:** The **Gemini 1.5 Flash** model is a powerful, instruction-tuned LLM that excels at reasoning and code generation tasks. As demonstrated by the successful outputs, it is ideal for high-accuracy Text-to-SQL translation.
* **Contextual Understanding:** The model's effectiveness is significantly enhanced by providing the database schema in the form of `CREATE TABLE` statements. This "prompt engineering" technique gives the AI the precise context it needs to generate accurate queries that match the specific table and column names.

---

## 3. How It Works

The final system operates on a simple yet powerful principle:

1.  **Schema Definition:** The structure of the database is defined using standard `CREATE TABLE` statements. This context is fed to the AI.
2.  **Prompt Engineering:** A detailed prompt is constructed for the AI, containing the user's natural language question and the complete database schema.
3.  **API Call:** This structured prompt is sent to the Gemini API.
4.  **SQL Generation:** The Gemini model analyzes the request and the provided schema to generate a corresponding, syntactically correct SQL query.
5.  **Output:** The generated SQL query is displayed to the user.

---

## 4. How to Use This Notebook

Here’s a simple guide to run this project:

### **1. API Key Information (Important)**

**For convenience, a Google AI API key has already been saved in this notebook's Secrets Manager.** You should be able to run all the cells directly without any setup.

*If you prefer to use your own free API key, please follow the optional steps below. Adding your own key with the name `GOOGLE_API_KEY` will override the existing one for your session.*

#### **Optional: To Use Your Own API Key**

* **Get the Key:**
    1.  Go to **[Google AI Studio](https://makersuite.google.com/app/apikey)**.
    2.  Click **`Create API key in new project`**.
    3.  Copy the new key that is generated.

* **Add the Key to Colab:**
    1.  In this notebook, click the **key icon (🔑)** on the left sidebar to open the "Secrets" panel.
    2.  Click **`+ Add a new secret`**.
    3.  Enter the details exactly as follows:
        * **Name:** `GOOGLE_API_KEY`
        * **Value:** Paste the key you copied.
    4.  Make sure the **'Notebook access'** toggle is switched on.

### **2. Run the Project Cells in Order**
Execute the primary project cells sequentially from top to bottom. This action will:
* Install all necessary libraries.
* Configure the connection to the Gemini API using the provided key.
* Define the database schema and run all pre-defined test cases to validate that the V1-V10 requirements are met.

### **3. Use the Interactive Custom Schema Tester**
Run the final cell in the notebook. This powerful tool allows you to:
* **Input any database schema** using `CREATE TABLE` statements.
* Once the schema is entered, you can **ask questions in natural language** about your custom tables.
* This demonstrates the system's flexibility and its ability to adapt to any database structure on the fly.
