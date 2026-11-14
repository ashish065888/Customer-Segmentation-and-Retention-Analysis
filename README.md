# RFM-and-Cohort-Retention-Analysis

## Project Overview
This project explores a retail company's transaction history to understand customer value, purchasing patterns, and retention. It combines Recency–Frequency–Monetary (RFM) segmentation with acquisition-cohort analysis and a retrospective comparison of customers who eventually fall into different RFM segments. The objective is to identify customer groups worth prioritizing and generate hypotheses for loyalty and re-engagement campaigns—not to claim that any campaign has already improved retention.

## Business Problem

An e-commerce company wants to improve customer retention and maximize customer lifetime value. However, it lacks a clear understanding of its customer base, including which customers contribute the most revenue, how customer retention varies over time, and what purchasing behaviors distinguish high-value customers from those who eventually become inactive.

Without these insights, the company may struggle to prioritize customer segments, allocate marketing resources effectively, and identify opportunities to encourage repeat purchases.

**The objective of this project is to analyze historical transaction data to segment customers based on purchasing behavior, evaluate retention patterns, and identify early repeat-purchase behaviors associated with high-value customers.** The findings will help inform data-driven customer engagement, loyalty, and retention strategies.

## Business Objective

- Identify high-value customers and their revenue contribution
- Understand how customer retention changes across acquisition cohorts	
- Compare the purchasing journeys of different customer segments	
- Determine whether high-value customers make repeat purchases sooner
- Identify potential opportunities for early customer engagement

## Key Business Questions

1. Which customer segments contribute the most revenue, and how is revenue distributed across segments?
2. How does customer retention change over time, and how does it vary across acquisition cohorts?
3. How do customers who eventually become Champions or Loyal Customers differ in their purchasing behavior from other segments?
4. How quickly do customers make their second purchase, and how does this vary across RFM segments?
5. At which stages of the customer journey could the business test targeted interventions to encourage repeat purchases and improve long-term retention?

## Dataset

