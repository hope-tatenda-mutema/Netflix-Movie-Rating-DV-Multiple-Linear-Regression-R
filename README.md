# Netflix Movie Ratings Regression Analysis

Analyzing the factors that influence Netflix movie ratings using multiple regression in R.

![R](https://img.shields.io/badge/R-276DC3?style=flat-square&logo=r&logoColor=white)
![Quarto](https://img.shields.io/badge/Quarto-75AADB?style=flat-square&logo=quarto&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-success?style=flat-square)

---

## Overview

This project explores how various factors including genre, viewing hours, global release status, and seasonal timing impact Netflix movie ratings. Using multiple regression analysis in R, I identified key drivers of ratings across diverse content in the Netflix 2023 catalog.

---

## Research Question

**What factors most significantly influence Netflix movie ratings?**

The analysis examines:
- **Genre** - How different genres affect ratings
- **Viewing Hours** - Relationship between viewership and ratings
- **Global Release** - Impact of worldwide vs. regional availability
- **Season** - Seasonal patterns in movie ratings
- **Interactions** - Combined effects of multiple factors

---

## Dataset

**Source:** Netflix 2023 Movies Dataset

**Variables Analyzed:**
- Movie ratings (dependent variable)
- Genre classifications
- Total hours viewed (millions)
- Global availability status
- Release season
- Additional movie metadata

**Sample Size:** 3,355 movies

---

## Methodology

### Statistical Approach
- **Multiple Linear Regression** (Ordinary Least Squares)
- **Software:** R (tidyverse, ggplot2, broom)
- **Validation:** OLS assumption testing and diagnostics

### Analysis Workflow

1. **Data Preparation**
   - Data cleaning and validation
   - Missing value treatment
   - Variable transformation

2. **Exploratory Analysis**
   - Univariate distributions
   - Correlation analysis
   - Visual exploration

3. **Model Development**
   - Variable selection
   - Model fitting
   - Interaction effects

4. **Model Validation**
   - OLS assumptions testing
   - Residual diagnostics
   - Outlier detection

5. **Interpretation**
   - Coefficient analysis
   - Statistical significance
   - Practical implications

---

## Key Findings

### Primary Results

The multiple regression model reveals:

- **Genre Impact**: Specific genres (particularly Comedy) show significant effects on ratings
- **Viewing Hours**: Positive correlation between hours viewed and ratings
- **Global Availability**: Movies with global release demonstrate different rating patterns
- **Seasonal Effects**: Release season influences ratings, with variation across genres
- **Model Fit**: The combined model explains substantial variance in Netflix ratings

### Statistical Significance

- **R-squared**: Model explains significant portion of rating variance
- **F-statistic**: Overall model is highly significant (p < 0.001)
- **Coefficients**: Multiple predictors show statistically significant relationships

---

## Visualizations

### 1. Ratings vs Hours Viewed and Global Availability

![Ratings vs Hours Viewed](./visualizations/Ratings_Vs_Hour-Viewed_and_Global_Availability.png)

This scatterplot reveals:
- Relationship between viewing hours and movie ratings
- Differentiation by global availability status
- Concentration of movies in lower viewing hours
- Positive trend line for globally available content

---

### 2. Ratings by Season and Comedy Genre

![Ratings by Season](./visualizations/Ratings_by_Season_of_Release_and_Comedy.png)

Box plot analysis showing:
- Rating distributions across four seasons (Fall, Spring, Summer, Winter)
- Comparison between Comedy and non-Comedy genres
- Median ratings remain relatively stable across seasons
- Similar patterns between genre categories

---

### 3. OLS Regression Diagnostics

![OLS Assumptions](./visualizations/OLS_Assumptions_Check.png)

Comprehensive diagnostic plots:
- **Residuals vs Fitted**: Checks linearity assumption
- **Q-Q Plot**: Validates normality of residuals
- **Scale-Location**: Assesses homoscedasticity
- **Residuals vs Leverage**: Identifies influential outliers

The diagnostics confirm that OLS regression assumptions are reasonably met.

---

## Model Performance

### Regression Statistics

- **Multiple R-squared**: [Value indicates model fit]
- **Adjusted R-squared**: [Accounts for number of predictors]
- **F-statistic**: [Tests overall model significance]
- **Residual Standard Error**: [Measures prediction accuracy]

### Variable Significance

**Significant Predictors (p < 0.05):**
- Genre categories
- Hours viewed
- Global availability
- Season of release
- Interaction terms

---

## Business Implications

### For Content Strategy
- **Genre Selection**: Focus on high-performing genres identified in the model
- **Release Timing**: Consider seasonal patterns for optimal launch dates
- **Global vs Regional**: Leverage insights for distribution decisions

### For Analytics Teams
- **Predictive Modeling**: Use coefficients to forecast potential ratings
- **Content Acquisition**: Data-driven decisions on new content
- **Performance Benchmarking**: Compare actual vs predicted ratings

### For Stakeholders
- Quantifiable understanding of rating drivers
- Evidence-based content strategy recommendations
- Framework for evaluating new content opportunities

---

## Files in This Repository

```
netflix-ratings-regression/
├── README.md                                              # This file
├── NetflixRating_Multiple_Regression_Analysis.qmd        # Quarto source
├── NetflixRating_Multiple_Regression_Analysis.html       # Full analysis report
├── Netflix_Multiple_Regression_Analysis_Memo.docx        # Executive summary
├── total_netflix_2023_new.csv                            # Dataset
└── visualizations/
    ├── Ratings_Vs_Hour-Viewed_and_Global_Availability.png
    ├── Ratings_by_Season_of_Release_and_Comedy.png
    └── OLS_Assumptions_Check.png
```

---

## How to Reproduce

### View Results
1. Open `NetflixRating_Multiple_Regression_Analysis.html` in any web browser
2. Review the memo for executive summary

### Run Analysis
```r
# Install required packages
install.packages(c("tidyverse", "quarto", "broom", "car"))

# Open and render the Quarto document
quarto::quarto_render("NetflixRating_Multiple_Regression_Analysis.qmd")
```

### Requirements
- R version 4.0+
- RStudio (recommended)
- Packages: tidyverse, ggplot2, broom, car, quarto

---

## Technical Details

### Model Specification

```r
lm(rating ~ genre + hours_viewed + global_availability + 
   season + genre:season + hours_viewed:global_availability)
```

### Assumptions Verified
✅ Linearity of relationships  
✅ Independence of residuals  
✅ Homoscedasticity (constant variance)  
✅ Normality of residuals  
✅ No severe multicollinearity  

### Limitations
- Cross-sectional data (2023 only)
- Observational study (correlation, not causation)
- External factors not captured (marketing spend, competition)
- Self-selection bias in viewing hours

---

## Future Enhancements

**Potential Extensions:**
- Time series analysis across multiple years
- Machine learning models (Random Forest, XGBoost)
- Interactive Shiny dashboard
- Deeper genre subcategory analysis
- Inclusion of cast/director variables
- Sentiment analysis of reviews

---

## Insights Summary

### Key Takeaways

1. **Multi-factor Influence**: Ratings are influenced by multiple interacting factors
2. **Genre Matters**: Specific genres show consistent rating patterns
3. **Viewership Correlation**: Higher viewing hours associate with better ratings
4. **Global Appeal**: Worldwide availability relates to rating performance
5. **Seasonal Nuances**: Release timing shows subtle effects

### Recommendations

- Prioritize high-performing genre combinations
- Consider global release for quality content
- Monitor seasonal trends for strategic launches
- Use predictive model for content evaluation

---

## About This Project

This analysis demonstrates practical application of multiple regression techniques to real-world streaming data, combining statistical rigor with business insight.

**Author:** Hope Tatenda Mutema  
**Course:** Statistical Analysis / Data Analytics  
**Year:** 2023

**Connect:**
- Portfolio: [hopetatendamutema.com](https://hopetatendamutema.com)
- LinkedIn: [hope-mutema](https://www.linkedin.com/in/hope-mutema)
- GitHub: [@hope-tatenda-mutema](https://github.com/hope-tatenda-mutema)

---

## License

This project is available for educational and portfolio purposes.

---

<div align="center">

**Understanding what makes content successful, one regression at a time.**

![Made with R](https://img.shields.io/badge/Made%20with-R-276DC3?style=flat-square&logo=r)
![Netflix Data](https://img.shields.io/badge/Data-Netflix%202023-E50914?style=flat-square)

</div>
