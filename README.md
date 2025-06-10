# SemEval 2024 Task 9: BRAINTEASER
## Lateral Thinking Puzzles for Large Language Models

![Project Banner](https://img.shields.io/badge/SemEval-2024-blue) ![Python](https://img.shields.io/badge/Python-3.7+-green) ![License](https://img.shields.io/badge/License-MIT-yellow)

**Authors:** AIT DIHIM Nassim, EL-HAMIDY Abderrahman, MENSOURI Mustapha  
**Affiliation:** Cadi Ayyad University  
**Date:** June 10, 2025

## 🧠 Overview

This repository presents our comprehensive evaluation of Large Language Models (LLMs) on lateral thinking puzzles as part of SemEval 2024 Task 9: BRAINTEASER. The project challenges AI models to "think outside the box" by solving creative reasoning problems that defy conventional commonsense associations.

### 🎯 Key Innovation
- **First comprehensive benchmark** for lateral thinking in NLP
- Tests ability to overcome default commonsense associations
- Evaluates creative, non-linear reasoning capabilities
- Compares zero-shot vs fine-tuning approaches

## 🧩 Task Description

### Lateral vs Vertical Thinking

| **Vertical Thinking** | **Lateral Thinking** |
|----------------------|---------------------|
| Sequential & Logical | Creative & Divergent |
| Step-by-step reasoning | Non-linear approach |
| Based on rules and rationality | Defies preconceptions |
| Convergent process | "Thinking outside the box" |

### Example Puzzles

**Sentence Puzzle:**
```
Q: A man shaves everyday, yet keeps his beard long.
A: He is a barber (shaves others, not himself)
```

**Word Puzzle:**
```
Q: What part of London is in France?
A: The letter "N"
```

## 📊 Dataset

### Data Statistics
| Dataset | Sentence Puzzle | Word Puzzle |
|---------|----------------|-------------|
| Training | 627 | 492 |
| Average Question Length | 34.88 tokens | 10.65 tokens |
| Long Questions (>30 tokens) | 48.32% | 2.23% |

- **Total Original Puzzles:** 373
- **With Reconstructions:** ~1,119 questions
- **Topics Covered:** 80+ domains (Math, Physics, Nature, Language)

### Data Format
```python
{
    'id': 'SP-0-OR',  # Data type and index
    'question': 'The six daughters of Mr. and Mrs. Mustard...',
    'answer': 'Each daughter shares the same brother.',
    'distractor1': 'Some daughters got married...',
    'distractor2': 'Some brothers were not loved...',
    'distractor(unsure)': 'None of above.',
    'label': 1,
    'choice_list': ['Some brothers were not loved...', 
                   'Each daughter shares the same brother.', 
                   'Some daughters got married...', 
                   'None of above.'],
    'choice_order': [2, 0, 1, 3]
}
```

## 🚀 Installation & Setup

```bash
# Clone the repository
git clone https://github.com/your-username/semeval-2024-brainteaser.git
cd semeval-2024-brainteaser

# Install dependencies
pip install -r requirements.txt

# Download the dataset
python download_data.py
```

## 🔧 Usage

### Training Fine-tuned Models
```bash
# Train RoBERTa model on sentence puzzles
python train.py --model roberta-large --task sentence --epochs 10

# Train DEBERTA model on word puzzles  
python train.py --model deberta-base --task word --epochs 8
```

### Zero-shot Evaluation
```bash
# Evaluate Claude Sonnet 4
python evaluate_zeroshot.py --model claude-sonnet-4 --task both

# Evaluate other models
python evaluate_zeroshot.py --model gemini-2.5-pro --task both
```

### Data Preprocessing
```bash
# Process raw data
python preprocess.py --input data/raw --output data/processed

# Generate adversarial examples
python generate_adversarial.py --type semantic --input data/processed
```

## 📈 Results

### Performance Comparison (Accuracy %)

| Model | Sentence Puzzle | Word Puzzle | Overall |
|-------|----------------|-------------|---------|
| **Human Performance** | **91.98** | **91.67** | **91.83** |
| | | | |
| **Zero-shot:** | | | |
| RoBERTa-large | 45.17 | 20.20 | 34.22 |
| Claude (Sonnet 4) | 41.66 | 58.07 | 53.46 |
| Deep Seek (R1) | 66.67 | 70.46 | 65.07 |
| Gemini (2.5 Pro) | 31.68 | 38.65 | 32.20 |
| | | | |
| **Fine-tuned:** | | | |
| **DEBERTA** | **95.54** | **87.50** | **78.45** |
| RoBERTa2 | 92.91 | 86.87 | 77.24 |
| ALBERT-base-v2 | 75.54 | 69.40 | 65.50 |
| DistilBERT-base | 75.00 | 71.50 | 68.25 |
| Random Baseline | 24.40 | 25.34 | 24.87 |

### Key Findings
- ✅ **Fine-tuned models consistently outperform zero-shot approaches**
- ⚠️ **Significant gap remains between AI and human performance**
- 🔍 **Models struggle more with word puzzles requiring letter-level reasoning**
- 🧠 **Current AI lacks true lateral thinking capabilities**

## 🏗️ Project Structure

```
semeval-2024-brainteaser/
├── data/
│   ├── raw/                    # Original puzzle data
│   ├── processed/              # Preprocessed data
│   ├── SP-train.npy           # Sentence puzzle training data
│   └── WP-train.npy           # Word puzzle training data
├── src/
│   ├── models/                # Model implementations
│   ├── evaluation/            # Evaluation scripts
│   ├── preprocessing/         # Data processing utilities
│   └── utils/                 # Helper functions
├── experiments/               # Experiment configurations
├── results/                  # Output results and logs
├── requirements.txt          # Python dependencies
└── README.md                # This file
```

## 🔬 Models Evaluated

### Fine-tuned Models
- **RoBERTa-large** (355M parameters)
- **DEBERTA-base** (125M parameters) 
- **ALBERT-base-v2** (12M parameters)
- **DistilBERT-base** (66M parameters)

### Zero-shot Models
- **Claude Sonnet 4**
- **Gemini 2.5 Pro**
- **Deep Seek R1**
- **RoBERTa-large**

## 📊 Evaluation Metrics

1. **Instance-based Accuracy:** Each question treated as separate instance
2. **Group-based Accuracy:** Score of 1 only when all questions in a group are correct
3. **Adversarial Robustness:** Performance on semantic and context reconstructions

## 🚧 Challenges & Limitations

- **Commonsense Bias:** Models stick to default assumptions
- **Memorization vs Reasoning:** Better performance on seen patterns
- **Inconsistency:** Different answers for reconstructed puzzles
- **Creative Reasoning Gap:** Difficulty with non-linear thinking

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

```bash
# Fork the repository
# Create a feature branch
git checkout -b feature/amazing-feature

# Commit your changes
git commit -m 'Add amazing feature'

# Push to the branch
git push origin feature/amazing-feature

# Open a Pull Request
```

## 📄 Citation

If you use this work, please cite:

```bibtex
@inproceedings{aitdihim2024brainteaser,
    title={SemEval 2024 Task 9: BRAINTEASER - Lateral Thinking Puzzles for Large Language Models},
    author={Ait Dihim, Nassim and El-Hamidy, Abderrahman and Mensouri, Mustapha},
    booktitle={Proceedings of SemEval 2024},
    year={2024},
    organization={Cadi Ayyad University}
}
```

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🔗 Links

- **SemEval 2024 Task Page:** [Official Task Description](https://semeval.github.io/SemEval2024/tasks)
- **Dataset Registration:** [Registration Form](mailto:yifjia@isi.edu)
- **Mailing List:** [Task Updates](mailto:yifjia@isi.edu)

## 🙏 Acknowledgments

- SemEval 2024 organizers for providing the BRAINTEASER dataset
- Cadi Ayyad University for supporting this research
- The NLP community for valuable feedback and discussions

---

**Made with 🧠 by the Cadi Ayyad University Team**
