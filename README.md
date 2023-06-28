# ANOVA with FDR Correction (anova_fdr.py)

This script performs an Analysis of Variance (ANOVA) on a dummy dataset consisting of results from three different treatments, and applies False Discovery Rate (FDR) correction to the resulting p-values.

## Script Stages:

### 1. Dataset Creation:

The script first creates a dummy dataset. The dataset consists of the results of three different treatments (`T1`, `T2`, `T3`), each applied to 30 patients. The results are simulated as normally distributed random variables with specified mean (`loc`) and standard deviation (`scale`).

pythonCopy code

`treatment1 = np.random.normal(loc=5, scale=2, size=30)
treatment2 = np.random.normal(loc=6, scale=2, size=30)
treatment3 = np.random.normal(loc=5.5, scale=2, size=30)` 

### 2. ANOVA Test:

The script then performs an ANOVA test on the dummy dataset to see if there's a significant difference between the means of the treatments. The null hypothesis is that all the means are the same. The F-value and p-value are printed. The F-value measures the variance between the group means over the variance within the groups. The p-value measures the probability of getting an F-value as extreme as the observed one under the null hypothesis.

pythonCopy code

`fvalue, pvalue = stats.f_oneway(data[data['Treatment']=='T1']['Result'], 
                                data[data['Treatment']=='T2']['Result'],
                                data[data['Treatment']=='T3']['Result'])` 

### 3. FDR Correction:

Finally, the script performs FDR correction on the p-value from the ANOVA test. This correction is necessary when performing multiple comparisons to control the expected proportion of false positives. In other words, it reduces the chances of type I errors. The Benjamini/Hochberg method is used for the correction.

pythonCopy code

`_, pvals_fdr, _, _ = multipletests(pvalue, method='fdr_bh')` 

## Result:

The script prints out the F-value and p-value from the ANOVA test, and the FDR-corrected p-value. If the FDR-corrected p-value is less than our significance level (usually 0.05), we reject the null hypothesis and conclude that there's a significant difference between at least one pair of treatments.
