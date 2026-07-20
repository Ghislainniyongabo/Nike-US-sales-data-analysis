# Personal project: Nike US Sales — What Drives Revenue?

An exploratory analysis of Nike US sales data to understand what drives revenue and identify a few practical business recommendations.

## The dataset

- 9,360 transactions from January 2020 to December 2021
- Columns: `Invoice Date`, `Product`, `Region`, `Retailer`, `Sales Method`,
  `State`, `Price per Unit`, `Total Sales`, `Units Sold`
- There were no missing values, so data cleaning was minimal.
  
## What's in the notebook

1. Load the data and take a first look
2. Check the data quality — does `Total Sales` actually match
   `Price per Unit × Units Sold`?
3. Break revenue down by product and sales method
4. Check how the numeric columns correlate with revenue
5. Build a model (Random Forest + Linear Regression) to see what actually
   predicts revenue
6. Ask the more useful question — what predicts *units sold*, since revenue
   is just volume times price
7. Summarize what was found

## What I found

One thing that stood out is that revenue is mostly just math: Units Sold accounted for most of the model's importance (86%), followed by Price per Unit (11%). Everything else — product, region, state, channel — barely moves the needle once you already know those two numbers.

The more interesting question is what drives **units sold**, since that's
something the business can actually influence. There, `State` (28%),
`Price per Unit` (25%), and `Sales Method` (17%) matter most, followed by
`Product` (12%) and `Region` (10%).

One thing worth flagging: for about 85% of Online and Outlet transactions,
`Total Sales` doesn't match `Price × Units` — it's roughly 90% lower than
expected. That's too big to be a normal discount, so it's worth checking
with whoever owns the data before trusting these numbers for reporting.

A few other quick takeaways: Men's Street Footwear and Women's Apparel
bring in the most revenue and have the highest average price. Women's
Athletic Footwear brings in the least. In-store has the highest average
order value, Online the lowest.

## Recommendations

1. Figure out the Online/Outlet revenue issue before using this data for
   forecasting or reporting.
2. Focus on selling more units, not raising prices — that's what actually
   moves revenue here.
3. Put more inventory and marketing into the best-performing states and
   the in-store channel.
4. Keep investing in the top product lines, and dig into why Women's
   Athletic Footwear is underperforming.
5. Take a closer look at the Online channel and its lower order values.
6. For short-term forecasting, a simple price × volume model works well. For planning where to invest, use the demand model instead.

## Built with

- Python 3.11
- pandas, numpy
- matplotlib, seaborn
- scikit-learn (Random Forest + Linear Regression)

## Files

```
.
├── nike_revenue_analysis.ipynb   # the analysis
├── nike.csv                      # dataset (add your own — not included here)
└── README.md
```

## Running it

```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
jupyter notebook nike_revenue_analysis.ipynb
```

Just make sure `nike.csv` is sitting in the same folder as the notebook.