**Source:** [UCI Online Retail Dataset](https://archive.ics.uci.edu/dataset/352/online+retail)

- Real transactional data from a UK-based online retailer.
- Contains invoice-level transactions with product, quantity, price, date, customer, and country information.
- Time period: December 2010 to December 2011.
- Approximately 541,909 transactions and 8 columns. [142][147]

### Key columns used
| Column | Description |
|---|---|
| `InvoiceNo` | 6-digit transaction ID. Codes starting with "C" mean a cancellation. |
| `StockCode` | 5-digit product ID. |
| `Description` | Product name |
| `Quantity` | Number of units purchased |
| `InvoiceDate` | Date and time of transaction |
| `UnitPrice` | Price per unit in British Pounds (£) |
| `CustomerID` | 5-digit unique customer ID |
| `Country` | Customer country |


## Tools Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook

## Data Cleaning and Preprocessing
The following data cleaning operations were performed:
1. Rows with missing CustomerIDs are removed.
2. Identified and removed duplicate rows.
3. Removed cancelled invoices.
4. Checked each column for mixed data types and corrected wherever needed.
5. Resolved inconsistent description (extra spaces, commas, and abbreviations) by mapping all variations to a single standardized name based on StockCode and Description renamed to ProductName.

## Key Analysis Sections

### Sales Performance
1. Top countries by revenue
   
   <img width="600" height="400" alt="Revenue by country" src="https://github.com/user-attachments/assets/47fea14c-8b48-4fd4-b7e8-cd83b0efb470" />

2. Top products by revenue

   <img width="600" height="400" alt="Revenue by product" src="https://github.com/user-attachments/assets/0880d7a9-b4bb-4ebf-bf18-7c0d6377b326" />

3. Revenue trend over months

   <img width="600" height="400" alt="Revenue trend over months" src="https://github.com/user-attachments/assets/8d7d5f83-4487-4bee-99ad-e1e5ba64474f" />

**Key Findings:**
- The monthly revenue trend reveals that there is sudden spike in sales from september to november. This sudden increase might be due to festive season.
  
### RFM Customer Segmentation
Computed three customer-level measures:
| Measure | Definition | Business meaning |
|---|---|---|
| **Recency** | Days since last purchase, measured from one day after the latest transaction | How recently a customer purchased |
| **Frequency** | Number of distinct invoices | How often a customer ordered |
| **Monetary** | Sum of sales | How much revenue a customer generated |

Assigned R, F, and M scores using quintile-based approaches, then applied rule-based conditions to classify customers into seven segments: Champions, Loyal Customers, New Customers, Big Spenders (Low Freq), At Risk, About to Sleep / Drifting, and Lost.

<img width="500" height="400" alt="Customer Segment distribution" src="https://github.com/user-attachments/assets/d34fb1dc-faa7-4c66-abc0-601934915eb2" /> <img width="500" height="400" alt="Customer segment contribution in revenue" src="https://github.com/user-attachments/assets/c21d8655-4eaf-435d-98f1-e1f4c0cbb9bf" />

**Key Findings:**
- Champions and Loyal Customers together account for 82% of analyzed revenue. Maintaining strong relationships with these customer groups is therefore commercially important.

### Cohort Analysis
Grouped customers by their first-purchase month. For each cohort, calculated the proportion of customers who placed an order in each subsequent calendar month and visualized the result with retention heatmaps.
> Retention definition: Percentage of the original cohort purchasing in a given later month. This is monthly purchasing activity, not necessarily uninterrupted month-over-month repeat buying.

<img width="600" height="600" alt="Cohort retention Heatmap" src="https://github.com/user-attachments/assets/fe84f1ab-eca2-4a55-8829-f588b8f54eeb" />

**Key Findings:**
- The most significant drop in customer retention occurs after the first month (Month 0 to Month 1) across almost all cohorts.
- The Dec 2010 cohort shows the most consistent and highest long-term retention compared to other months. By Month 11, it remarkably spikes to 50.3%.
- Several early cohorts (Dec 2010, Jan 2011) show a noticeable bump in retention around Month 10 and Month 11 (which corresponds to late 2011), suggesting a seasonal trend, holiday effect, or successful reactivation campaign during that period.
  
### Customer Purchase Behavior & Retention Analysis

#### 1. Retention Analysis by RFM Segment

**Objective:** Understand how customers who eventually became Champions, Loyal Customers, or other RFM segments behaved over time, starting from their first purchase.

**Methodology:**
- Grouped customers according to their final RFM segment.
- Tracked monthly purchasing activity relative to each customer's first purchase (Month 0).
- Calculated the percentage of customers making purchases in each subsequent month.
- Compared retention curves across customer segments to identify differences in purchasing behavior.

<img width="600" height="500" alt="Retention Curves by RFM Segment" src="https://github.com/user-attachments/assets/aa1364ca-fd92-480a-80fc-00df82f77caa" />



**Key Findings:**
- Champions demonstrated the strongest early repeat-purchase behavior, with **46.62% returning in Month 1**, compared with **25.94% of Loyal Customers**.
- At Risk customers showed relatively strong early purchasing activity, with **29.39% returning in Month 1**, suggesting that some customers who eventually became inactive had initially engaged with the business.
- Lost customers demonstrated extremely low repeat-purchase activity, with only **1.93% returning in Month 1**.

**Business Insight:**

Early purchasing behavior differs across eventual customer segments. The relatively strong initial engagement of At Risk customers suggests an opportunity to investigate when previously active customers begin disengaging.

---

#### 2. Time to Second Purchase Analysis

**Objective:** Determine whether customers who eventually become Champions or Loyal Customers make their second purchase sooner than other customer segments.

**Methodology:**
- Identified each customer's first and second distinct orders.
- Calculated the number of days between the first and second purchases.
- Compared the median time to second purchase across RFM segments.

**Key Findings:**

| Customer Segment | Median Days to Second Purchase |
|---|---:|
| Champions | **37.13** |
| At Risk | 54.92 |
| Loyal Customers | 69.85 |
| Lost | 82.99 |
| About to Sleep / Drifting | 99.94 |
| New Customers | 101.01 |
| Big Spenders (Low Freq) | 102.89 |

- Champions made their second purchase fastest, with a median of **37 days**, approximately 33 days earlier than Loyal Customers.
- At Risk customers had the second-shortest median time (55 days), indicating relatively strong early repeat-purchase behavior despite their eventual classification.
- The results suggest that the time to second purchase may be a useful indicator of future customer engagement.

**Business Insight:**

Faster second purchases are associated with eventual Champion status. Encouraging repeat purchases early in the customer journey could be explored as a retention strategy, subject to experimental validation.

---

#### 3. Cumulative Second-Purchase Conversion Analysis

**Objective:** Identify how quickly customers make their second purchase after acquisition and explore potential intervention windows for encouraging repeat purchases.

**Methodology:**
- Calculated the percentage of customers completing their second purchase within **7, 14, 30, 60, and 90 days**.
- Included only customers with at least 90 days of observable transaction history to ensure a consistent comparison population.
- Compared cumulative second-purchase conversion across eventual RFM segments.

<img width="700" height="400" alt="image" src="https://github.com/user-attachments/assets/f224530a-40d9-484b-8388-238cd32bd91b" />


**Key Findings:**

| Days Since First Purchase | Champions | At Risk | Loyal Customers |
|---|---:|---:|---:|
| 7 Days | 16.75% | 13.73% | 7.51% |
| 14 Days | 26.51% | 19.50% | 10.33% |
| 30 Days | **41.05%** | 29.80% | 16.90% |
| 60 Days | 64.50% | 53.20% | 32.39% |
| 90 Days | 76.56% | 67.39% | 47.73% |

- By Day 30, **41.05% of eventual Champions** had made a second purchase, compared with **16.90% of Loyal Customers**.
- Champions consistently demonstrated higher cumulative second-purchase conversion across all measured time windows.
- At Risk customers also showed strong early repeat-purchase behavior, with **67.39% completing a second purchase within 90 days**.

**Business Insight:**

The first 30 days after acquisition represent a promising period to investigate for customer engagement initiatives. Targeted reminders, personalized recommendations, or second-purchase incentives could be tested among customers who have not yet purchased again.


## Business Recommendations

Based on the findings, the following initiatives could be explored:

1. **Encourage early repeat purchases:** Experiment with personalized recommendations or second-purchase incentives during the first 30 days after acquisition.
2. **Improve retention of previously engaged customers:** Investigate the purchasing journeys of At Risk customers to identify when engagement begins to decline.
3. **Protect high-value customer relationships:** Introduce or test loyalty benefits for customers displaying strong repeat-purchasing behavior.
4. **Measure campaign effectiveness:** Use controlled A/B tests to determine whether these interventions improve second-purchase conversion, long-term retention, and incremental profit.



