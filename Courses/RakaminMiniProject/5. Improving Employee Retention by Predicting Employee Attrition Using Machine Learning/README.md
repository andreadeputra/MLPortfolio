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

