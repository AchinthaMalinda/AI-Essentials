# 🌊 Operation Ditwah – Crisis Intelligence Pipeline

An AI-powered disaster relief pipeline that classifies SOS messages, plans rescue logistics, and extracts structured data from news feeds using advanced prompt engineering techniques.

---

## 📌 Overview

Simulates a post-cyclone crisis response system for Sri Lanka's Disaster Management Center (DMC). The pipeline processes hundreds of incoming messages, prioritizes victims, and generates structured reports — all powered by LLMs.

---

## 🗂️ Project Structure

```
operation-ditwah/
├── data/
│   ├── sample_messages.txt     # Mixed incoming SOS/news messages
│   ├── scenarios.txt           # Ambiguous crisis scenarios
│   ├── incidents.txt           # Critical rescue incidents
│   └── news_feed.txt           # Raw 30-item news feed
├── outputs/
│   ├── classified_messages.xlsx
│   └── flood_report.xlsx
├── notebooks/
│   ├── part1.ipynb     # Few-shot classification
│   ├── part2.ipynb   # Temperature stress test
│   ├── part3.ipynb     # CoT & ToT rescue planning
│   ├── part4.ipynb   # Token economics / spam filter
│   └── part5.ipynb  # News feed extraction pipeline
├── .env.example
└── README.md
```

---

## ⚙️ Features

### Part 1 – Few-Shot Message Classifier
- Classifies incoming messages as `Rescue`, `Supply`, `Info`, or `Other`
- Uses few-shot prompting with 4+ labelled examples
- Outputs structured results to `classified_messages.xlsx`

```
Input:  "We are trapped on the roof with 3 kids!"
Output: District: None | Intent: Rescue | Priority: High

Input:  "Breaking News: Kelani River level at 9m."
Output: District: Colombo | Intent: Info | Priority: Low
```

### Part 2 – Temperature Stress Test
- Runs the same crisis scenario at `temperature=1.0` (Chaos) vs `temperature=0.0` (Safe)
- Demonstrates why determinism is critical in crisis systems

### Part 3 – Rescue Logistics (CoT + ToT)
- **Chain-of-Thought**: Scores each incident (1–10) based on age, need, and urgency
- **Tree-of-Thought**: Explores 3 routing strategies for a single rescue boat
  - Branch 1: Highest score first (Greedy)
  - Branch 2: Closest first (Speed)
  - Branch 3: Furthest first (Logistics)
- Selects the optimal route to maximize lives saved

### Part 4 – Token Budget Manager
- Counts tokens per message using `tiktoken`
- Messages over 150 tokens are truncated or summarized
- Prints `BLOCKED/TRUNCATED` for spam inputs

### Part 5 – News Feed Extraction Pipeline
- Parses 30 raw news items using an LLM
- Validates each item against a **Pydantic schema** (`CrisisEvent`)
- Exports clean structured data to `flood_report.xlsx`

---

## 🧠 Tech Stack

| Tool | Purpose |
|------|---------|
| Python | Core language |
| Google /  Groq | LLM backbone |
| Pydantic | Schema validation |
| Pandas | Data processing & Excel export |
| tiktoken | Token counting |
| python-dotenv | API key management |

---

## 🚀 Getting Started

### 1. Clone the repo
```bash
git clone https://github.com/yourusername/Crisis Management.git
cd Crisis Management
```

### 2. Install dependencies

### 3. Set up environment variables
```bash
cp .env.example .env
# Add your API key inside .env
```

`.env.example`:
```
GEMINI_API_KEY=your_key_here
```

### 4. Run any part
```bash
python parts/part1.ipynb
python parts/part2.ipynb
```

---

## 📊 Sample Output

**classified_messages.xlsx**

| Message | District | Intent | Priority |
|---------|----------|--------|----------|
| We are trapped on the roof! | None | Rescue | High |
| Kelani River level at 9m | Colombo | Info | Low |
| Need insulin urgently in Gampaha | Gampaha | Supply | High |

---

## 📚 Concepts Demonstrated

- ✅ Few-Shot Prompting
- ✅ Chain-of-Thought (CoT) Reasoning
- ✅ Tree-of-Thought (ToT) Strategy
- ✅ Temperature Control
- ✅ Token Economics
- ✅ Pydantic Schema Validation
- ✅ Structured Data Pipelines

---

## 👤 Author

**Your Name**  
[LinkedIn](https://www.linkedin.com/in/achintha-malinda/) • [GitHub](https://github.com/AchinthaMalinda)

---

## 📄 License

MIT License
