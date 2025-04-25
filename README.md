# cf-contest-problem-scraper

# Codeforces Recent Contest Problem Collector 🧠

A Python script to collect and filter **recent Codeforces contest problems** by division and index — perfect for effective, modern competitive programming practice.

---

## ❓ Why not just solve old Codeforces problems?

Older Codeforces problems often don't reflect the **current style** or **difficulty progression** seen in today's contests. If you're practicing with problems from years ago, you're likely building intuition that's not so much optimal for recent rated rounds.

---

## ❓ What does this script do?

This script helps you **collect problems from recent contests only**, filtered by:

- **Division**: Div. 1, Div. 2, Div. 3, or Div. 4  
- **Problem Index**: A, B, C, D, etc.  
- **Date Range**: Only contests from the **last 2 years** you can change the time duration  
- **Contest Type**: Rated ,Unrated 

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
import requests
import csv
from datetime import datetime, timedelta

def fetch_contests():
    url = "https://codeforces.com/api/contest.list"
    response = requests.get(url)
    return response.json()

def fetch_problem(contest_id, problem_index):
    url = f"https://codeforces.com/api/contest.standings?contestId={contest_id}&from=1&count=10"
    response = requests.get(url)
    if response.status_code == 200 and response.json()["status"] == "OK":
        problems = response.json()["result"]["problems"]
        for problem in problems:
            if problem["index"] == problem_index:
                return {
                    "index": problem["index"],
                    "name": problem["name"],
                    "rating": problem.get("rating", "N/A"),
                    "tags": ", ".join(problem.get("tags", [])),
                    "link": f"https://codeforces.com/contest/{contest_id}/problem/{problem['index']}"
                }
    return None

def save_to_csv(data, filename):
    with open(filename, mode='w', newline='', encoding='utf-8') as file:
        writer = csv.DictWriter(
            file,
            fieldnames=["contest_name", "problem_name", "rating", "tags", "link", "complete"]
        )
        writer.writeheader()
        for row in data:
            row["complete"] = ""
            writer.writerow(row)

# 📌 MANUAL CONFIGURATION SECTION — Edit these two values as your input
selected_div = "div. 2"      # Options: "div. 1", "div. 2", "div. 3"
problem_index = "A"          # Example: "A", "B", "C", "D", "E", etc.

def is_index_ge(index: str, target: str) -> bool:
    return ord(index.upper()) >= ord(target.upper())

def is_index_le(index: str, target: str) -> bool:
    return ord(index.upper()) <= ord(target.upper())

def match_div(contest_name: str, selected_div: str, index: str) -> bool:
    name = contest_name.lower()

    if selected_div == "div. 1":
        if "div. 1" in name:
            return True
        if "div. 1 + div. 2" in name or "div. 2 + div. 1" in name:
            return is_index_ge(index, "E")
        return False  # 

    elif selected_div == "div. 2":
        if "div. 2" in name or "educational" in name:
            return True
        if "div. 1 + div. 2" in name or "div. 2 + div. 1" in name:
            return is_index_le(index, "D")
        return False

    elif selected_div == "div. 3":
        return "div. 3" in name
    
    elif selected_div == "div. 4":
        return "div. 4" in name

    return False

def main():
    OUTPUT_DIR = "D:/"

    data = fetch_contests()
    if data["status"] != "OK":
        print("❌ Failed to fetch contests.")
        return

    now = datetime.now()
    two_years_ago = now - timedelta(days=730) #Set Days (Manually)
    filtered_rows = []

    for contest in data["result"]:
        if contest["id"] >= 100000 or "startTimeSeconds" not in contest:
            continue

        contest_name = contest["name"]
        start_time = datetime.fromtimestamp(contest["startTimeSeconds"])
        if not (two_years_ago <= start_time <= now):
            continue

        if not match_div(contest_name, selected_div, problem_index):
            continue

        problem = fetch_problem(contest["id"], problem_index)
        if problem:
            row = {
                "contest_name": contest["name"],
                "problem_name": problem["name"],
                "rating": problem["rating"],
                "tags": problem["tags"],
                "link": problem["link"]
            }
            filtered_rows.append(row)

    filename = f"{OUTPUT_DIR}/cf_{selected_div.replace('.', '').replace(' ', '')}_problem_{problem_index.lower()}.csv"
    save_to_csv(filtered_rows, filename)
    print(f"✅ Saved {len(filtered_rows)} problems to '{filename}'")

if __name__ == "__main__":
    main()

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

## 🔗 Related Tags

`codeforces` · `competitive-programming` · `practice-tool` · `python-script` · `cf-api` · `recent-contests`

---

## ⭐ Found this useful?
Star the repo, share it with fellow CP learners, or drop suggestions..
