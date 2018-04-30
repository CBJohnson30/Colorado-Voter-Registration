# Colorado Voter Registration

In this Repo I will be going through my Capstone Project for the General Assumbly Immersive I took. This project was about Colorado Voter Registrtion numbers in the years 2013 to 2017 and how they change over time. One of the main questions I had going into this project was to see if elections results could tell you anything about the following years registration numbers. Does momentem of winning the election carry over to an increase of more voter registration for the winning party? I will be breaking this down to a county level to have smaller sample sizes and more samples to look at.  I will also be forecasting out voter registration numbers for each county as well. 

IMPORTANT! - You may click on any graph to go to my Tableau Public profile so every grapgh will be interactive. You may also view all other visuals I made that were not included in this repo.  

## Data

All of the data came from the [Colorado Secretary of State's website](https://www.sos.state.co.us/). I was able to export all of the data in excel files. All of these files were formatted and there was one for each month I wanted to look at, 72 in all. Some of these files were formatted differently than the others and before 2015 they were .xls files and 2015 and after they were .xlsx files. This caused some unexpected problem when turing the data into a format I can work with in Pandas. All of this was done in the workbook [Excel to CSV.ipynb](). 
  - Key notes about the data:
    - I considered all prereg voters as active voters. Before 2015 prereg voters were not in the excel files. 
    - I counted all other political parties besides Demorcate and Republican as unifillieated voters. This was to simplfiy my visuals and models. 

Below are two graphs that show all of my data. the first one is showing Grand Total of voters. This included active and inactive registrated voters. The second one shows the total of active voters by registration type. 

[![Total_reg]()]()

[![reg_type]()]()

Major insights from these graphs:
  1. The major spike in July 2013 is because of Colorado HB 13-1303, Create the Voter Access and Modernized Elections Act. This changed the difination of an inactive voter. Before this bill if you did not vote in the previouse election you became a inactive voter. After the bill, if USPS returned your ballot you became an inactive voter even if you did not vote. Example - If you received your ballot but did not vote for what ever reason you are still labeled as an active voter. Because of this defination change I was not able to go back past 2012 as it changed the defination of one of the major vareribles. 
  
  2. I was surprised to find out that September of 2016 was the first time in my data that there were more registered Deomcrates than Repbulicans. From growing up in the state I thought it would of been a lot closer thoughout this time frame, if not having more regirstared demorates. I was shocked to find out during 2015 there were roughly 60,000 more registared repbulicans than Democrates. 
  

## Analysis

For my analysis of the data I will be creating a few labels for each county to be able to compaire them visually. 

The first label I made was how a county voted historically. A county could either be Democratic, Republician, or Swing. I did this in another repo in my git hub called, [Colorado-County-Voting-Classification](https://github.com/CBJohnson30/Colorado-County-Voting-Classification). This allowed me to see if this label for a county made counties behaved differently at any time. 

Another form of analysis I did was using a time series tool called pct_change (percent change). In my example this gives me the percent change from the previous month. This was useful to see if any party was increasing or decreasing in voter registration. This transformation happened in the notebook called, [Change from the Previous Month](). I also used this in the last peice of analysis I did.  Below is a graph of the change from the previous month by voter registration type. 

[![change_reg_type]()]()

The most interesting note about this graph is that besides a few months before primaries unifilliated voters are almost always growing at a faster rate than either party is.

The last peice of analysis I did was to look at registration changes in counties by who they voted for. This took place in the notebook called, [Election results](). I know this is going to where I am going to be able to answer the question if momentem of winning the election carry over to an increase of more voter registration for the winning party. The three elections I used for this was the 2012 presidentional, 2014 gubitorial and 2016 presidentional. I thought they would have the most coverage of each election and influance passion before and after each election the most. Below are two graphs of voter registration changes from right after the 2016 election to the 2017 election. One graph shows counties won by Hillary Clinton and the other shows counties won by Donald Trump.

[![2017_trump]()]()

[![2017_clinton]()]()

There are two major take aways from these two graphs. 
  1. The difference in party registared voters throughout the year 2017. In counties that Donald Trump won you see a clear increase in Rupublican registared voters throughout the year while Democratic registared voters flucuate while mostly decreasing. In counties won by Hillary Clinton this same pattern does not happen. Boths parties voter registations tends to flucuate togeather throught the year. Taking this from a state point of view if a county voted for the losing canadiant (Hillary Clinton won Colorado), you will see a increase in the loseing parties voter registation numbers. You will find a simlar situation happen in 2015 compaired to the 2014 gubitotial race. 
  
  2. Another important thing to note is that the rate of increase of unifillated voter registrations is higher in counties won by Donald Trump than Hillary Cilinton. In counties won by Donald Trump unifillieated voters increased by an average of .008125% per month while counties won by Hillary Clinton only increased by .00675% per month. 
  
To answer the question posed in the introduction of this readme. Political momentum from winning an election does not carry over to the following year in terms of new voter registrations. When viewed at a county level it is the oppisite. If a county votes a different way than the states result the county will see an incease in voters registrations for the party that lost the state election. This effect does not only cover a political parties registarted voters but unifillated voters as well. 


## Forecasting

This last part of this project was to forecast out voter registration through 2018. This was all done in the notebook called [Grand Total Time Series]() and [Registration Type Time Series](). My first step in this process was to use time series techniques to predict on its self. The goal was to overfit these models as much as possible to generate dependate variables that I know will help out my model when it comes to forcasting. I came up with two dependant variables that overfit my models. THey were drop months, when counties remove people from voter registries, and election buzz months, few months before even year elections when get out to vote campaigns are in full gear. 

After I had these it was time to pick a forecasting model. I chose to use a seasonal ARIMA model. ARIMA stands for autoregressive integrated moving average. The seasonal part is very important because of the pattern at appears in the data, this is what is known as a season. For this data the season is  2 years or 24 months. This model takens into account not only what happenes a few time perioeds before the forcasting date but the season before as well. Below is the forcasting graph for regerstrations types and forcasting for total regerstared voters can be viewed [here](). 

[![reg_type_forecast]()]()

