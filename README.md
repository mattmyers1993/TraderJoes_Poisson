# How I Order Chips for Trader Joe's using Python, Poisson Distributions, and Power BI

## Aloha!
Thank you for checking out my product ordering probability calculator. 
[Please find the Power BI report here](https://app.powerbi.com/view?r=eyJrIjoiYWI0N2MyNDAtYTdkNy00YmNhLWE5N2QtMzQyOGJhMGRkNWMxIiwidCI6ImJjMzM5NDJjLTE2YjQtNDcwYS04Yjc5LTk1MmNmMzY0NmJjYiIsImMiOjZ9)

This tool helps me when ordering products for my store. The goal is to balance meeting customer demand while carrying the least amount of product to reduce spoilage and optimize storage space. Any Trader Joe's is one big exercise in probability.

This calculator addresses the problem that as crew members responsible for ordering product, we are given only one number to work from-- daily average sales in cases. This is a good start, as it tells us about  the middle of the historic daily sales distribution. I want to model where the ceiling of the distribution is as well. In terms of percentiles, we are given roughly the 50th percentile amount, but knowing the 100th percentile amount helps me prepare for a day of heavy sales without just overloading on inventory haphazardly.

In addition, if we order a shipment to meet the 100th percentile we can model how many cases of product we will have left over. This gives me a huge leg up on managing the space in our stockroom.

The goal is to order inventory for as much of that ceiling as we can, while keeping as little back stock as we can. Come aboard for an adventure of high probabilities, low inventory, and tasty treats.

## How this report works:
The main tool is the table in the middle. Provided a product's average sales for a given day, the table provides 2 probabilities for each number of cases ordered (0-20).

The first probability is the probability that x number of cases meets demand (Probability Demand Met or PDM). This is the percent chance we have at least as much product as customers want to buy.

The second probability tells us for x number of cases ordered, how many cases are we likely to have leftover the next day on average.

The goal is to optimize both numbers for our needs. We could order 20 cases of a product and hit 100% probability that we meet demand, but we might be likely to have 19 cases left over that need to be stored or might spoil. 

This tradeoff can be seen in the line graph in the lower right. As PDM in red goes up, so do the likely leftovers.  We want to look for the point where the red PDM line starts to level out and the blue expected leftovers line is still low.

## More Nuance:

If you're interested in more nuance to the expected leftover cases, the upper right column chart titled "Leftover Cases Probability Distribution" gives the probability distribution for ordering X cases. We may have 3.1 cases left on average according to the table, but we can calculate the exact probability we will have 0,1,2,3, etc. cases given its average sales.

## Get to Orderin'!:

Simply click on the products and the report filters to a hypothetical state with an average number of cases sold per day. I've also selected a number of cases I would order to maximize PDM and minimize expected leftover cases. Feel free to select other order amounts on the table's first column to see how this affects the probability distribution in the upper right column chart.

When you are ready for a new product, hit the "X" on the text box and click on a new item.

## What's Going On Under the Hood?

This lookup table is built using the Poisson Distribution, which models the probability of a certain number of events—like sales—occurring over a fixed time period, given an average rate. The Poisson model assumes events happen independently and at a steady average rate (called lambda, or λ). It's especially helpful in retail environments where sales patterns can be noisy or sample sizes are small, because it requires only an average value to produce meaningful probability estimates. While Poisson doesn’t account for seasonality by itself, those effects can be incorporated by adjusting the input using rolling weekday averages—data that’s typically available to order writers. The result is a simple, data-driven view into the probability of demand being met and cases left over, built from the natural randomness of everyday sales.

## Want to See How It’s Built?

If you're curious about how these probabilities are calculated, [check out my Jupyter notebook] where I use Python’s scipy.stats library and the Poisson function to generate the full lookup table powering this report.

## About the Data

This project is for demonstration purposes only. No private information from Trader Joe’s has been used. All average sales numbers are fictional, and the underlying lookup table relies solely on Poisson-generated distributions—not actual sales data.

## License

This repository is provided for educational and demonstration purposes only.  
All content, including Power BI reports and Python code, is © Matt Myers.  
**Commercial use, redistribution, or adaptation is not permitted without written consent.**
