# Improving Employee Retention by Predicting Employee Attrition Using Machine Learning
This project is part of Rakamin Academy's portfolio building. In this project, I am given a dataset about an employee database from a company. This company is dealing with a high attrition rate on their employees. The goal of this project is to analyze and predict resignation behaviour using machine learning model. The expected output will be to make business recommendations utilizing the resulting prediction.

## Data Preprocessing
The data consists of 287 rows of unique employees. There are some problematic values that will be handled in this step. The summary of what's done for this step will be listed below.

### Handling Missing Values
Based on descriptive analysis, here are the method in handling missing values on these columns:
- **SkorKepuasanPegawai** will be filled with mode
- **JumlahKeikutsertaanProjek** will be filled with 0
- **JumlahKeterlambatanSebulanTerakhir** will be filled with 0
- **JumlahKetidakhadiran** will be filled with 0
- **IkutProgramLOP** will be filled with 0
- **AlasanResign** will be filled with 'masih_bekerja'

### Standardizing Values
Based on descriptive analysis, here are the method in standardizing values on these columns:
- **StatusPernikahan**: '-' will be merged to 'Lainnya'
- **PernahBekerja**: 'yes' will be combined to '1'
- **TanggalResign**: '-' as the values indicating that employees are still working will be replaced with an arbitrary date of '2100-1-1'

## Annual Report on Employee Number Changes
Employee number changes will be analyzed by calculating total employees every year to see the changes due to hiring and resigning of employees. The summary for employee number changes can be seen on the graph below:

![Waterfall Chart for Employee Number Changes](img/waterfall.png)

Based on the graph above, here are the summary:
- Worst turnover can be observed at year 2018 with 11.29% turn over rate that's higher than 10% for [industry average turnover rate](https://www.linkedin.com/business/talent/blog/talent-strategy/industries-with-the-highest-turnover-rates#:~:text=compared%20with%20the%20overall%20average%20of%2010.6%25)
- The upward trend on employment rate might be attributed to the [growing amount of data worldwide](https://www.nasdaq.com/articles/a-decade-of-change%3A-how-tech-evolved-in-the-2010s-and-whats-in-store-for-the-2020s#:~:text=AI%20and%20Big%20Data%20Took%20Off) benefiting tech companies
- The slowing down of employment rate on 2015 and 2016 might be attributed to the company's [resource maturity](https://www.upwork.com/resources/stages-of-business-growth#resource-maturity:~:text=After%20a%20successful%20take%2Doff%20where%20the%20company%20has%20achieved%20the%20rapid%20growth%20it%20aimed%20for%2C%20the%20main%20concern%20of%20businesses%20entering%20the%20resource%20maturity%20stage%20is%20proper%20management%20of%20the%20financial%20gains%20from%20the%20last%20phase).
- The downward trend on year 2017 might be attributed to change in [world economy](https://money.cnn.com/2017/12/28/news/economy/jobs-2017/index.html#:~:text=Another%20sign%20of,plenty%20of%20options.)

## Resign Reason Analysis for Employee Attrition Management Strategy
Resign reason analysis will be done to understand the reason behind the increasing turnover rate since year 2017. As a starting point to understand the resigning reasons, I will be observing turnover rate based on job roles in the company.

![Retention by Job](img/Retention_by_job.png)
Based on the graph above, it can be observed that 'Data Analyst' has the highest turn over rate in this company at 50%. I will be focusing on getting a better understanding towards turnover rate in Data Analyst role.

![Sunburst Chart for Resigned Data Analyst](img/Sunburst.png)
Based on the sunburst chart above, here are the findings from Data Analyst turnover data:
- All of the resigned Data Analysts are in freshgraduate program
- For reasoning behind resignation, 75% answered 'toxic culture' while 25% answered 'internal conflict'
- Only 1 resigned Data Analysts is underperforming, while the other majority performs rather well

Here are the recommendations towards solving this problem:
- Reevaluate the company's leadership structure
- Fascilitate a safe space for employees to speak their concerns and act on it

## Machine Learning Modeling
While the company is on a downward trend in its employee number growth, the company needs a system to predict for the resign possibilities within current employees. This system will be made in order to solve the problems for the problem in the early stages, so they can start to map possible dissatisfied employees in the retention program to prevent more turnover. Machine learning will be used to help automate this detection system. However, some concern that has to be addressed will be possible bias in form of racism or gender-based decision. 

To understand what metrics to use, the business impact of each confusion matrix elements will be as follow:
- True Positive (TP): employees that will resign are predicted correctly
- True Negative (TN): employees that will NOT resign are predicted correctly
- False Positive (FP): employees that will NOT resign are predicted to resign, resulting in **retention program filled with staying employees**
- False Negative (FN): employees that will resign are predicted to NOT resign, resulting in **employees resigning without getting handled**

Based on that analysis, the metrics to focus on in this project will be recall to reduce FN.

The following columns will be dropped as a part of feature selection and addressing concern regarding discriminations:
- **JenisKelamin**
- **AsalDaerah**
- **HiringPlatform**
- **AlasanResign**
- **TanggalLahir**
- **TanggalHiring**
- **TanggalPenilaianKaryawan**
- **TanggalResign**

### Model Summary
Here is the machine learning model summary done for this project. The preprocessing pipeline can be checked in the notebook.

![Model Summary](img/Model_summary.png)

Based on that summary, I took a closer look on the top 4 models based on their recall scores. The confusion matrix for these 4 models can be seen below:

![Confusion Matrix](img/Conf_matrix.png)

Unfortunately, the trade offs will be somewhat big for this problem. Here are the analysis:
- There is no change in result for **Logistic Regression** between before and after tuning
- **KNN** has worse performance after tuning where TP and FP stays the same but getting worse in predicting TN
- Between **LogReg Base** and **KNN Base**, **KNN Base** is better due to having better precision

## Result Presentation with XAI
The last task in this project is to simulate result presentation to business users in the company. The metrics used in model evaluation above don't mean much to business users, thus the need for explanable AI. This is done to build trust and transparency to business users by explaining why the model decides its result predictions.

The XAI library used for this project will be SHAP. SHAP explains what features affects the result, how much the impact of each features for prediction, and whether it impacts negatively or positively.

![SHAP graph](img/shap.png)

From the graph above, here are the summary:
- Employees who do **NOT** work as **Software Engineer (Back End)** have **higher** probability to be labeled as resigning. This decision makes sense considering this job role is the majority in the company
- Employees whose marital status is **'not married'** have **lower** probability to be labeled as resigning. There might be some need to look further about this topic to understand this impact.
- Employees with **higher participations on projects** have **higher** probability to be labeled as resigning. This decision is somewhat understandable due to possible burnout from projects being the reason for resigning, or project management issues.
- **Outsource employees** have **lower** probability, while **Fulltime employees** have **higher** probability to be labeled as resigning. This makes sense considering fulltime employees work directly under the company's management system, so they are more exposed to possible management or work culture problems compared to outsource employees.

### Recommendations
Based on that insight, the recommendations are:
- Reevaluate projects in the company, especially in regards to compensation and appreciation towards employees with higher participations in them
- Reevaluate in-company's management system and check up on employees regularly to mediate internal conflict