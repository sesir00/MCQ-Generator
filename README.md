## Download Model
Run this command to download and extract the model:
```bash
./download_model.sh





# MCQ Generation System

## Overview
This project is an **MCQ (Multiple-Choice Question) Generation System** built using a **fine-tuned T5 model** on the **SQuAD dataset**. The model generates questions based on a given context and an answer, ensuring high relevance and accuracy.

## Features
- Uses a **fine-tuned T5 model** to generate factual MCQs.
- Trained on **SQuAD dataset** (train: 70k samples, validation: full dataset).
- Supports **Google Drive** and **Hugging Face** for model distribution.
- Automated model download script for easy setup.

## Installation
### 1. Clone the Repository
```bash
git clone https://github.com/your-username/mcq-generation.git
cd mcq-generation
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Download the Model
#### **Option 1: Google Drive (Automatic)**
```bash
./download_model.sh
```

## Usage
Run the script to generate MCQs from a given context:
```python
from transformers import AutoModelForSeq2SeqLM, AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("model")
model = AutoModelForSeq2SeqLM.from_pretrained("model")

def generate_mcq(context, answer):
    input_text = f"generate question: {answer} context: {context}"
    inputs = tokenizer(input_text, return_tensors="pt")
    outputs = model.generate(**inputs)
    question = tokenizer.decode(outputs[0], skip_special_tokens=True)
    return question

context = "Michael Phelps holds the record for the most Olympic gold medals."
answer = "Michael Phelps"
print(generate_mcq(context, answer))
```

## Model Details
- **Base Model:** `t5-base`
- **Fine-Tuned Dataset:** SQuAD (train: 70k, validation: full set)
- **Training Epochs:** 20 epochs (after initial 3 epochs on full data)
- **Output Style:** Generates factual, well-formed questions

## How the Model Works
- Identifies key subjects or concepts from the context.
- Constructs questions that retrieve the answer without explicitly including it.
- Examples:
  - **Input:** "Michael Phelps" → **Generated Question:** "Who holds the record for the most Olympic gold medals?"
  - **Input:** "Every four years" → **Generated Question:** "How often is the FIFA World Cup held?"

## Contributing
Feel free to open issues or submit pull requests. Any improvements, especially in refining the model’s performance, are welcome!

## License
This project is licensed under the MG License.

