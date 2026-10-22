# Recorded walkthrough script

The text below follows the supplied recording. The video is approximately 4 minutes 37 seconds and has captions burned in.

## Problem and source

Hi, this project asks which observable home features are associated with sale price in Ames, Iowa, and how well those features predict prices on held-out homes. I use Kaggle's House Prices educational competition data, originally compiled by Dean De Cock. The training file has 1,460 sales and 79 explanatory variables. It is historical data, not a current market sample.

## Cleaning and split

I excluded the row ID from predictors and kept the sale price as the outcome. There are 7,829 missing cells. In this dataset, many missing categorical values mean a feature is absent, so I preserve them as an explicit Missing category. Numeric missing values use medians learned from the training split. I made a seeded 80/20 split before fitting preprocessing to avoid leaking validation information.

## Findings

The clearest pattern is overall quality: median sale price rises from $50,150 at quality 1 to $432,390 at quality 10, roughly 8.6 times higher. The chart uses medians by the ordinal quality score. Neighborhood medians also vary: the five highest in this sample are North Ridge Heights, Northridge, Stone Brook, Timberland, Somerset. Finally, living area and sale price have a Pearson correlation of 0.71, but the scatterplot makes clear that homes of similar size still sell at very different prices.

## Model and takeaway

For the bonus, a Ridge regression predicts log sale price from standardized numeric predictors and one-hot categorical predictors. On a held-out 20 percent of the data, RMSE is $40,277, MAE is $17,291, and R-squared is 0.782. This is a baseline, not a valuation tool. The practical takeaway is that quality, size, and location relate to price together; no single feature is enough.

## Limitations and close

These sales are from 2006 to 2010 in one city, so the result does not transfer automatically to today's market. The analysis is associational, and the random split tests similar historical examples, not future sales. The README documents the data, cleaning, results, limits, and steps to rerun the notebook.

## How to read the model results

The recording reports a separate Ridge demonstration with dollar-scale RMSE and MAE. The final notebook compares the mean baseline, Ridge, Lasso, and Random Forest using log-price RMSE and R², and selects Lasso by train-only cross-validation. These are separate evaluations and their error values should not be compared directly.
