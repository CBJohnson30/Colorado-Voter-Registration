# Colorado Voter Registration

In this repo, I will be going through my Capstone Project for the General Assembly Immersive I took. This project was about Colorado Voter Registration numbers in the years 2013 to 2017 and how they change over time. One of the main questions I had going into this project was to see if elections results could tell you anything about the following years' registration numbers. Does momentum of winning the election carry over to an increase of voter registrations for the winning party? I will be breaking this down to a county level to have smaller sample sizes and more samples to look at.  I will also be forecasting out voter registration numbers for each county as well. 

IMPORTANT! - You may click on any graph to go to my Tableau Public profile so every graph will be interactive. You may also view all other visuals I made that were not included in this repo.  

## Data

All of the data came from the [Colorado Secretary of State's website](https://www.sos.state.co.us/). I was able to export all of the data in excel files. All of these files were formatted and there was one for each month I wanted to look at, 72 in all. Some of these files were formatted differently than the others and before 2015 they were .xls files and 2015 and after they were .xlsx files. This caused some unexpected problem when turning the data into a format I can work with Pandas. All of this was done in the workbook [Excel to CSV.ipynb](https://github.com/CBJohnson30/Colorado-Voter-Registration/blob/master/Excel%20to%20CSV.ipynb). 
  - Key notes about the data:
    - I considered all pre-reg voters as active voters. Before 2015 pre-reg voters were not in the excel files. 
    - I counted all other political parties besides Democrat and Republican as unaffiliated voters. This was to simplify my visuals and models.

Below are two graphs that show all of my data. the first one is showing Grand Total of voters. This included active and inactive registered voters. The second one shows the total of active voters by registration type. 

[![Total_reg](https://github.com/CBJohnson30/Colorado-Voter-Registration/blob/master/Images/total_reg.png)](https://public.tableau.com/profile/cbjohnson30#!/vizhome/Colorado_Voter_Registration/Total)

[![reg_type](https://github.com/CBJohnson30/Colorado-Voter-Registration/blob/master/Images/reg_type.png)](https://public.tableau.com/profile/cbjohnson30#!/vizhome/Colorado_Voter_Registration/Active)

Major insights from these graphs:
  1. The major spike in July 2013 is because of Colorado HB 13-1303, Create the Voter Access and Modernized Elections Act. This changed the definition of an inactive voter. Before this bill, if you did not vote in the previous election you became an inactive voter. After the bill, if USPS returned your ballot you became an inactive voter. If you received your ballot but did not vote for whatever reason you are still labeled as an active voter. Because of this definition change, I was not able to go back past 2012 as it changed the definition of one of the major variables. 
  
  2. I was surprised to find out that September of 2016 was the first time in my data that there were more registered Democrats than Republicans. From growing up in the state I thought it would have been a lot closer throughout this time frame, if not having more registered Democrats. I was shocked to find out during 2015 there were roughly 60,000 more registered Republicans than Democrats. 
  

## Analysis

For my analysis of the data, I will be creating a few labels for each county to be able to compare them visually.

The first label I made was how a county voted historically. A county could either be Democratic, Republican, or Swing. I did this in another repo in my git hub called, [Colorado-County-Voting-Classification](https://github.com/CBJohnson30/Colorado-County-Voting-Classification). This allowed me to see if this label for a county made counties behaved differently at any time. 

Another form of analysis I did was using a time series tool called pct_change (percent change). In my example, this gives me the percent change from the previous month. This was useful to see if any party was increasing or decreasing in voter registration. This transformation happened in the notebook called, [Change from the Previous Month](https://github.com/CBJohnson30/Colorado-Voter-Registration/blob/master/Change%20from%20Previous%20Month%20.ipynb). I also used this in the last piece of analysis I did.  Below is a graph of the change from the previous month by voter registration type. 

[![change_reg_type](https://github.com/CBJohnson30/Colorado-Voter-Registration/blob/master/Images/change_reg_type.png)](https://public.tableau.com/profile/cbjohnson30#!/vizhome/Colorado_Voter_Registration/ActiveChange)

The most interesting note about this graph is that besides a few months before primaries unaffiliated voters are almost always growing at a faster rate than either party is.

The last piece of analysis I did was to look at registration changes in counties by who they voted for. This took place in the notebook called, [Election results](https://github.com/CBJohnson30/Colorado-Voter-Registration/blob/master/Elections%20results.ipynb). I know this is going to where I am going to be able to answer the question if the momentum of winning the election carry over to an increase of more voter registration for the winning party. The three elections I used for this was 2012 presidential, 2014 gubernatorial and 2016 presidential. I thought they would have the most coverage of each election and influence passion before and after each election the most. Below are two graphs of voter registration changes from right after the 2016 election to the 2017 election. One graph shows counties won by Hillary Clinton and the other shows counties won by Donald Trump.

[![2017_trump](https://github.com/CBJohnson30/Colorado-Voter-Registration/blob/master/Images/Trump_2017.png)](https://public.tableau.com/profile/cbjohnson30#!/vizhome/Colorado_Voter_Registration/2016ElecLabelParty)

[![2017_clinton](https://github.com/CBJohnson30/Colorado-Voter-Registration/blob/master/Images/Hillary_2017.png)](https://public.tableau.com/profile/cbjohnson30#!/vizhome/Colorado_Voter_Registration/2016ElecLabelParty)

There are two major take aways from these two graphs. 
  1. The difference in party registered voters throughout the year 2017. In counties that Donald Trump won you see a clear increase in Republican registered voters throughout the year while Democratic registered voters fluctuate while mostly decreasing. In counties won by Hillary Clinton, this same pattern does not happen. Both parties voter registrations tend to fluctuate together throughout the year. Taking this from a state point of view if a county voted for the losing candidate(Hillary Clinton won Colorado), you will see an increase in the losing parties voter registration numbers. You will find a similar situation happen in 2015 compared to the 2014 gubernatorial race. 
  
  2. Another important thing to note is that the rate of increase of unaffiliated voter registrations is higher in counties won by Donald Trump than Hillary Clinton. In counties won by Donald Trump unaffiliated voters increased by an average of .008125% per month while counties won by Hillary Clinton only increased by .00675% per month.
  
To answer the question posed in the introduction of this readme. Political momentum from winning an election does not carry over to the following year in terms of new voter registrations. When viewed at a county level it is the opposite. If a county votes a different way than the states result the county will see an increase in voters registrations for the party that lost the state election. This effect does not only cover political parties registered voters but unaffiliated voters as well. 


## Forecasting

This last part of this project was to forecast out voter registration through 2018. This was all done in the notebook called [Grand Total Time Series](https://github.com/CBJohnson30/Colorado-Voter-Registration/blob/master/Grand%20Total%20Time%20Series.ipynb) and [Registration Type Time Series](https://github.com/CBJohnson30/Colorado-Voter-Registration/blob/master/Registration%20Type%20Time%20Series%20.ipynb). My first step in this process was to use time series techniques to predict on its self. The goal was to overfit these models as much as possible to generate dependent variables that I know will help out my model when it comes to forecasting. I came up with two dependent variables that overfit my models. They were "drop months" when counties remove people from voter registries, and "election buzz months", few months before even year elections when get out to vote campaigns are in full gear.

After I had these it was time to pick a forecasting model. I chose to use a seasonal ARIMA model. ARIMA stands for autoregressive integrated moving average. The seasonal part is very important because of the pattern it appears in the data, this is what is known as a season. For this data, the season is  2 years or 24 months. This model takes into account not only what happens a few time periods before the forecasting date but the season before as well. Below is the forecasting graph for registration types and forecasting for total registered voters can be viewed [here](https://public.tableau.com/profile/cbjohnson30#!/vizhome/Colorado_Voter_Registration/RegTotalForecast).

[![reg_type_forecast](https://github.com/CBJohnson30/Colorado-Voter-Registration/blob/master/Images/forecast_reg_type.png)](https://public.tableau.com/profile/cbjohnson30#!/vizhome/Colorado_Voter_Registration/RegtypeForecast)

To the eye, these forecasts may look reasonable but I do not trust these forecasts as much as I would like. There are a few reasons for this but they all come back to is that I do not have enough data for my forecast to be correct. With the data, I have available to me this is a problem I can not solve either. The definition of an inactive and active voter changed in 2013 as mentioned above does not allow me to go back any farther than I already do.

My model can only look back one season if I include any autoregressive and moving average components. This is a problem because of the massive influx of voters in 2016 due to the controversial presidential election. Looking at Novembers in even years for the grand total of registered voters to goes: 2012 - 3.65 million, 2014 - 3.66 million and 2016 - 3.87 million. My forecast predicts November of 2018 to have 4.02 million voters. I do not think the population of Colorado, roughly 5.6 million be able to sustain this growth in voter registrations. If I was able to look back three or even 4 seasons It would help mitigate the large increase in 2016 and I think it will produce better results. 
