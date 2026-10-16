<h1> Dekoruma Failed Installation Analysis </h1>

## 1. Project Overview
This project analyzes business data to extract insights, improve decision-making, and identify key trends. The primary focus is to **[Your Problem Statements]**(mention business objectives, such as optimizing sales, reducing operational costs, customer segmentation, etc.).

Key Objectives:
- Supplier Quality Improvement: identify suppliers and product categories that disproportionately drive missing parts and damaged panels.
- Installer & Logistics Performance: test whether delivery-to-installation lag, installers, store location, or region affect failure rates.
- Omnichannel Attribution Accuracy: measure the link between DEC presence and App/Web purchases, and how much of it is captured in the data.
- Data Quality: document validation gaps (inconsistent categories, impossible values, illogical dates, missing acquisition channels) as prerequisites for reliable KPIs

## 2. Data Sources
Six tables from the dekoruma MySQL database (transactions January–December 2023), provided as part of the Purwadhika Data Analytics capstone:
- [orders] - Consist of 321,760 rows data - orders, delivery and installation dates, installer, installation status, assembly fee
- [return_requests] – Consist of 24,843 rows data - Return reason, resolution status, refund method and amount, satisfaction score
- [products] - Consist of 1,500 rows data - SKU, category, assembly requirement, supplier, unit price, weight category
- [suppliers] - Consist of 32 rows data - Supplier type, region, product family, quality certification
- [customers] - Consist of 277,928 rows data - Domicile city, registration and acquisition channel, membership
- [stores] - Consist of 40 rows data - 	Physical stores (DEC) and online channels (Mobile App, Web)

## 3. Technologies Used
- Programming Language: Python (Pandas, NumPy)
- Database: MySQL (PyMySQL)
- Statistics: SciPy, Statsmodels (logistic regression)
- Visualization: Matplotlib, Seaborn
- Presentation: Microsoft PowerPoint
- Others: Jupyter Notebook, Git

## 4. Project Structure

```
├── README.md          <- The top-level README for developers using this project.
|
├── data
│   ├── raw            <- Data from third party sources.
│   └── cleaned        <- The data that has been cleaned.
│
├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
│                         the creator's initials, and a short `-` delimited description, e.g.
│                         `1.0-jqp-initial-data-exploration`.
│
├── reports            <- Generated analysis as PowerPoint, PDF, LaTeX, etc.
|   ├── slide          <- Generated PowerPoint
│   └── figures        <- Generated graphics and figures to be used in reporting
│
├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
│                         generated with `pip freeze > requirements.txt`
│
└── src                <- Source code for use in this project.

```

## 5. Summary of Finding
### 5.1 Business Insight
Failure rate and financial impact
    28,782 of 204,557 installed orders failed (14.07%): 9.1% due to missing parts and 5.0% due to damaged panels. The rate is stable every month in 2023, so the problem is structural, not seasonal.
Failed installations account for Rp 38.5 billion (91.7%) of all valid refund claims (Rp 42.0 billion), equal to about 5.5% of 2023 product sales (Rp 702 billion). About Rp 18.6 billion was transferred back to customers; the rest was settled through product exchange or store credit.
7,189 failed orders (25%) were never returned, so the true cost of failed installations is likely higher than the refund value.

Root cause: two suppliers
    Two suppliers (UMKM Furnitur Ciputat and Mebel Rakyat Klaten) handle only 11.8% of installed orders but cause 30.6% of all failures and 40.9% of missing-parts cases. Their failure rate is ~36%, versus ~11% for the other 27 suppliers.
A logistic regression controlling for category, weight, store tier, certification, delivery lag, and price confirms the effect: orders from these two suppliers have 4.5× higher odds of failing (6.9× for missing parts, p < 0.001). Damaged panels show no supplier effect.
The high failure rate of Dining Tables (21%) disappears (to 11%) once these two suppliers are excluded, so the category itself is not the problem.

What is not the cause
    Delivery-to-installation lag (0–6 days), installer performance, supplier certification, customer–supplier distance, and whether the store is in the customer's city show no meaningful difference in failure rates.
Damaged panels are evenly spread (~5%) across every category, weight, store tier, and supplier type, so their cause is not captured in the current data.

Returns handling
    3,358 failed-installation claims are still "in process", with a median age of 182 days and an estimated exposure of Rp 7.1 billion.
Customer satisfaction stays at ~3.9 for returns resolved within 5 days, then drops steadily to ~2.3 after 15 days.

Omnichannel attribution
    Customers in cities with a DEC buy online twice as often (14.7% vs 6.9% of orders), and 75.2% of online buyers also shop at a DEC.
54.4% of online orders come from customers who bought at a DEC first, yet only 11% of those orders are recorded as "Walk-in" acquisition; 61% have no acquisition channel at all. DEC's contribution to online sales is therefore likely understated.
In this section, you can present the **actionable insights** derived from the analysis results.

### 5.2 Actionable Recommendation
In this section, you can offer **actionable business recommendations** to address the identified problems.

## 6. Contact
- Name: Fransiskus B Simanjorang
- Email: fransiskusjorang@gmail.com
- Linkedin: https://www.linkedin.com/in/fransiskusbs
