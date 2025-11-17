# Netflix Movie Ratings Regression Analysis

Analyzing the factors that influence Netflix movie ratings using multiple regression in R.

![R](https://img.shields.io/badge/R-276DC3?style=flat-square&logo=r&logoColor=white)
![Quarto](https://img.shields.io/badge/Quarto-75AADB?style=flat-square&logo=quarto&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-success?style=flat-square)

---

## Overview

The goal was to figure out what actually makes Netflix movies get good ratings. Does genre matter? What about how many people watch it? Does it make a difference if it's available globally or just in certain regions? And what about when it comes out do certain seasons get better ratings?

Using 2023 Netflix data on over 14,000 movies, I ran a multiple regression in R to see if these factors could predict ratings. Turns out they really don't. Which is honestly kind of interesting in itself.

---

## Research Question

**What factors most significantly influence Netflix movie ratings?**

**Hypothesis:** Movies with higher viewing hours, released during certain seasons, or in popular genres (Comedy, Drama, Animation) tend to have higher average ratings on Netflix.

The analysis examines:
- **Genre** - Comedy, Drama, and Animation vs. other genres
- **Viewing Hours** - Total hours viewed (in millions)
- **Global Availability** - Worldwide vs. regional release
- **Release Season** - Winter, Spring, Summer, Fall patterns

---

## Dataset

**Source:** Netflix 2023 Movies Dataset

**Variables Analyzed:**
- **Rating** - Movie rating (interval ratio, dependent variable)
- **Genre** - Comedy, Drama, Animation (dummy coded, reference: other genres)
- **Hours Viewed** - Total hours viewed (recoded in millions)
- **Global Availability** - Binary (available globally or not)
- **Release Season** - Winter (Dec-Feb), Spring (Mar-May), Summer (Jun-Aug), Fall (Sep-Nov), reference: Winter

**Sample Size:** 14,633 movies

---

## Methodology

### Statistical Approach
I used **Multiple Linear Regression** with Ordinary Least Squares (OLS) estimation. Did everything in R using tidyverse, ggplot2, pwr, summarytools, stargazer, lubridate and base R. The significance level was set at α = 0.05.

### How I Did This

**Data Prep**
First, I cleaned the dataset and recoded some variables to make them easier to work with. Hours viewed got converted to millions, and I created dummy variables for genres (Comedy, Drama, Animation) and seasons (Fall, Spring, Summer), leaving Winter and "other genres" as reference categories.

**Looking at the Data**
Ran summary statistics to understand the distributions. Turns out most movies aren't available globally, and releases are pretty evenly spread across seasons. Comedy and Drama have way more movies than Animation.

**Building the Model**
Set up a multiple regression with Rating as the dependent variable and everything else as predictors: global availability, genre dummies, hours viewed, and season dummies.

**Checking if it Works**
Ran all the OLS diagnostics - residual plots, Q-Q plot, leverage analysis. Also checked for multicollinearity using VIF values. Did a power analysis to make sure the sample size was good enough.

**Making Sense of Results**
Looked at which coefficients were significant, what the R-squared told me, and whether the F-test showed the model was useful. Spoiler: it mostly wasn't, but that's actually interesting.

---

## Key Findings

### What I Found

Here's the thing - this model basically didn't work. And that's actually telling us something:

- **Comedy has a tiny negative effect** - Comedy movies rate about 0.063 points lower than other genres (p < 0.05). That's statistically significant but... it's not even a tenth of a point. Not really meaningful in practice.
- **Nothing else matters (in this model)** - Drama, Animation, hours viewed, global availability, release season - none of it showed significant effects
- **The model explains almost nothing** - R² of 0.001 means these variables explain 0.1% of why ratings differ. That's basically nothing.
- **Not even better than guessing** - The F-test wasn't significant, meaning I might as well just use the average rating instead of this whole model

### What This Actually Means

The fact that this model performed so poorly is the real finding. Movie ratings aren't about simple stuff like "it's a comedy" or "it came out in summer." They're about things I didn't measure like who's in it, how good the story is, how much Netflix promoted it, whether people actually liked watching it.

---

## Visualizations

### 1. Ratings vs Hours Viewed and Global Availability

![Ratings vs Hours Viewed](https://github.com/hope-tatenda-mutema/Netflix-Movie-Rating-DV-Multiple-Linear-Regression-R/blob/main/Ratings%20Vs%20Hour-Viewed%20and%20Global%20Availability.png)

This scatterplot reveals:
- Relationship between viewing hours and movie ratings
- Differentiation by global availability status
- Concentration of movies in lower viewing hours
- Positive trend line for globally available content

---

### 2. Ratings by Season and Comedy Genre

![Ratings by Season](https://github.com/hope-tatenda-mutema/Netflix-Movie-Rating-DV-Multiple-Linear-Regression-R/blob/main/Ratings%20by%20Season%20of%20Release%20and%20Comedy.png)

Box plot analysis showing:
- Rating distributions across four seasons (Fall, Spring, Summer, Winter)
- Comparison between Comedy and non-Comedy genres
- Median ratings remain relatively stable across seasons
- Similar patterns between genre categories

---

### 3. OLS Regression Diagnostics

![OLS Assumptions](https://github.com/hope-tatenda-mutema/Netflix-Movie-Rating-DV-Multiple-Linear-Regression-R/blob/main/OLS%20Assumptions%20Check.png)

Comprehensive diagnostic plots:
- **Residuals vs Fitted**: Checks linearity assumption
- **Q-Q Plot**: Validates normality of residuals
- **Scale-Location**: Assesses homoscedasticity
- **Residuals vs Leverage**: Identifies influential outliers

The diagnostics confirm that OLS regression assumptions are reasonably met.

---

## Model Performance

### Regression Statistics

- **Multiple R-squared**: 0.001 (0.1% of variance explained)
- **Adjusted R-squared**: ~0.000 (essentially no explanatory power)
- **F-statistic**: 1.414 (not significant, p > 0.05)
- **Power Analysis**: f² = 0.001, Power = 0.88 (high statistical power confirmed)

### Regression Equation

```
Movie Rating = 6.654 - 0.016(Global: Yes) - 0.063(Comedy)* + 0.011(Drama) 
               - 0.012(Animation) + 0.0003(Hours Viewed, mil) - 0.016(Fall) 
               + 0.001(Spring) - 0.024(Summer)
```
*Statistically significant at α = 0.05

### Coefficient Interpretations

| Variable | Coefficient | p-value | Interpretation |
|----------|-------------|---------|----------------|
| **Intercept** | 6.654 | <0.05* | Baseline rating for reference groups (Winter, non-Comedy/Drama/Animation, not global, 0 hours) |
| **Global Availability (Yes)** | -0.016 | >0.05 | No significant effect |
| **Comedy** | -0.063 | <0.05* | **Significant negative effect** - Comedy movies rated 0.063 points lower |
| **Drama** | 0.011 | >0.05 | No significant effect |
| **Animation** | -0.012 | >0.05 | No significant effect |
| **Hours Viewed (millions)** | 0.0003 | >0.05 | No significant effect |
| **Fall** | -0.016 | >0.05 | No significant effect vs. Winter |
| **Spring** | 0.001 | >0.05 | No significant effect vs. Winter |
| **Summer** | -0.024 | >0.05 | No significant effect vs. Winter |

### Multicollinearity Check

✅ **All VIF values < 5** - No serious multicollinearity problems detected

---

## Business Implications

### The Big Picture

So this model has an R² of 0.001. That's terrible. But it tells us something important: **you can't predict movie quality with basic metadata.**

### What This Means for Netflix

**Don't overthink the simple stuff:**
- Genre? Barely matters (and even then, only Comedy shows a tiny effect)
- Release timing? Doesn't matter
- Global vs regional? Doesn't matter
- Hours viewed? Doesn't correlate with ratings

**Focus on what actually matters:**
- Who's in the movie (cast quality)
- Who made it (director, writers)
- How good the story actually is
- How well you market it
- Whether the right audience finds it

### For Anyone Doing This Kind of Analysis

This is a good reminder that just because you *can* measure something doesn't mean it predicts what you care about. I had data on genre, viewing, and release patterns all easy to track. But ratings depend on stuff that's harder to quantify: talent, storytelling, production quality, marketing effectiveness.

If you're building predictive models, you need variables that actually relate to what you're trying to predict. This analysis basically shows what *doesn't* work as a starting point for future research.

---

## Files in This Repository

Here's what you'll find in this repo:

- **README.md** - You're reading it
- **NetflixRating_Multiple_Regression_Analysis.qmd** - The Quarto source file where I did all the analysis
- **NetflixRating_Multiple_Regression_Analysis.html** - Full analysis report (open this in your browser to see everything)
- **Netflix_Multiple_Regression_Analysis_Memo.docx** - Executive summary I wrote up
- **total_netflix_2023_new.csv** - The Netflix dataset
- **visualizations/** - All the plots and diagnostic charts

---

## How to Reproduce

### Just Want to See the Results?
Open `NetflixRating_Multiple_Regression_Analysis.html` in your browser. That's it. Everything's in there.

The `.docx` memo has a quick summary if you want the short version.

### Want to Run It Yourself?
```r
#Required Packages 
library(tidyverse)
library(dplyr)
library(lubridate)
library(summarytools)
library(car)
library(stargazer)
library(pwr)

# Render the analysis
quarto::quarto_render("NetflixRating_Multiple_Regression_Analysis.qmd")
```

You'll need R and ideally RStudio.

---

## Technical Details

### Model Specification

```r
#regression model

movie_ratings_model <- lm(RatingNum ~ Available.Globally. + genre_comedy + genre_drama + genre_animation + Hours.Viewed_mil + Season_Fall + Season_Spring + Season_Summer, data = netflix_data)


stargazer(type = 'text', movie_ratings_model, single.row = T)
```

### Reference Categories
- **Genre**: Other genres (not Comedy, Drama, or Animation)
- **Season**: Winter (December - February)
- **Global Availability**: No (regional only)

### Assumptions Verified
✅ **Linearity**: Residuals vs. Fitted plot shows no clear pattern  
✅ **Independence**: Residuals appear independent  
✅ **Homoscedasticity**: Constant variance maintained (Scale-Location plot)  
✅ **Normality**: Q-Q plot shows residuals are approximately normally distributed  
✅ **No influential outliers**: Residuals vs. Leverage plot shows no concerning points  
✅ **No multicollinearity**: All VIF values < 5  

### Limitations
- **Very low R² (0.001)** - Model explains virtually none of the rating variance
- **Non-significant F-test** - Model doesn't predict better than the mean
- **Cross-sectional data** - Single time period (2023)
- **Missing key variables**: Cast, director, budget, marketing, viewer demographics, storyline quality
- **Observational study** - Correlation only, not causation
- **Limited practical significance** - Even the one significant coefficient (Comedy) has minimal real-world impact

---

## Study Limitations

### The Obvious Problem: Missing the Important Stuff

The biggest issue here is what I *didn't* include in the model. All the things that probably actually matter:

- Cast and actors
- Director and production team
- Budget (production and marketing)
- How Netflix promoted it
- Who actually watched it (demographics)
- Whether people finished watching it
- What reviewers said
- What else was competing for attention when it came out

That R² of 0.001? That's because all the real predictors aren't in the dataset.

### What Could Be Better

If I did this again (or if someone else wants to), here's what would actually make a difference:
- Get cast and crew information
- Include budgets if available
- Look at viewer engagement (did people finish it?)
- Add sentiment from reviews
- Break down by viewer demographics
- Consider what else was releasing at the same time

---

## Future Enhancements

If I or someone else wanted to improve on this:

- Add cast and director data
- Include production budgets
- Get marketing spend information
- Look at viewer completion rates
- Analyze review sentiment
- Try machine learning approaches
- Build an interactive dashboard to explore the data
- Break down by viewer demographics

---

## What I Learned

### Main Takeaways

1. **Basic metadata can't predict quality** - Genre, season, availability... none of it really matters for ratings
2. **Comedy has a tiny (but significant) negative effect** - But we're talking 0.063 points. That's nothing.
3. **Popular ≠ Good** - Hours viewed doesn't correlate with ratings at all
4. **Timing doesn't matter** - No seasonal patterns found
5. **Global availability is irrelevant** - Doesn't affect how people rate movies

### Why This Matters

Sometimes the most interesting finding is that there *isn't* a finding. This analysis shows that you can't judge a movie's quality by looking at simple categorical data. Ratings are about deeper things the actual content, the talent, how it's marketed, who watches it.

### If You're Building on This

- **For researchers**: Add the variables that actually matter (cast, budget, engagement)
- **For Netflix folks**: Don't rely on genre/season/availability for predictions about quality
- **For data people**: This is a good baseline of what *doesn't* work, which helps guide what to try next

---

## About This Project

This was part of my statistical analysis coursework. I wanted to see if I could predict Netflix movie ratings using basic variables that are easy to find. 

Turned out I couldn't. But that's actually a useful finding - it shows that movie quality isn't about simple categories like genre or release season. It's about the things that are harder to measure: who's in it, how good the story is, how it's marketed.

I made sure to do everything properly checked all the OLS assumptions, ran diagnostics, did power analysis. The methodology is solid. The model just doesn't work because the variables I had access to aren't the ones that matter.

Sometimes negative results are the most informative.

**Author:** Hope Tatenda Mutema  
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
