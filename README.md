# cf-contest-problem-scraper

# Codeforces Recent Contest Problem Collector 🧠

A Python script to collect and filter **recent Codeforces contest problems** by division and index — perfect for effective, modern competitive programming practice.

---

## ❓ Why not just solve old Codeforces problems?

Older Codeforces problems often don't reflect the **current style** or **difficulty progression** seen in today's contests. If you're practicing with problems from years ago, you're likely building intuition that's no longer optimal for recent rated rounds.

---

## ❓ What does this script do?

This script helps you **collect problems from recent contests only**, filtered by:

- **Division**: Div. 1, Div. 2, Div. 3, or Div. 4  
- **Problem Index**: A, B, C, D, etc.  
- **Date Range**: Only contests from the **last 2 years**  
- **Contest Type**: Rated contests only (no unrated/testing rounds)

It then saves the problems into a **CSV file** with metadata like tags, rating, and direct links — ready for structured practice.

---

## ❓ Who is this for?

- 🧩 **Beginners** who want to get better faster by solving modern problems  
- 🔁 **Returning CP users** who want to adapt to new trends  
- 📊 **Serious coders** looking to organize practice based on real, recent contests  

---

## ❓ How do I use it?

### 1. Install `requests` if not already:
```bash
pip install requests

### 2. Edit two lines in the script:
```python
selected_div = "div. 2"    # Choose from: "div. 1", "div. 2", "div. 3", "div. 4"
problem_index = "B"        # Set the problem index you're practicing
```

### 3. Run the script:
```bash
python cf_recent_problem_scraper.py
```

### 4. Get your CSV:
Your filtered problems will be saved with ratings, tags, links, and a checkbox column.

---
## ❓ What does the CSV contain?

Each row includes:

- Contest name  
- Problem name  
- Problem rating  
- Problem tags  
- Direct problem link  
- A column to mark as "complete" ✔️

Perfect for building your own practice tracker!

---

## ❓ Why focus on recent contest problems?

Practicing modern problems helps you:

- Train on **up-to-date patterns**
- Prepare for upcoming contests more effectively
- Skip outdated styles and low-relevance questions
- Build **relevant problem-solving muscle**

This is especially important if you plan to participate in rated contests soon.

---

## ❓ What makes this tool different?

Unlike tools that show the entire problemset, this one:

✅ Filters **recent contests only**  
✅ Filters by **division and index**  
✅ Saves everything neatly to CSV  
✅ Lets you stay focused and skip searching manually

---

## 📎 License

This project is licensed under the **MIT License** — free to use, modify, and distribute.

---

## 🔗 Related Tags

`codeforces` · `competitive-programming` · `practice-tool` · `python-script` · `cf-api` · `recent-contests`

---

## ⭐ Found this useful?
Star the repo, share it with fellow CP learners, or drop suggestions in the issues tab!
