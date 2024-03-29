# Hypothesis-testing
Hypotheses testing
Kabirat Nasiru

Introduction
	Parametric tests are a category of statistical tests that assume certain characteristics about the distribution parameters of the population from which a sample has been extracted. They often require knowledge of specific population parameters, such as the mean or the standard deviation. These tests are powerful when their assumptions are met, as they can provide more precise estimates and stronger evidence to support a hypothesis.
	Univariate tests for normality assess if the distribution of data for a single variable closely resembles a normal distribution. Such tests are vital since the assumption of normality is a foundation for numerous parametric tests. Examples are the Shapiro-Wilk test, the Anderson-Darling test, and the Kolmogorov-Smirnov test. These methods help determine whether the data distribution significantly deviates from what is expected in a normal distribution.
	Hypothesis testing is a method of statistical inference used to decide whether there is enough evidence in a sample of data to infer that a certain condition is true for the entire population. It usually starts with a null hypothesis (H0), representing no effect or no difference, and an alternative hypothesis (H1), indicating a significant effect or difference. By testing we can either reject the null hypothesis in favor of the alternative or fail to reject the null hypothesis.
Dataset Selection
For this Analysis, we used a dummy crop data set that includes variables such as yield, fertilizer type, amount of rainfall, and temperature conditions. This dataset is suitable because it likely includes variables that can be assumed to follow a normal distribution, such as yield, which is important for conducting parametric tests in agricultural science. There is also a presence of both categorical (fertilizer type) and continuous variables (yield, rainfall) allows for a diverse set of statistical tests. The reason for choosing this is for understanding the effects of different variables on crop yield is crucial in agricultural research for optimizing farming practices.
Code
import numpy as np
import pandas as pd
from scipy.stats import shapiro, ttest_ind
import io  # Import the io module
from google.colab import files

# Upload the file
uploaded = files.upload()

# Read the CSV file into a pandas DataFrame
crop_dataset = pd.read_csv(io.BytesIO(uploaded['crop_dataset.csv']))

# Shapiro-Wilk test for normality on crop yield
stat, p = shapiro(crop_dataset['yield'])
print(f'Shapiro-Wilk Test Statistic: {stat}, p-value: {p}')
from scipy.stats import ttest_ind

# Separating yields by fertilizer type
yield_A = crop_dataset[crop_dataset['fertilizer_type'] == 'A']['yield']
yield_B = crop_dataset[crop_dataset['fertilizer_type'] == 'B']['yield']

# Independent Samples t-Test between yields of fertilizer types A and B
t_stat, p_val = ttest_ind(yield_A, yield_B)
print(f't-statistic: {t_stat}, p-value: {p_val}')
 Output
 
Results and Conclusion
Shapiro-Wilk Test for Normality- Test Statistic: 0.989, P-value: 0.621
The Shapiro-Wilk test results suggest that the crop yield data does not significantly deviate from a normal distribution, as indicated by the high p-value (> 0.05). This means we fail to reject the null hypothesis of normality, validating the assumption required for conducting parametric tests like the t-test on this dataset.
Independent Samples t-Test- T-statistic: -0.0126, P-value: 0.990
The t-test compares the mean yields between the two types of fertilizers (A and B). The very high p-value (0.990) is well above the conventional alpha level of 0.05, indicating a lack of significant difference in mean yields between the two fertilizer types. Thus, we fail to reject the null hypothesis, which posits that there is no significant difference in mean yields.
Conclusion from Sample
From the crop dataset with 100 observations, the crop yield data appears to follow a normal distribution, satisfying one of the key assumptions for conducting the t-test. The Independent Samples t-Test revealed no significant difference in mean yields between the two types of fertilizers used (p-value: 0.990). This suggests that, within the sample observed, the type of fertilizer does not significantly impact crop yield, therefore we suggest exploring additional variables that may influence crop success, such as soil conditions, climate, and agricultural practices.
