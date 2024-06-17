# Sea Level Predictor

This is the boilerplate for the Sea Level Predictor project. Instructions for building your project can be found at https://www.freecodecamp.org/learn/data-analysis-with-python/data-analysis-with-python-projects/sea-level-predictor

### Project Description: Sea Level Predictor

The Sea Level Predictor project involves analyzing historical data of global sea levels and predicting future sea levels. Using a dataset of sea level measurements, you will create visualizations to illustrate trends and fit linear regression models to project future sea levels.

### Objectives

1. **Read and Process the Dataset**: Load the dataset from a CSV file and process the date and sea level measurements.
2. **Visualize Historical Sea Levels**: Create a scatter plot of historical sea level data.
3. **Fit Regression Models**: Fit a linear regression model to the historical data to predict future sea levels.
4. **Extend Predictions**: Use the regression model to predict sea levels up to the year 2050.
5. **Return the Visualization**: Display or save the plot with the historical data and future predictions.

### Dataset

The dataset contains the following columns:
- `Year`: The year of the sea level measurement.
- `CSIRO Adjusted Sea Level`: The adjusted sea level measurement from CSIRO.

### Function Specifications

1. **Input**: Path to the CSV file.
2. **Output**: A plot showing:
   - A scatter plot of the historical sea level data.
   - A line of best fit for the entire dataset.
   - A second line of best fit using data from the year 2000 onwards.
   - Predictions of sea levels up to the year 2050.

### Steps to Follow

1. **Load the Data**:
   - Use pandas to read the CSV file into a DataFrame.

2. **Process the Data**:
   - Ensure that the `Year` column is numeric and the `CSIRO Adjusted Sea Level` column contains valid float values.

3. **Visualize Historical Sea Levels**:
   - Create a scatter plot of the `Year` vs. `CSIRO Adjusted Sea Level`.

4. **Fit Regression Models**:
   - Fit a linear regression model to the entire dataset.
   - Fit a second linear regression model to data from the year 2000 onwards.

5. **Extend Predictions**:
   - Use the models to predict sea levels up to the year 2050.

6. **Create the Plot**:
   - Plot the historical data, both lines of best fit, and the future predictions.

7. **Enhance the Plot**:
   - Add labels, titles, legends, and grid lines for better readability.

8. **Save or Display the Plot**:
   - Save the plot to a file or display it in an interactive window.

### Example Implementation

Here's an implementation using `matplotlib`, `pandas`, and `numpy`:

```python
import pandas as pd
import matplotlib.pyplot as plt
from scipy.stats import linregress

def draw_plot():
    # Read data from file
    df = pd.read_csv('epa-sea-level.csv')
    
    # Create scatter plot
    plt.figure(figsize=(10, 6))
    plt.scatter(df['Year'], df['CSIRO Adjusted Sea Level'], color='blue', label='Original Data')
    
    # Create first line of best fit
    result = linregress(df['Year'], df['CSIRO Adjusted Sea Level'])
    years_extended = pd.Series([i for i in range(1880, 2051)])
    sea_levels_predicted = result.intercept + result.slope * years_extended
    plt.plot(years_extended, sea_levels_predicted, 'r', label='Fit: 1880-2050')
    
    # Create second line of best fit
    recent_df = df[df['Year'] >= 2000]
    result_recent = linregress(recent_df['Year'], recent_df['CSIRO Adjusted Sea Level'])
    years_recent = pd.Series([i for i in range(2000, 2051)])
    sea_levels_predicted_recent = result_recent.intercept + result_recent.slope * years_recent
    plt.plot(years_recent, sea_levels_predicted_recent, 'g', label='Fit: 2000-2050')
    
    # Formatting the plot
    plt.title('Rise in Sea Level')
    plt.xlabel('Year')
    plt.ylabel('Sea Level (inches)')
    plt.legend()
    plt.grid(True)
    
    # Save plot and return data for testing (DO NOT MODIFY)
    plt.savefig('sea_level_plot.png')
    return plt.gca()

# Example usage
draw_plot()
```

### Expected Output

The expected output will be a PNG file named `sea_level_plot.png` that includes:
- A scatter plot of historical sea level data.
- A red line of best fit for the entire dataset.
- A green line of best fit for the data from 2000 onwards.
- Predictions of sea levels up to the year 2050.

### Detailed Breakdown

1. **Reading the Data**:
   - Load the CSV file into a DataFrame using pandas.
   - Verify and clean the data if necessary.

2. **Creating Scatter Plot**:
   - Use `plt.scatter()` to plot the `Year` vs. `CSIRO Adjusted Sea Level`.

3. **Fitting Regression Models**:
   - Use `linregress()` from `scipy.stats` to fit a linear regression model to the entire dataset.
   - Calculate the predicted sea levels for each year from 1880 to 2050 using the model.
   - Repeat the process for data from 2000 onwards.

4. **Plotting the Lines of Best Fit**:
   - Use `plt.plot()` to draw the line of best fit for the entire dataset.
   - Use a different color to draw the line of best fit for data from 2000 onwards.

5. **Enhancing the Plot**:
   - Add a title, labels for the x and y axes, and a legend to distinguish between the two lines of best fit.
   - Add grid lines for better readability.

6. **Saving the Plot**:
   - Save the plot to a file named `sea_level_plot.png`.

This project provides practice with data visualization, linear regression, and prediction using historical data. It helps in understanding trends in sea level changes and projecting future changes based on historical patterns.
