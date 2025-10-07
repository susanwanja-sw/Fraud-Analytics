# Fraud-Analytics

This project blends analytics and curiosity to explore where customer growth meets financial risk.

https://github.com/user-attachments/assets/e65fc27d-04f7-4c6a-9ebe-cdea41c6f510


## Table of Contents
- [Objective](#objective)
- [Dataset Information](#dataset-information)
- [Data Preparation (Power Query)](#data-preparation-power-query)
- [Data Modeling (Power BI)](#data-modeling-power-bi)
- [Visualization & Insights](#visualization--insights)
- [Tools & Technologies](#tools--technologies)
- [How to View the Dashboard](#how-to-view-the-dashboard)
- [Key Findings & Recommendations](#key-findings--recommendations)
- [Acknowledgments](#acknowledgments)

## Objective
This project explores the intersection of customer growth and fraud risk through interactive Power BI dashboards.  
The goal was to uncover how legitimate spending behaviors overlap with potential fraud patterns, helping businesses not only grow smarter but stay safer.  

Key objectives included:
- Analyzing customer demographics, transactions, and spending habits to identify growth segments.  
- Detecting and visualizing patterns of confirmed fraud to highlight high-risk groups, merchants, and timeframes.  
- Comparing growth and fraud trends side by side to reveal where business opportunity meets operational risk.  
- Demonstrating how data-driven insights can inform smarter marketing, fraud prevention, and customer engagement strategies.

## Dataset Information
The dataset used for this project contains approximately **1,296,675 transaction records**, simulating real-world financial activity with both legitimate and fraudulent behaviors.  

Each record captures customer, merchant, and transaction-level details, allowing for deep analysis of spending patterns, geographic distribution, and potential fraud signals.

<details>
<summary><b> Dataset Information</b></summary>
  
**Key Columns:**

1. cc_num – Unique customer card number identifier  
2. Merchant – Business or vendor where the transaction occurred  
3. category – Spending category (e.g., grocery_pos, gas_transport, shopping_pos)  
4. amt – Transaction amount in USD  
5. Full Name, gender, job, dob – Customer demographic and occupation details  
6. city, state, lat, long – Customer geographic information  
7. trans_date, Hour, Minute – Timestamp and derived temporal details  
8. Age, Age Groups – Calculated age and categorized segments for trend analysis  
9. trans_num – Unique transaction identifier  
10. is_fraud – Binary flag (1 = Fraudulent, 0 = Legitimate)

<img width="1287" height="506" alt="image" src="https://github.com/user-attachments/assets/286d0998-0f13-4dfd-bcd1-b409db910a81" />

<img width="487" height="498" alt="image" src="https://github.com/user-attachments/assets/241269d4-1296-404d-9765-8ef978603473" />


**Dataset Size:**  
- **Rows:** 1,296,675  
- **Columns:** 17  
- **Target Variable:** is_fraud

**Data Source:**  
A simulated dataset for financial fraud detection, enriched with customer demographic and transaction behavior attributes.  
Used for analytical exploration, segmentation, and fraud trend visualization within Power BI.

</details>    

##  Data Preparation (Power Query)
Data cleaning and transformation were performed in **Power Query** to prepare the dataset for accurate analysis and modeling.  
The process focused on ensuring data consistency, removing irrelevant fields, and engineering useful analytical columns.

<img width="1366" height="730" alt="image" src="https://github.com/user-attachments/assets/b1ac8d6e-7c28-4074-a8c2-1fe598f5983e" />

<details>
<summary><b>Key Transformation Steps </b></summary>

1. **Data Type Correction:** Adjusted column data types (e.g., numeric, date, text) for accurate aggregation and visualization.  
2. **Column Renaming:** Standardized column names for better readability and consistency across reports.  
3. **Splitting Columns:** Used delimiters to extract relevant details from concatenated fields (e.g., separating date and time).  
4. **Value Replacement:** Corrected inconsistencies and standardized categorical values.  
5. **Merging Columns:** Combined related fields (e.g., names, addresses) for reporting clarity.  
6. **Filtering Rows:** Excluded incomplete and invalid entries to maintain clean data.  
7. **Feature Engineering:**  
   - Extracted **Hour** and **Minute** from timestamps.  
   - Calculated **Age** and **Age Groups** for segmentation.  
8. **Reordered Columns:** Optimized dataset structure for intuitive data modeling.

The end result was a well-structured and analysis-ready dataset, clean, consistent, and rich in derived insights, perfectly suited for fraud detection and behavioral analytics in Power BI.

</details>

## Data Modeling (Power BI)

I designed the data model in **Power BI** to support seamless analysis, accurate calculations, and interactive storytelling across all report pages.  
The model follows a **star schema**, connecting one main fact table with supporting dimension and measure tables for clarity and scalability.

<img width="770" height="536" alt="image" src="https://github.com/user-attachments/assets/4ceea1bc-5869-489a-9615-123cc6cda829" />


<details>
<summary><b>Model Components</b></summary>

1. **Fact Table: fraud data**  
   - Stores all transaction-level records along with customer, merchant, and fraud details.  
   - Includes engineered fields like **Age**, **Age Groups**, **Hour**, and **Minute** for segmentation and time-based analysis.  
   - Serves as the foundation for KPIs such as total transactions, total spend, and confirmed fraud cases.

2. **Date Table:**  
   - A dedicated time dimension created to enable **time intelligence functions** in DAX.  
   - Includes fields for **Day**, **Month**, **Quarter**, **Year**, and **Year-Month**.  
   - Linked to the trans_date column in the fact table using a **one-to-many relationship**, allowing for period-based insights and trend tracking.

3. **Measures Table (_Measures):**  
   - Central hub for all custom DAX calculations, keeping the model clean and easy to maintain.  
   - Contains key metrics such as:  
     - Total Transactions 
     - Total Spend  
     - Total Customers 
     - Conditional color measures (age_amt_Color, cat_amt_Color, Con_Transactions_Color) used to dynamically highlight top-performing segments.  
   - These measures power the visual interactivity and KPI storytelling across the dashboard.

**Relationships:**
- **fraud data ↔ Date Table** – connected via the trans_date field.  
- The relationship enables accurate filtering, drill-downs, and dynamic time comparisons.

Overall, I designed this model for **clarity, flexibility, and performance** ensuring that every visual in the report can adapt dynamically to filters, user selections, and data exploration.

</details>


## Visualization & Insights

This report is organized into three pages. Each page answers a different business question and is fully interactive with slicers for location, gender, and the `is_fraud` flag.

### 1) Customer Profile
**Purpose:** Identify the segments, categories, and locations that drive overall activity and potential growth.
<img width="1241" height="691" alt="image" src="https://github.com/user-attachments/assets/646a8970-e70b-46c0-bd4a-e43cf324e595" />

**What you see**
- **KPI cards:** Total Customers (≈983), Total Transactions (≈1.297M), Total Spent (≈91.22M).
- **Key Age Segments:** Column chart of transactions by age group. Ages **50–59** and **40–49** lead.
- **High-Spending Occupations:** Bar chart highlighting professions with the highest transaction counts (e.g., film/video editor appears as a top contributor in this dataset).
- **Top Cities for Expansion Opportunities:** Map showing cities with dense activity bubbles.
- **Categories with the Largest Revenue Potential:** Bar chart by category; **gas_transport** ranks #1 by transaction count (~131.66K), followed by **grocery_pos**, **home**, and **shopping_pos**.

**Why it matters**
- Focuses marketing and retention on proven high-value segments (age 50–59 / 40–49).
- Reveals categories and cities where investment will likely return the most volume.
- Surfaces occupations that respond well to offers, helping with audience targeting.

### 2) Spending Trends
**Purpose:** Understand when money moves and which segments/categories drive spend so operations and campaigns can be timed effectively.
<img width="1229" height="688" alt="image" src="https://github.com/user-attachments/assets/96d92bdd-6a09-467c-bb56-123563ac7861" />

**What you see**
- **Monthly Spend Trend:** Line chart showing spend across the year, with clear dips and recoveries.
- **Peak Spending Hours & Days:** Heatmap matrix by hour (0–23) vs. weekday; strongest activity clusters **between 12:00 and 23:00**, with notable evening and weekend pockets.
- **Age Groups Driving the Highest Customer Spend:** Bar chart of **total amount** by age group; **40–49** and **50–59** are consistently high.
- **Top Spending Categories and Merchants:** Bar chart of **total amount** by category; **grocery_pos** leads (~14.46M in this dataset), followed by shopping-related categories.

**Why it matters**
- Staffing and monitoring can be aligned to **afternoon–late-evening** peaks.
- Campaigns and pricing can be scheduled when customers are most active.
- Category insights help allocate budget to the products and partners that lift revenue.

### 3) Fraud Analysis
**Purpose:** Isolate confirmed fraud and show where risk concentrates so controls can be targeted without slowing growth.
<img width="1240" height="690" alt="image" src="https://github.com/user-attachments/assets/23d5ad9e-9f85-440a-b689-65f8f917276d" />

**What you see** *(page filtered to `is_fraud = 1`)*  
- **KPI cards (fraud only):** ~**8K** transactions, **3.99M** total spend, **762** customers involved.
- **Age Groups Most Involved in Confirmed Fraud:** Funnel showing the largest shares in **50–59** and **60–69**.
- **Cities Experiencing the Most Confirmed Fraud Activity:** Map highlighting geographic hotspots.
- **Individuals Linked to the Largest Fraud Amounts:** Bar chart surfacing high-impact cases.
- **Merchants with the Highest Confirmed Fraud Cases:** Trend/line visual; top merchants cluster around **47–49 cases**.

**Why it matters**
- Shows the **overlap between profitable segments and elevated risk** (e.g., 50–59).
- Points to **repeat-risk merchants and individuals** for enhanced scoring, monitoring, and rules.
- Enables time- and location-aware controls without blunt, conversion-killing blanket filters.

## Tools & Technologies

The project was built using a combination of Microsoft Power Platform tools and data analytics best practices to create a seamless, end-to-end analytical experience.

**Power BI Desktop & Power BI Service**  
Used to design, model, and visualize the data through interactive dashboards. Power BI Desktop handled development and DAX logic, while Power BI Service hosted and shared the final reports for easy access.

**Power Query**  
Handled all the heavy lifting during data preparation, cleaning over 1.29 million records, fixing data types, splitting and merging columns, and creating calculated time fields such as Hour and Minute for time-based analysis.

**DAX (Data Analysis Expressions)**  
Used to build calculated measures and KPIs such as Total Transactions, Total Spend, and Fraud Rate. Also applied dynamic color logic to highlight top-performing segments and critical fraud indicators.

**Kaggle Dataset**  
The dataset originated from a simulated financial fraud detection dataset on Kaggle, enriched with customer demographics and transaction attributes for pattern discovery and segmentation.

**Azure Maps (Power BI Visual)**  
Enabled visualization of city-level activity, helping to spot regional opportunities and fraud clusters on an interactive geographic map.

**GitHub**  
Serves as the version-controlled home for this project hosting the `.pbix` file, documentation, and assets. The repository also includes the README, screenshots, and structured folders for transparent sharing and collaboration.

Together, these tools built a full analytical workflow from raw transactional data to a visually engaging, insight-rich Power BI dashboard that connects customer growth and fraud detection in one unified story.

## How to View the Dashboard

The Power BI dashboard was designed to be fully interactive and easy to navigate, allowing users to explore insights naturally through built-in buttons and slicers.

**Navigation Panel**  
Located on the left side of the report, the navigation panel enables smooth movement between the three key pages:  
- **Customer Profile** – Highlights customer segments, occupations, and top-performing categories.  
- **Spending Trends** – Visualizes spending patterns over time, revealing engagement peaks and high-value categories.  
- **Fraud Analysis** – Focuses on confirmed fraud activity, showing high-risk demographics, locations, and merchants.  

Each navigation button is fully interactive, letting viewers switch between pages with a single click.

**Slicers (Top Filters)**  
At the top of each page, slicers allow dynamic filtering across the entire report:  
- **City** – View data for specific geographic locations.  
- **Gender** – Compare male and female customer activity.  
- **is_fraud** – Toggle between all transactions (`0`) and confirmed fraudulent ones (`1`) to isolate fraud-related insights.  

Selecting a slicer updates every visual in real time, creating a smooth, exploratory experience.

**Guide Button**  
The **Guide** button opens an on-screen tutorial overlay designed within Power BI to walk new users through the report.  
When activated, it highlights and explains key areas navigation buttons, slicers, using descriptive tooltips.  
This makes it easy for anyone, even non-technical users, to understand how to explore the dashboard effectively.

**Reset Button**  
The **Reset** button clears all filters and slicer selections, restoring the dashboard to its original default state.  
It’s especially useful after deep exploration or comparisons between multiple filters.

**External Links**  
Additional links in the **Links** section provide quick access to external pages:  
- **LinkedIn** and **TikTok** – To connect professionally or view related dashboard content.  
- **Guide** – To reopen the on-screen instructions.  
- **Reset** – To revert tthe initial clean dashboard view.

**How to Access the Dashboard**  
The dashboard is published on **Power BI Service** and can be viewed directly online.

1. Click the **Power BI link** provided in this repository to open the report.  
2. Once loaded, use the **Guide** button for a step-by-step walkthrough of key features and visuals.  
3. Interact with slicers at the top (City, Gender, is_fraud) to filter insights dynamically.  
4. Navigate through pages using the left sidebar (**Customer Profile**, **Spending Trends**, **Fraud Analysis**).  
5. Click **Reset** anytime to return the dashboard to its original state for a fresh view.

[https://app.powerbi.com/view?r=eyJrIjoiOGE5NjUzZWEtMzUwYi00ZjQyLTg0ZDMtMmYwOGJlN2Y4MGZjIiwidCI6IjcwODkwZDkxLTc1NmQtNDk2Yi04NjJmLWYyZTA2NTEzYjE2ZiJ9]

This setup makes it simple to explore insights directly in your browser, no installation or setup required.

## Key Findings & Recommendations

This dashboard connects two sides of business growth driving customer engagement while keeping transactions secure.  
By analyzing over 1.29 million transactions, several clear trends and actionable insights emerged.

### Key Findings
- **Age Segments That Drive Growth:**  
  Customers aged **50–59** and **40–49** generate the highest number of transactions and spending volume, representing the core growth demographic.

- **Spending Behavior:**  
  The majority of spending occurs between **12:00 and 23:00**, with noticeable peaks in the early evening.  
  **Grocery, home, and gas** categories dominate total spend, showing everyday convenience and household needs as key motivators.

- **Fraud Risk Concentration:**  
  When filtered for confirmed fraud (is_fraud = 1), the same 50–59 and 60–69 age groups appear most frequently.  
  Fraudulent activity clusters around a few cities and merchants suggesting recurring behavioral and system vulnerabilities.

### Recommendations

**1. Grow Responsibly, Target, Don’t Exploit.**  
Market actively to high-spending age groups (40–59) with loyalty programs, tailored offers, and value-driven campaigns.  
However, pair every marketing push with fraud-aware communication, reminding users to verify links, report suspicious activity, and use secure payment methods.

**2. Strengthen Fraud Prevention During Peak Hours.**  
Deploy fraud detection resources between **noon and midnight**, when most spending and potential fraud occurs.  
Implement real-time transaction monitoring and anomaly alerts for unusual spending bursts during these hours.

**3. Prioritize Merchant Risk Scoring.**  
A small set of merchants show repeated fraud incidents.  
Introduce a **risk-based merchant scoring system** that adjusts verification thresholds dynamically based on transaction patterns and historical fraud rates.

**4. Blend Marketing and Security Data.**  
Encourage collaboration between **marketing** and **fraud analytics teams**.  
Understanding who buys the most and when can help design promotions that attract genuine customers while flagging suspicious behavior early.

**5. Educate and Empower Customers.**  
Fraud prevention isn’t just a technical task it’s a communication opportunity.  
Use the same channels that drive engagement (emails, in-app messages, social media) to educate customers on safe spending habits.

By aligning marketing insights with fraud analytics, a business can do both: **make people spend smarter** and **stay protected while doing it**.  
This balance between growth and guardrails is what keeps customer trust, and revenue growing together.

## Acknowledgments

This project was inspired by real-world fraud analytics challenges where the balance between customer growth and transaction security defines business success.  

Special thanks to:  
- **Kaggle** for providing the open-source simulated fraud dataset that made this exploration possible.  
- **Microsoft Power BI Community** for continuous learning resources and DAX best practices.  
- **Design inspiration** drawn from modern dashboard storytelling blending analytics with accessibility and guided user experience.  

Additional appreciation goes to everyone in the data community who shares insights, visuals, and templates that push analytics beyond numbers turning data into decisions.

 
All rights reserved. © 2025 susanwanja

