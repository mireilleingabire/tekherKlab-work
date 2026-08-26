# 🤖 AI Bootcamp — Assignments Repository

Welcome to my **AI Bootcamp Assignments Repository**! 👩‍💻

This repository documents my learning journey throughout the AI Bootcamp, covering everything from **Python programming and data analysis to machine learning, deep learning, NLP, Generative AI, and model deployment**.

Each assignment represents a step toward building practical skills and developing real-world AI solutions.

---

## 👩‍💻 Author

**Ingabire Mireille**

🎯 **Focus:** Artificial Intelligence, Machine Learning & Data Science
📚 **Program:** AI Bootcamp
🌍 **Location:** Rwanda

> *Learning, building, experimenting, and growing one assignment at a time.*

---

## 🎯 Repository Goals

The main goals of this repository are to:

* 🐍 Strengthen Python programming skills
* 📊 Learn data manipulation and visualization
* 🤖 Understand machine learning concepts
* 🧠 Explore deep learning and neural networks
* 💬 Learn Natural Language Processing (NLP)
* ✨ Explore Generative AI
* 🚀 Practice deploying AI/ML models
* 📈 Develop practical problem-solving skills
* 💻 Build a strong portfolio of AI projects

---

## 📁 Repository Structure

```text
tekherKlab-work/
│
├── .venv/                    # Virtual environment (gitignored)
│
├── data/
│   ├── raw/                  # Original datasets
│   └── processed/            # Cleaned and processed datasets
│
├── notebooks/                # Jupyter notebooks for assignments
│
├── src/                      # Source code and reusable utilities
│
├── reports/                  # Reports, results, and visualizations
│
├── checkpoints/              # Saved model checkpoints (gitignored)
│
├── .env.example              # Environment variables template
├── .gitignore                # Git ignore rules
├── README.md                 # Project documentation
└── requirements.txt          # Python dependencies
```

---

# 🚀 Getting Started

Follow the steps below to set up the project locally.

## 1️⃣ Clone the Repository

```bash
git clone https://github.com/yourusername/tekherKlab-work.git
```

Move into the project directory:

```bash
cd tekherKlab-work
```

---

## 2️⃣ Create a Virtual Environment

### Windows — PowerShell

```powershell
python -m venv .venv
```

Activate the environment:

```powershell
.venv\Scripts\Activate.ps1
```

### macOS / Linux

```bash
python3 -m venv .venv
```

Activate it:

```bash
source .venv/bin/activate
```

---

## 3️⃣ Install Dependencies

After activating the virtual environment, install the required Python packages:

```bash
pip install -r requirements.txt
```

---

## 4️⃣ Configure Environment Variables

Create a `.env` file from the provided template:

### Windows

```powershell
Copy-Item .env.example .env
```

### macOS / Linux

```bash
cp .env.example .env
```

Add any required API keys or environment variables to `.env`.

> ⚠️ Never commit `.env` or API keys to GitHub.

---

# 📚 Assignments

The assignments are organized according to the bootcamp learning progression.

| Day    | Topic                               | Status     |
| ------ | ----------------------------------- | ---------- |
| Day 1  | 🐍 Python Fundamentals & AI Setup   | ✅ Complete |
| Day 2  | 🐼 Data Manipulation with Pandas    | ⏳ Upcoming |
| Day 3  | 📊 Data Visualization               | ⏳ Upcoming |
| Day 4  | 🤖 Introduction to Machine Learning | ⏳ Upcoming |
| Day 5  | 📈 Regression Models                | ⏳ Upcoming |
| Day 6  | 🎯 Classification Models            | ⏳ Upcoming |
| Day 7  | 🔍 Unsupervised Learning            | ⏳ Upcoming |
| Day 8  | 🧠 Neural Networks                  | ⏳ Upcoming |
| Day 9  | 🖼️ Convolutional Neural Networks   | ⏳ Upcoming |
| Day 10 | 🔄 Recurrent Neural Networks        | ⏳ Upcoming |
| Day 11 | 💬 NLP & Transformers               | ⏳ Upcoming |
| Day 12 | ✨ Generative AI                     | ⏳ Upcoming |
| Day 13 | 🚀 Model Deployment                 | ⏳ Upcoming |
| Day 14 | 📡 Production & Monitoring          | ⏳ Upcoming |
| Day 15 | 🏆 Final Project                    | ⏳ Upcoming |

