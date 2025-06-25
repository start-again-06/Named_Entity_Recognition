# 🧠 Named Entity Recognition (NER) using DistilBERT and TensorFlow

This project builds a Named Entity Recognition (NER) model using DistilBERT and TensorFlow. It processes annotated text data in DataTurks format and trains a transformer-based model to identify named entities such as people, organizations, and locations.

---

## 📂 Input Format

The dataset should be in JSON format, where each entry includes:

- `"content"`: the raw text
- `"annotation"`: a list of labeled entity spans with:
  - Entity label(s)
  - Character-level start and end positions
  - The exact matched text

This format is compatible with exports from annotation tools like DataTurks.

---

## 🛠️ Project Pipeline

### 1. Data Preprocessing

- Read the JSON data line by line.
- Remove newline characters and unnecessary fields (e.g., `extras`).
- Normalize spacing and format the content.

### 2. Entity Span Extraction

- Extract entity spans and labels from the annotations.
- Merge overlapping or adjacent spans that have the same label.

### 3. Format Conversion

- Convert data into a format compatible with spaCy and Hugging Face Transformers.
- Trim whitespaces from entity boundaries to ensure clean alignment.

### 4. Label Encoding

- Create mappings for each entity label to a unique ID.
- Tag each word/token with its corresponding entity label.
- Pad or truncate the tag sequences to a fixed length (e.g., 512 tokens).

### 5. Tokenization and Alignment

- Use a pretrained DistilBERT tokenizer to tokenize text.
- Align the tokenized words with their entity labels.
- Handle subword tokens with optional label propagation logic.

### 6. TensorFlow Dataset Creation

- Convert input IDs and label IDs into a TensorFlow Dataset.
- Shuffle and batch the dataset for training.

### 7. Model Training

- Use `TFDistilBertForTokenClassification` for token classification.
- Compile the model using an Adam optimizer and cross-entropy loss.
- Train the model for a few epochs (e.g., 3+) using the prepared dataset.

---

## 📦 Dependencies

- TensorFlow
- Hugging Face Transformers
- Pandas
- TQDM

You can install all dependencies using `pip`.

---

## 📁 Folder Structure

- ner.json # Annotated dataset
- tokenizer/ # Pretrained tokenizer files
- model/ # Pretrained or fine-tuned model files
- README.md # Project documentation

# ✅ Output

The final output is a fine-tuned DistilBERT model that can classify tokens in text as named entities. This model can be used in applications like document parsing, chatbot pipelines, or text analytics.

---

## 💡 Applications

- Resume and job description parsing
- Customer support automation
- Medical or legal text annotation
- Financial document processing
- Chatbot intent and slot recognition

---

## 📜 License

This project is intended for research, educational, and internal development use. For production or commercial deployment, please conduct additional testing and validation.

---
