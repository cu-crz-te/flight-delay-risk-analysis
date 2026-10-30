# Flight Delay Risk Across Departure Conditions

How does departure delay risk vary with time, airline, route and demand conditions? For our Business Analytics class, we used 2024 U.S. domestic flight records and logistic regression to explore how departure conditions relate to delay risk. We also compared how airlines responded across two modeled scenarios.

[Portfolio case study](https://emily-chen-portfolio.woollymaple7.chatgpt.site/#/work/flight) · [Dataset on Kaggle](https://www.kaggle.com/datasets/hrishitpatil/flight-data-2024)

## Key findings

- **Time of day:** Evening departures showed higher delay risk; holiday status had a negative adjusted association in the main-effects model.
- **Carrier differences:** We found that the relationship between delay risk and departure time or distance varied by airline, making a single ranking less useful.
- **Scenario sensitivity:** Our model estimated Southwest's delay probability at 9.2% and 37.5% in two defined scenarios, a 4.08× ratio. SkyWest, Republic and Hawaiian had the smallest absolute increases in the comparison.

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

- `flight-delay-analysis.Rmd`: analysis notebook, translated into English from the original R Markdown
- `team-report.pdf`: original class assignment, in Chinese

## Running the analysis

Our notebook requires R and the packages `car`, `formattable`, `fBasics`, `dplyr`, `tidyr`, `ggplot2`, and `scales`. It installs missing packages itself. Download the 2024 dataset from Kaggle, follow its terms, and place `flight_data_2024.csv` in the working directory. It also reads a separate `flight_data_2024_sample_200k.csv` from the working directory; that sample is not included. Open the notebook in RStudio and run its chunks in sequence after supplying both files. Review paths and package installation before running. We wrote the report in Chinese for our class assignment, and it remains in its original language. For this repository, the notebook’s narrative, comments, and messages have been translated into English without changing the analysis logic. The translated notebook has not been fully rerun.

## Reproducibility and limitations

- We used a random sample of 200,000 records for modeling. The notebook reads an existing sample file, so the exact sample cannot be recreated without that file or the original sampling procedure and seed.
- The notebook defines `is_delayed` as `dep_delay > 15`, while the report discusses a 15-minute threshold. Exactly 15 minutes is excluded by this implementation. Check this distinction before interpreting or rerunning results.
- Our full-year back-test uses the same year as the modeling sample, so it is not an independent holdout. The reported accuracy should also be compared with a majority-class baseline.
- Weather and several operational factors were not directly measured. The holiday and peak variables are engineered definitions in the notebook; inspect them before comparing with external definitions.
- Data is not included. Package versions and the original execution environment are not locked; exact numerical reproduction is not guaranteed.

## Credits

We completed this project as a team for a Business Analytics class at National Taiwan University.