---

# 🛠️ Technologies & Tools

Throughout the bootcamp, this repository may include the following technologies:

### 🐍 Programming

* Python
* Jupyter Notebook

### 📊 Data Science

* NumPy
* Pandas
* Matplotlib
* Seaborn

### 🤖 Machine Learning

* Scikit-learn

### 🧠 Deep Learning

* TensorFlow
* PyTorch
* Keras

### 💬 Natural Language Processing

* Transformers
* Hugging Face

### 🚀 Deployment & APIs

* Flask
* FastAPI

---

# 📦 Main Python Libraries

The main dependencies are maintained in:

```text
requirements.txt
```

Some of the key packages include:

```text
numpy
pandas
matplotlib
seaborn
scikit-learn
tensorflow
torch
transformers
jupyter
flask
fastapi
```

Install everything with:

```bash
pip install -r requirements.txt
```

---

# 🔀 Git & GitHub Workflow

Each assignment should be developed on its own branch.

## 1. Create a Branch

```bash
git checkout -b dayXX-assignment
```

Example:

```bash
git checkout -b day01-assignment
```

## 2. Add Changes

```bash
git add .
```

## 3. Commit Changes

```bash
git commit -m "feat: day XX assignment"
```

## 4. Push the Branch

```bash
git push -u origin dayXX-assignment
```

## 5. Submit the Branch

Use the corresponding GitHub branch URL:

```text
https://github.com/yourusername/tekherKlab-work/tree/dayXX-assignment
```

---

# 🧪 Working With Jupyter Notebooks

To start Jupyter Notebook:

```bash
jupyter notebook
```

Alternatively, notebooks can be opened and executed directly using **VS Code** with the Jupyter extension.

Make sure the correct Python environment/kernel is selected before running the notebook.

---

# 🔧 Common Issues

| Problem                             | Possible Solution                                       |
| ----------------------------------- | ------------------------------------------------------- |
| `ModuleNotFoundError`               | Run `pip install -r requirements.txt`                   |
| Jupyter kernel not starting         | Select the correct Python interpreter/kernel            |
| Packages installed but not detected | Make sure VS Code is using `.venv`                      |
| Plots are not displayed             | Run the notebook cell again or use `%matplotlib inline` |
| Git push rejected                   | Run `git pull` and resolve any conflicts                |
| Permission errors                   | Check folder permissions or use an appropriate terminal |

---

# 📖 Learning Resources

The following official documentation is useful throughout the bootcamp:

* [Python Documentation](https://docs.python.org/3/)
* [NumPy Documentation](https://numpy.org/doc/)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Scikit-learn Documentation](https://scikit-learn.org/stable/)
* [Matplotlib Documentation](https://matplotlib.org/stable/)
* [TensorFlow Documentation](https://www.tensorflow.org/)
* [PyTorch Documentation](https://pytorch.org/)
* [Hugging Face Documentation](https://huggingface.co/docs)

---

# 🎓 Academic Integrity

This repository is part of my personal learning journey.

I commit to:

* ✅ Understanding the code I submit
* ✅ Using external resources for learning
* ✅ Giving credit where appropriate
* ✅ Practicing and experimenting independently
* ❌ Not copying another student's work
* ❌ Not submitting code that I do not understand

---

# 🌱 Learning Journey

This repository will continue to grow as I progress through the bootcamp.

From writing my first Python programs to developing and deploying AI solutions, every assignment is an opportunity to:

**Learn → Practice → Build → Improve → Grow 🚀**

---

# 📌 Repository Status

🚧 **Active Development**

Assignments will be added and updated throughout the AI Bootcamp.

---

### ⭐ Thank You for Visiting!

Thank you for checking out my AI Bootcamp journey.

**Learning today. Building tomorrow. Creating impact with AI. 🤖✨**

---
