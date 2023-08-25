# Distance Data Codebase

[![License Badge](https://img.shields.io/github/license/DoctorGoose/PAMJ)](https://github.com/DoctorGoose/PAMJ/blob/main/LICENSE)
[![Issues Badge](https://img.shields.io/github/issues/DoctorGoose/PAMJ)](https://github.com/DoctorGoose/PAMJ/issues)
[![Pull Requests Badge](https://img.shields.io/github/issues-pr/DoctorGoose/PAMJ)](https://github.com/DoctorGoose/PAMJ/pulls)
[![Contributors Badge](https://img.shields.io/github/contributors/DoctorGoose/PAMJ)](https://github.com/DoctorGoose/PAMJ/graphs/contributors)
[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/dwyl/esta/issues)

Welcome to the Distance Data codebase! This codebase provides functionalities for analyzing and visualizing distance data between zip codes, as well as performing data preprocessing and manipulation tasks. It is designed to work with CSV files containing distance data and a zip code database.

## Functionalities

The main functionalities of the Distance Data codebase include:

1. Reading and writing distance data to/from CSV files.
2. Plotting histograms of distance data.
3. Filtering distance data based on desired state.
4. Computing patient/dispensary ratios and distance*patient values.
5. Adding latitude and longitude information to zip codes in dispensary and patient data.

## Installation

To use the Distance Data codebase, follow these steps:

1. Clone the repository:

   ```bash
   git clone https://github.com/DoctorGoose/PAMJ.git
   ```

2. Navigate to the codebase directory:

   ```bash
   cd PAMJ
   ```

3. Install the required dependencies:

   ```bash
   pip install pandas numpy matplotlib geopandas zipfile
   ```

## Usage

### Reading and Writing Distance Data

To read distance data from a CSV file, use the following code:

```python
import pandas as pd

df = pd.read_csv('Distance Data.csv')
```

To write distance data to a CSV file, use the following code:

```python
df.to_csv('Distance Data.csv', index=False)
```

### Plotting Histograms

To plot a histogram of the "Nearest Disp Distance" column in the distance data, use the following code:

```python
import matplotlib.pyplot as plt

plt.hist(df['Nearest Disp Distance'])
plt.show()
```

### Filtering Distance Data

To filter the distance data to include only zip codes from a desired state (e.g., Pennsylvania), use the following code:

```python
desired_state = 'PA'
filtered_df = df[df['state'] == desired_state]
```

### Computing Ratios and Values

To compute the patient/dispensary ratio and distance*patient values, use the following code:

```python
df['Patient/Dispensary Ratio'] = df.apply(lambda row: row['Patient Count'] if row['Dispensary Count'] == 0 else row['Patient Count']/row['Dispensary Count'], axis=1)
df['Distance*Patient'] = df['Nearest Disp Distance'] * df['Patient Count']
```

### Adding Latitude and Longitude Information

To add latitude and longitude information to zip codes in the dispensary and patient data, use the following code:

```python
df_dispo = pd.read_csv('DispoZipLatLong.csv')
df_pat = pd.read_csv('PatientZipLatLong.csv')

zipcodes_dispo = df_dispo['Zipcode'].unique()
zipcodes_pat = df_pat['Zipcode'].unique()

zipcode_counts_dispo = df_dispo['Zipcode'].value_counts()
zipcode_counts_pat = df_pat['Zipcode'].value_counts()

zipcode_counts_combined = pd.concat([zipcode_counts_dispo, zipcode_counts_pat], axis=1)
zipcode_counts_combined.columns = ['Dispensary Count', 'Patient Count']
```

## Contributors

The Distance Data codebase is maintained by [DoctorGoose](https://github.com/DoctorGoose).

## Contributing

Contributions to the Distance Data codebase are welcome! If you encounter any issues or have suggestions for improvements, please [open an issue](https://github.com/DoctorGoose/PAMJ/issues) on GitHub.

## License

The Distance Data codebase is licensed under the [MIT License](https://github.com/DoctorGoose/PAMJ/blob/main/LICENSE).
