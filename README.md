# Startup Investment Analysis

## Project Overview
Comprehensive analysis of 40,000+ startup investments to identify optimal investment strategies for a venture capital firm.

## Objectives
- Analyze funding patterns across market segments
- Identify outliers and anomalies in funding data
- Compare financing types by volume, popularity, and returns
- Provide investment recommendations for 2015

## Key Findings

### Market Structure
- 395 unique market segments classified into mass (49), mid (57), and niche (289)
- 59% of companies receive single-round financing
- Companies with extended funding cycles (>1 year) attract 60%+ of total investment

### Top Financing Types
| Type | Volume | Companies | Returns |
|------|--------|-----------|---------|
| Venture | $129.1B | 18,821 | $40.6B |
| Seed | $9.4B | 13,376 | $2.4B |
| Debt Financing | $8.2B | 3,265 | $4.7B |

### Investment Recommendations (for 2015)
1. **Technology** - Score: 56.9/100
2. **Apps** - Score: 39.0/100
3. **Medical** - Score: 36.8/100

## Tools & Technologies
- Python 3
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scipy

## Data
- `cb_investments.csv` - 40,000+ company records with funding information
- `cb_returns.csv` - Returns by financing type and year

## Methodology
1. Data preprocessing and cleaning (34.5% data loss)
2. Feature engineering (funding groups, market segmentation)
3. Outlier detection using IQR method per segment
4. Time series analysis of funding dynamics
5. Normalized return rate calculation
6. Composite scoring model for segment ranking

## Visualizations
The notebook includes:
- Pie charts for funding distribution
- Histograms for market segmentation
- Line charts for funding dynamics
- Bar charts for financing type comparison

## Author
Ilia Duda

