# YTD Order Analysis for Rechargeable Battery Company

## Overview

The following is an investigation into customer order data from a recently launched rechargeable battery brand's Amazon Seller Central account. In addition to EDA to uncover trends in purchase behavior, the goal of this analysis is determine whether or not the current rate of products being returned as defective warrants an investigation into the current manufacturer.

### Technologies Used

Pandas, Numpy, SciPy, Matplotlib, Plotly, Seaborn, 

## The Data

The data analyzed is from the 1257 orders and 1371 units shipped since going live on Amazon in January, in addition to exports from Seller Central detailing returns and requests for replacement.

## EDA

- Clean product purchase date data and convert to two columns - one for time of day and one for standard date. The left visualization represents the frequency of purchase during each hour of the day, where the stated hour "9 AM" contains orders placed between 9:00 and 9:59:59. The right visualization is frequency of orders by date over time:

<div align="center">
    <img src="https://github.com/ryankirkland/customer-data-analysis/blob/master/images/Screen%20Shot%202020-07-23%20at%202.56.37%20PM.png" width=49% />
    <img src="https://github.com/ryankirkland/customer-data-analysis/blob/master/images/orders-over-time.png" width=49% />
</div>

- In another exercise, I chose to clean the order ship address data to allow for grouping by state to create a visualization of the regions that have placed the most orders YTD:

<div align="center">
   <img src="https://github.com/ryankirkland/customer-data-analysis/blob/master/images/orders-by-state.png" width=70%>
</div>

The following charts break out the return reasons across all return and replacement request, then a visualization of the total shipped product that was marked as defective by customers compared to those that shipped in expected working condition, but may have been returned for reasons outside of defect:

<div align='center'>
    <img src="https://github.com/ryankirkland/customer-data-analysis/blob/master/images/defect-vs-quality.png" width=45% />
    <img src="https://github.com/ryankirkland/customer-data-analysis/blob/master/images/return-reasons.png" width=45% />
</div>

## Hypothesis Testing: Frequentist Approach

#### One-Tailed Hypothesis Test to Determine with 95% Confidence Battery Company Does Not Need to Investigate Manufacturer

 - In the early stages, the battery company's tolerance for defect is higher as they work out kinks with the manufacturer and battery design. They are consistently researching defective product to fix known issues, but in the early stages are willing to manage defects up to 5%, at which stage they would request a formal investigation into the manufacturer to determine whether or not the root cause of defect is a result of manufacturing practices as opposed to a design flaw.
 
 
 - The null hypthesis in this test would be that the defective rate for these batteries will fall at or below 5% as future orders come through based on the current sample of orders and customer returns/defects.
 
<div align='center'>
    <img src="https://github.com/ryankirkland/customer-data-analysis/blob/master/images/binomial.png"/>
</div>

##### Confidence Interval

We can be 95% confident that the mean defect rate of a sample of all products will fall between 1.01% and 2.33%.

## Hypothesis Test: Bayesian Approach

#### Beta Distribution for determining the probability that 5% or more units will be defective in future shipments

I want to build a probability distribution for the value of p, which is the proportion of units that will turn out to be defective in future shipments. We will define success as locating a defective and failure as no defects found.

<div align='center'>
    <img src="https://github.com/ryankirkland/customer-data-analysis/blob/master/images/total-beta.png"/>
</div>

#### Beta Distributions of Defect Rates by Product

- Even though analysis at the product level yielded a close to 0 probability of defect rates rising over 5% based on current data, there is still a possibility that the defect rate at the individual product level is >5%, and a single product is responsible dragging up the overall defect rate.

<div align='center'>
    <img src="https://github.com/ryankirkland/customer-data-analysis/blob/master/images/aa-aaa-beta.png"/>
</div>

- Probability of 5% or greater defect rate for AA: 0.0
- Probability of 5% or greater defect rate for AAA: 0.0
- Probability of 2% or greater defect rate for AA: 0.1303
- Probability of 2% or greater defect rate for AAA: 0.5639

##### Credible Interval

- 95% Credible Interval of AA Defect Rates: (0.57%, 2.6%)
- 95% Credible Interval of AA Defect Rates: (1.22%, 3.27%)
            
## Results

- The results of the hypothesis test lead me to conclude, based on the current data, the defect rate at the total product level and individual product level does not warrant an investigation into manufacturing practices, as I was unable to reject my null hypothesis in the Frequentist approach to testing whether or not the defect rate for the batteries would land at or below 5% in future shipments. The Bayesian approach also showed an almost 0 probability of a 5% or greater defect rate.

## Future Work

-  I would like to build on this to leverage Bayesian Decision Making taking in defect rates, demand levels, wholesale price, retail sales prices, and costs associated to selling to determine the most profitable choice in manufacturer through modeling future months of performance.
