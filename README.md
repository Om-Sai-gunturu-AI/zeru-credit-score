# Zeru Credit Score

This project is part of the Zeru AI Engineer Internship Assignment. The objective is to develop a machine learning-based scoring system that evaluates wallet creditworthiness (score range: 0–1000) using raw DeFi transaction data from the Aave V2 protocol.

---

## 🚀 Problem Statement

You are provided with 100K raw transaction-level JSON records of wallets interacting with the Aave V2 protocol via the following actions:

- `deposit`
- `borrow`
- `repay`
- `redeemunderlying`
- `liquidationcall`

Your task is to:
- Engineer meaningful features per wallet
- Build a scoring system that evaluates how safe or risky each wallet is
- Output a normalized credit score between 0 and 1000 for every wallet
- Analyze the distribution and explain score patterns

---

## 🛠️ Project Structure

```
zeru-credit-score/
│
├── main.py                  # Loads JSON and extracts features per wallet
├── score_wallets.py         # Computes credit scores using normalized features
├── analyze_scores.py        # Plots score distribution and summarizes findings
│
├── user_transactions.json   # Input dataset (~100K records)
├── wallet_features.csv      # Engineered wallet-level features
├── wallet_scores.csv        # Final credit scores for each wallet
├── score_distribution.png   # Histogram of score distribution
├── analysis.md              # Insights and patterns from scoring results
└── requirements.txt         # Python dependency list (optional)

🔍 Features Engineered per Wallet
| Feature                   | Description                                        |
| ------------------------- | -------------------------------------------------- |
| `num_txn`                 | Total number of transactions                       |
| `num_active_days`         | Count of unique days wallet was active             |
| `deposit_sum`             | Total deposit volume                               |
| `borrow_sum`              | Total borrow volume                                |
| `repay_sum`               | Total repay volume                                 |
| `redeemunderlying_sum`    | Total redemption volume                            |
| `liquidationcall_count`   | Number of liquidation events                       |
| `repay_to_borrow_ratio`   | Ratio of repay to borrow volume (safety indicator) |
| `redeem_to_deposit_ratio` | Redeemed vs deposited (capital recycling)          |

🎯 Scoring Logic
Credit scores are computed based on weighted normalized features:
Score = 
    + 0.25 * (repay_to_borrow_ratio)
    + 0.20 * (deposit_sum)
    + 0.20 * (num_active_days)
    + 0.15 * (redeem_to_deposit_ratio)
    + 0.10 * (txn_count)
    - 0.50 * (liquidation_count)
All inputs are normalized using MinMaxScaler and final scores are scaled to [0, 1000].

📈 Score Distribution
Scores range from ~200 to ~950

Most wallets fall between 400–800

High scores are associated with responsible activity:

High repay/borrow ratio

No liquidations

Consistent deposits and redemptions

Low scores indicate:

Little or no repayments

High borrow activity

Liquidation calls present

See analysis.md and score_distribution.png for a detailed breakdown.

💻 How to Run
1. Set up environment

python -m venv venv
.\venv\Scripts\activate
pip install -r requirements.txt

2. Run the full pipeline

python main.py           # Step 1: Extract features from raw JSON
python score_wallets.py  # Step 2: Score wallets based on features
python analyze_scores.py # Step 3: Analyze and plot results

📄 Requirements
You can install dependencies directly or use:

pip install pandas numpy matplotlib seaborn scikit-learn tqdm

📬 Submission
Final submission includes:

Source code (GitHub link)

wallet_scores.csv, score_distribution.png, analysis.md, and README.md

Submitted via the provided Google Form

👤 Author
G Om Sai
B.Tech (CSE) | Applicant for AI Engineer Internship @ Zeru

---