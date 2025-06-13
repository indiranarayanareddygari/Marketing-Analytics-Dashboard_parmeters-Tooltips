# 📊 Marketing Analytics Dashboard (Power BI)

This Power BI dashboard helps visualize and evaluate the performance of marketing campaigns across different **channels**, **devices**, and **regions**.

---

## 🧩 Key Features

* 📈 Dynamic KPIs: ROI, CTR, Conversion Rate, and Profit
* 🌀 **Metric Switcher** with Field Parameters for flexible visuals
* 📊 Performance breakdown by **Channel**, **Device**, **Campaign**, and **Region**
* 🧱 Custom **Funnel Chart** using DAX & DATATABLE
* 💡 Tooltips:

  * `Tooltip Page`: Extra KPIs on **Total Clicks by Campaign Name**
  * `Tooltip2`: Stepwise **Funnel Value by Channel**

---

## 📌 Dataset Used

* Simulated marketing dataset with fields like:

  * `Campaign Name`,`Device`, `Channel`, `Region`,`Campaign_ID`,`Impressions`,`Clicks`,`Conversions`,`Spend`,`Revenue`

---

## 📐 Key DAX Measures

```DAX
Profit = [Total Revenue] - [Total Spend]
ROI = DIVIDE([Total Revenue] - [Total Spend], [Total Spend], 0)
Click-Through Rate (CTR) = DIVIDE([Total Clicks], [Total Impressions], 0)
Conversion Rate = DIVIDE([Total Conversions], [Total Clicks], 0)
Cost Per Click (CPC) = DIVIDE([Total Spend], [Total Clicks], 0)
Cost Per Conversion = DIVIDE([Total Spend], [Total Conversions], 0)

Metrics_Parameter = {
  ("ROI", NAMEOF('Campaign_Performance'[ROI]), 0),
  ("Click-Through Rate (CTR)", NAMEOF('Campaign_Performance'[Click-Through Rate (CTR)]), 1),
  ("Conversion Rate", NAMEOF('Campaign_Performance'[Conversion Rate]), 2),
  ("Profit", NAMEOF('Campaign_Performance'[Profit]), 3)
}

Funnel_Steps = 
DATATABLE("Step", STRING, { {"Clicks"}, {"Conversions"}, {"ROI"} })

Funnel_Value = 
SWITCH(
  SELECTEDVALUE(Funnel_Steps[Step]),
  "Clicks", [Total Clicks],
  "Conversions", [Total Conversions],
  "ROI", [ROI]
)

Device_Performance_Value = 
SWITCH(
  SELECTEDVALUE(Metrics_Parameter[Metrics_Parameter]),
  "Clicks", [Total Clicks],
  "Conversions", [Total Conversions],
  "ROI", [ROI]
)

Channel Group = 
SWITCH(
  TRUE(),
  Campaigns[Channel] IN {"Email", "Social Media"}, "Digital Outreach",
  Campaigns[Channel] IN {"Search", "Display"}, "Ad Platforms",
  "Other"
)

Campaign Label = Campaigns[Campaign_Name] & " (" & Campaigns[Region] & ")"
Channel_Device = Campaigns[Channel] & " - " & Campaigns[Device]
Is Mobile Campaign = IF(Campaigns[Device] = "Mobile", TRUE(), FALSE())
```

---

## 📷 Dashboard Preview

### 🔹 Main Page

![Dashboard Main](images/dashboard-main.png)

### 🔹 Tooltip Pages

**Tooltip Page - Used in Total Clicks by Campaign Name**
![Tooltip 1](images/tooltip-page.png)

**Tooltip2 - Used in Funnel Value by Channel and Step**
![Tooltip 2](images/tooltip2.png)

---

## 🛠 Built With

* Power BI Desktop
* DAX & Calculated Tables
* Power Query
* Field Parameters & Custom Tooltips
* Performance Analyzer (used for optimization)


---

## 🔗 **Live Power BI Report**
https://app.powerbi.com/groups/me/reports/50bfc53b-0b6a-42fa-aef0-aaa449951ef6/0fead8111f136d82142b?experience=power-bi

--
## 👩‍💻 **Author**

**Indira Narayanareddygari**
📎 [LinkedIn](https://www.linkedin.com/in/indira-narayanareddygari-analyst061294/)
💼 *Data Analyst | Power BI Developer | SQL & Excel Specialist | Python Enthusiast*
