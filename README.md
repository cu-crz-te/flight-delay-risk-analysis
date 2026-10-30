# Flight Delay Risk Across Departure Conditions

How does departure delay risk vary with time, airline, route and demand conditions? This academic team project uses 2024 U.S. domestic flight records and a logistic regression model to compare conditional delay risk and airline sensitivity across scenarios.

[Portfolio case study](https://emily-chen-portfolio.woollymaple7.chatgpt.site/#/work/flight) · [Dataset on Kaggle](https://www.kaggle.com/datasets/hrishitpatil/flight-data-2024)

## Key findings

- **Time of day:** Evening departures showed higher delay risk; holiday status had a negative adjusted association in the main-effects model.
- **Carrier differences:** The selected model included carrier interactions with departure period and distance, so a single airline ranking can obscure conditional differences.
- **Scenario sensitivity:** The report estimated Southwest's delay probability at 9.2% and 37.5% in two defined scenarios, a 4.08× ratio. SkyWest, Republic and Hawaiian had the smallest absolute increases in the comparison.

These are model-based associations and scenario estimates, not causal effects or evidence of operational changes.

## Methods

1. **Data Cleaning:** Excluded cancelled and diverted flights and removed unsuitable or incomplete records before modeling
2. **Exploratory Data Analysis:** Examined distributions and delay patterns across time, routes, and airlines to inform predictor selection
3. **Variable Transformation:** Log-transformed distance, grouped airports and departure times, and created holiday and peak indicators
4. **Main-effects Logistic Modeling:** Built a binomial logistic GLM to estimate departure delay probability using timing, route, demand, and carrier variables
5. **Model Selection (Backward AIC):** Evaluated a main-effects specification with backward AIC selection
6. **Interaction Testing:** Tested whether relationships differed across conditions, including carrier by distance, time, peak, and holiday
7. **Model Comparison (LRT & AIC):** Compared nested models with likelihood-ratio tests and candidate specifications with AIC; the selected model included carrier-by-distance and carrier-by-time interactions
8. **Model Diagnostics:** Examined collinearity, dispersion, residuals, and influential observations
9. **Statistical Inference:** Interpreted coefficients, interaction terms, and significance tests in the context of the model
10. **Scenario & Sensitivity Analysis:** Compared modeled probabilities under defined lower- and higher-risk conditions using absolute and relative sensitivity
11. **Full-year Back-testing:** Compared reported fitted-sample and full-year accuracy. The latter is a same-year back-test, not an independent holdout; its code is commented out in the supplied notebook

## Repository contents

- `flight-delay-analysis.Rmd`: original analysis notebook, with Chinese comments
- `team-report.pdf`: original team report, in Chinese

## Running the analysis

The original notebook requires R and the packages `car`, `formattable`, `fBasics`, `dplyr`, `tidyr`, `ggplot2`, and `scales`. It installs missing packages itself. Download the 2024 dataset from Kaggle, follow its terms, and place `flight_data_2024.csv` in the working directory. The notebook also reads a separate `flight_data_2024_sample_200k.csv` from the working directory; that sample is not included. Open the notebook in RStudio and run its chunks in sequence after supplying both files. Review paths and package installation before running. The original code and report are preserved; a complete execution has not been verified here.

## Reproducibility and limitations

- The report describes a 200,000-record random sample, but the supplied notebook reads an existing sample file. The exact sample cannot be reproduced without the original file or its sampling procedure and seed.
- The notebook defines `is_delayed` as `dep_delay > 15`, while the report discusses a 15-minute threshold. Exactly 15 minutes is excluded by this implementation. Check this distinction before interpreting or rerunning results.
- The report's full-year back-test includes the same year as the modeling sample; it is not an independent holdout. Reported accuracy should be assessed against a majority-class baseline.
- Weather and several operational factors were not directly measured. The holiday and peak variables are engineered definitions in the notebook; inspect them before comparing with external definitions.
- Data is not included. Package versions and the original execution environment are not locked; exact numerical reproduction is not guaranteed.

## Credits

Team academic project for Business Analytics at National Taiwan University. Team member names and student IDs have been removed from the report. No license is specified; contact the authors before reuse.
