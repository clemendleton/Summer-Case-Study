# Code Reproducibility - Group 2

## 1. Data Ingestion/Carpentry 
### [1.1 KGS Production Data Carpentry](KGS_Production_Data_Carpentry.ipynb) 
The monthly well production data was combined from multiple individual source files (provided in individual excel files by year/decade) and indexed on county and date. 

* Requires: N/A; Source files are programmatically obtained in notebook 
* Produces: `county_production_monthly.csv`
 
### [1.2 KGS Well Data Carpentry](KGS_Well_Data_Carpentry.ipynb) 
The monthly well activity by county was produced from the Kansas Oil and Gas Well Database by spatially aggregating wells by county (point-in-polygon) and aggregating by date. 

* Requires: N/A; Source files are programmatically obtained in notebook 
* Produces: `ks_wells_clean.csv` 
 
### [1.3 Oil Price Data Carpentry](1-Oil_Price_And_Inflation_Data_Ingestion.ipynb) 
Ingests monthly and yearly oil prices and inflation adjustments, reduces these datasets to necessary columns and adjusts yearly oil prices for inflation. 

* Requires: `Monthly_Oil_Prices_EIA.csv`; `inflation_correction.csv`; `crude-oil-prices-yearly.csv` 
* Produces: `Inflation_Corrected_Oil_Prices_Yearly.csv` 
 
### [1.4 Unemployment Data by County Oil Prodution Data Carpentry](KS_Unemployment_Data_by_County_and_Oil_Prod_Carpentry.ipynb) 
Ingests monthly Unemployment data for the state of Kansas at the county level and cleans it, adjusts column count and headings to better join with other datasets. Also ingests monthly oil prices to clean for joining with visualization data. 

* Requires: `KS_Unemployment_Statistics.csv`, `Monthly_Oil_Prices_EIA.csv` 
* Produces: `Kansas_Unemployment_monthly.csv`, `oil_prices.csv` 

### [1.5 Data Population Estimated Data Exploration](Kansas_Population_DataCarpentry_1.ipynb) 
Cleaning the censis data for the kansas state and counites population  

* Ingests: Kansas state and counties population data (https://kslib.info/431/County-Data) and https://www.census.gov/data/tables/time-series/demo/popest/2010s-counties-total.html

* Produces:  `Kansas_1860_2019_population.to_csv`, `Kansas_State_population.to_csv`

## 2. Analysis 
### [2.1 Monthly well events by county](monthly_well_events_by_county.ipynb) 
Explores the well activity (permits, new wells spud/completed, plugged) aggregated by county 	and month.  

* Requires: `ks_wells.clean.csv` 
* Produces: `monthly_well_activity.csv`  
	 
### [2.2 Kansas Labor Force Exploration by County](Kansas_Labor_Force_Data_by_County_Exploration_R.ipynb) 
Explores labor force numbers over time at the county level. 

* Requires: `Kansas_Unemployment_monthly.csv` 
	 
### [2.3 Kansas Unemployment Exploration by County](Kansas_Unemployment_Data_by_County_Exploration_R.ipynb) 
Explores unemployment over time at the county level and summarizes all economic data at the county level. 

* Requires: `Kansas_Unemployment_monthly.csv` 
 
 
### [2.4 Multivariate/Correlation Analysis](multivariate.ipynb) 
Used to inform which features were correlated and which counties to focus on for the data 	story. 

* Requires: `monthly_well_activity.csv`, `county_production_monthly.csv`,  
`Kansas_Unemployment_monthly.csv` 
* Produces: `mv_join.csv` 
 
### [2.5 Multivariate Visual Analysis of Counties](Multivariate_Visual_Analysis_of_Counties_R.ipynb) 
Explores correlations between economic and well data at the county level. 

* Requires: `well_activity_and_economic_data.csv` 
	 
### [2.6 Kansas Production, Price, and Correlation](2-Oil_Production_Price_Inflation_Carpentry_Analysis.ipynb) 
Explores yearly and monthly production and prices.  Applies the inflation correction on yearly monthly oil prices. 

* Requires: `county_production_annual.csv`; `county_production_monthly.csv`; `Inflation_Corrected_Oil_Prices_Yearly.csv`; 
* Produces: `prod_price_inf_merge.csv`; `statewide_prod_eval.csv` 

### [2.7 Counties Estimates Population - Machine Learning](Estimate_Counties_Population_ML_2a.ipynb) 
Find the estimated Kansas counties population 

* Ingests: `Cleaned_Kansas_1860_2019_population.csv` 
* Produces:  `Estimated_Pottawatomie.population.csv`, `Estimated_Ellis.population.csv`, `Estimated_Dickinson.population.csv`, `Estimated_Riley.population.csv`

### [2.8 State Estimates Population - Machine Learning](Estimate_Kansas_State_Population_ML_2b.ipynb) 
Find the estimated Kansas state population 

* Ingests: `Cleaned_Kansas_State_population.csv` 
* Produces: `Estimated_states_PopulationByMonth.csv`  

### [2.9 Normalizing_Labor_Data](Normalizing_Labor__DataCarpentry_3.ipynb) 
Add the labor data and normalizing it by a percentage on the estimated population data  

* Ingests: `Estimated_Riley.population.csv`, `Estimated_Pottawatomie.population.csv`, `Estimated_Ellis.population.csv`, `Estimated_Dickinson.population.csv`,`Kansas_Unemployment_monthly.csv`

* Produces: `Dickinson_Labor_population.csv`, `Ellis_Labor_population.csv`, `Pottawatomie_Labor_population.csv`, `Riley_Labor_population.csv`
	 
## 3. Visualizations 
### [3.1 Cumulative Oil Production Overview](Cumulative_Prod_Viz.ipynb) 
The Kansas cumulative oil production interactive map was produced using plotly.express and 	exported to HTML using plotly.io.  

* Requires: `county_production_monthly.csv`
* Produces: Final interactive Cumulative Kansas Oil Visual   
 
### [3.2 Plotly Animation R](Plotly_Animation_R.ipynb) 
Used to clean and join data for the visualization of the three counties represented in the data 	story and built test animated visuals in R with the plotly package. 

* Requires: `Ellis_Labor_population.csv`, `Dickinson_Labor_population.csv`, `Riley_Labor_population.csv`, `county_production_monthly.csv`, `oil_prices.csv` 
* Produces: `animation_viz_data.csv` 
	 
### [3.3 Python Plotly](Python_Plotly.ipynb) 
Used cleaned visualization data to built python animated plotly  plot of the Dickinson, Ellis and 	Riley county labor force participation rate over oil price for data story. 

* Requires: `animation_viz_data.csv` 
* Produces: `laborforceoilpriceplot.html` 
 
### [3.4 Production vs Price vs Time](3-Production_vs_Price_vs_Time_Final_Viz.ipynb) 
Used to bring in the cleaned dataset, review it briefly, plot it in plotly, then export to html. 

* Requires: `prod_price_inf_merge.csv` 