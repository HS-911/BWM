# Fort McKay Car Rental Selection with the Best–Worst Method

This Python example uses the linear Best–Worst Method (BWM) to rank four rental options for a trip to Fort McKay. It compares two Toyota Camrys, a Volkswagen Jetta, and a Chevrolet Malibu on cost, comfort, style, safety, quality, and sustainability.

## Run the example

Use Python 3 with NumPy, pandas, SciPy, and Matplotlib. To install the packages locally, run `python -m pip install numpy pandas scipy matplotlib`.

1. In **section 02**, use the supplied survey ranks for a trial run or replace them with your results in `SURVEY`. Rank 1 is most preferred. Use 1–4 for colour, 1–3 for brand and model year, and 1–2 for body style.
2. Run the code in Google Colab or Jupyter. If you save it as a Python script, run it in a terminal where you can answer the prompts.
3. In **sections 15–16**, select the most and least important criteria. Rate Best over Worst from 1 to 9, where 1 means equal importance. The code then collects all Best-to-Others ratings before asking for Others-to-Worst ratings. The direct Best-to-Worst rating sets the upper limit for the remaining ratings.

## Calculate the vehicle scores

- **Categorical KPIs.** The code converts the survey ranks and the fixed equipment and powertrain ranks to preference scores between 0 and 1.
- **Daily cost and emissions.** Cost combines the daily rental rate and fuel cost. Sustainability is represented by estimated daily CO₂ emissions from fuel use. The exercise assumes 350 km/day, a fuel price of CAD 1.65/L, and an emissions factor of 2.3 kg CO₂/L. Rental rates are estimates, and model years and equipment levels are exercise assumptions.
- **Qualitative criteria.** Comfort, Style, Safety, and Quality combine the relevant KPI scores using the coefficients in **section 06**.
- **Criterion normalization.** The code scales each of the six calculated criteria across the four cars so 0 is worst and 1 is best. Lower daily cost and emissions score higher. Higher Comfort, Style, Safety, and Quality values score higher.

## Read the results

- **Criterion weights.** The linear BWM model uses the two comparison vectors to calculate six weights that sum to 1. [Rezaei (2016), *Best-worst multi-criteria decision-making method: Some properties and a linear model*](https://doi.org/10.1016/j.omega.2015.12.001)
- **Consistency.** The code reports the local and overall input-based consistency ratio (CRI) and shows the reference threshold when available. A CRI above the threshold produces a `review judgments` message. [Liang, Brunelli, and Rezaei (2020), *Consistency issues in the best worst method: Measurements and thresholds*](https://doi.org/10.1016/j.omega.2019.102175)
- **Car ranking.** The code multiplies each normalized criterion score by its BWM weight and adds the six contributions. The car with the highest total receives rank 1. The output also includes the KPI and criterion tables and a bar chart of the weights.
