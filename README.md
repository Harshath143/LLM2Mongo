
# 🧠 Natural Language to MongoDB Query Assistant

This Python application converts **natural language queries** into **MongoDB filter queries** using a **local LLM (Mistral via Ollama)**, and executes them against a local MongoDB collection.

---

## 📌 Features

- 🗣 Convert user-friendly text (e.g., "Find electronics with rating > 4") into MongoDB filter queries.
- ⚙️ Uses **Ollama + Mistral** for local LLM inference (no API keys or cloud services).
- 📊 Queries a MongoDB database and displays or saves the results.
- 💾 Output includes:
  - Original user input
  - Generated MongoDB filter
  - Matching documents

---

## 📂 Project Structure

```
project/
│
├── query_assistant.py         # Main script
├── README.md                  # Documentation
├── requirements.txt           # Required Python packages
```

## ⚙️ Requirements

- Python 3.8+
- MongoDB running locally
- Ollama with the `mistral` model pulled

## 📦 Installation

1. **Clone the Repository**
```bash
git clone https://github.com/your-repo/LLM2Mongo.git
cd LLM2Mongo
```

2. **Install Python Dependencies**
```bash
pip install -r requirements.txt
```
Or install manually:
```bash
pip install pymongo ollama
```

3. **Pull Mistral Model into Ollama**
Ensure Ollama is installed and running:
```bash
ollama pull mistral
ollama run mistral
```

## 🗃️ MongoDB Setup

Ensure your MongoDB server is running locally and contains the following:

- **Database:** `product_db`
- **Collection:** `products`

## 🚀 How to Use

Run the assistant script:
```bash
python query_assistant.py
```

Example interaction:
```
Enter your query (natural language): Show me electronics with rating above 4.5
Generated MongoDB Query: {'Category': 'Electronics', 'Rating': {'$gt': 4.5}}

Do you want to (d)isplay the results or (s)ave to a file? (d/s): s
Enter output file name (e.g., output.json): results.json
Query, MongoDB filter, and results saved to results.json
```

Output file (results.json) will look like:
```json
{
  "query": "Show me electronics with rating above 4.5",
  "mongodb_query": {
    "Category": "Electronics",
    "Rating": { "$gt": 4.5 }
  },
  "results": [
    {
      "ProductID": "E001",
      "ProductName": "Smart TV",
      "Category": "Electronics",
      "Rating": 4.7,
      ...
    }
  ]
}
```

## 🛠️ Customization

**Change database or collection:**
Edit these lines in `query_assistant.py`:
```python
db = mongo_client["product_db"]
collection = db["products"]
```

**Modify Supported Fields:**
Update the `system_msg` prompt to reflect your data schema.

## 🤝 Contributing

Pull requests and feature suggestions are welcome!

## 📄 License

MIT License

---

Let us know if you'd like:
- A sample `products.json` file to populate the database.
- Docker setup for easy deployment.
- Web UI version using Streamlit or FastAPI.
