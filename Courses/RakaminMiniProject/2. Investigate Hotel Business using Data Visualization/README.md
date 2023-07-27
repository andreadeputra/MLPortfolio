# Investigate Hotel Business using Data Visualization

This project is part of Rakamin Academy's portfolio building. In this project, I am given a dataset about hotel booking data distributed by Rakamin Academy modified after dataset from Kaggle's [Hotel Booking Demand](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand). The goal of this project is to gain business insight based on the dataset. That being said, the scope for this project will involve data preprocessing and data visualization.

## Data Pre-Processing
Based on quick data overview, here are the overview of what's being done in this step:
- Data Understanding
- Datatype Validation
- Duplicates Removal
- Missing Values Handling
- Handling Questionable Values

### Data Understanding
Before doing anything, it's best to try understand the dataset at hands. This dataset consists of 119390 rows and 29 columns. Unfortunately, the dataset given by Rakamin Academy doesn't include column's description. To avoid misinterpretations, I referenced the original dataset source for columns' descriptions. Since this dataset is already modified, there are some notable differences like:
- **meal**: this column's values are 'Breakfast', 'Dinner', 'Full Board', and 'No Meal'
- **city**: this column is adapted to contain cities in Indonesia instead of countries ID in the original source
- **market_segment**: this column is modified to have added variety of segments like 'Aviation' and 'Complimentary'

### Datatype Validation
Some columns in this dataset has datatype that doesn't fit with their descriptions. To make it simpler, here are the columns affected by this step:
- **is_canceled** and **is_repeated_guest** will be changed from int to object since they have binary value instead of numerical
- **children** will be changed from float to int because the it's a discreet value for counting people
- **agent** and **company** will be changed from float to object because they are not numerical values

### Duplicates Removal
There are 33261 rows of duplicates found in this dataset. These duplicates are dropped to avoid overrepresentations.

### Missing Values Handling
There are 4 columns with missing values in this dataset. Since the original dataset source used real data from mining, it's best to treat every missing values as intentional and try to interpret what they mean. Here are the approach taken for each columns:
- **children** will be filled with 0 because if a guest doesn't bring a child, it's not necessary to fill it in
- **city** will be filled with 'Others' because some guests' city of origin might be from other country
- **agent** and **company** will be filled with 'Not Applicable' since there are some bookings made without agent and/or company

### Handling Questionable Values
After doing some descriptive analysis and value checking, there are some notable change I've done to some columns. Here are some of the handling I've done:
- Removing booking transactions where total stay duration is 0
- Removing booking transactions where total guests staying is 0
- Changing 'Undefined' to 'No Meal' in **meal** by referencing original source
- Changing 'Complementary' to 'Complimentary' to follow general naming in hotel business
- Normalize **city** column's value by removing 'Kota' and 'Kabupaten' prefix

## Monthly Hotel Booking Analysis Based on Hotel Type
![Monthly Booking Trends based on Hotel Type](img/Graph01%20-%20Monthly%20Booking.png)

From the graph above, here are the findings:
- The trends can be segmented based on trimester, with second trimester having the best trends out of 3
- Hotel booking trends in Indonesia is mostly affected by holidays and academic calendar
- Peak timing for City Hotel is between June-August

## Impact Analysis of Stay Duration on Hotel Bookings Cancellation Rates
For this step, total duration of stay is made into 4 segments:
- Segment **A** for total stay duration of 1-3 days
- Segment **B** for total stay duration of 4-6 days
- Segment **C** for total stay duration of 7-9 days
- Segment **D** for total stay duration of 10+ days

![Cancellation Rate based on Hotel Type and Stay Duration](img/Graph04%20-%20Cancel%20Rate%20vs%20Duration.png)

From the graph above, here are the findings:
- Cancellation rate in City Hotel has positive correlation with stay duration, where the longer they stay duration is made on booking, the more likely it's being canceled
- Cancellation rate in Resort Hotel has no correlation with stay duration, which might mean Resort Hotel to be less prone to fraudulent bookings

## Impact Analysis of Lead Time on Hotel Bookings Cancellation Rate
For this step, lead time is categorized into:
- **Short**: consists of guests who book within 24 days lead time
- **Medium**: consists of guests who book within 125 days lead time
- **Long**: consists of guests who book beyond 125 days lead time

![Cancellation Rate based on Hotel Type and Lead Time](img/Graph07%20-%20Cancel%20Rate%20vs%20Lead%20Time.png)

From the graph above, here are the findings:
- Cancellation rate in City Hotel has positive correlation with lead time
- Cancellation rate in Resort Hotel has positive correlation with lead time on a smaller degree compared to City Hotel
- Low cancellation rate on shorter lead time might be attributed to cancellation policy
