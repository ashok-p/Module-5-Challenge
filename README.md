# Module-5-Challenge - Financial Planning with APIs and Simulations
This program utilizes the APIs and Monte Carlo Simulations to create an application for Financial Planning for Emergencies and Retirement. 

The Starter Code was provided along with the Monte Carlo Simulation library.

---

## User Story
The CTO of a large Credit Union board wants an application to help its members evaluate their financial health. Specifically, the application should be able to 1) assess current savings and forecast if they have enough reserves for their emergency fund, and 2) be able to forecast a reasonably effective retirement plan based upon their crypto, stock and bond portfolios. 

---

## Acceptance Criteria  
The application must meet the following acceptance criteria:  

### Part 1: Financial Planner for Emergencies  

* account for the member savings from his/her crypto and stock (SPY) & bond portfolios (AGG),  
* create a pie chart displaying the crypto vs stock & Bond portfolios
* based upon 3 times the member's monthly income as the emergency fund, forecast if the member:  
    - has enough savings to fund the emergency fund  
    - has just enough savings to fund the emergency fund  
    - does not have enough savings to fund the emergency fund  

### Part 2: Financial Planner for Retirement  

* use .env file for storing the Alpaca API and Secret Keys
* based upon 3 years of historical stock (SPY) and bond (AGG) data, run Monte Carlo Simulations with 500 samples for a 30 year period with a 60/40 (SPY/AGG) mix
* based upon the same historical data, run the Monte Carlo Simulations for a 10 year period with 80/20 mix.
* for both, the 30 and 10 year simulations:  
    - plot the overlay line plot of the simlulation   
    - plot the probability distribution of the simulation  
    - print summary statistics
* recommend if increasing the stock portion from 60 to 80% will help the member retire early  

---

## The Application  

The application follows these stages: 

### Part 1: Financial Planner for Emergencies  
* Assumptions: 
    - monthly income $12,000  
    - crypto wallet  
        - btc_coins = 1.2  
        - eth_coins = 5.3  
    - Stock and Bond Portfolio
        - SPY - 110 shares
        - AGG - 200 shares
* Evaluate the Crypto Portfolio  
    - get the current BTC and ETH data using the **requests** library API calls to Free Crypto API with the following URLs:
        - btc_url = "https://api.alternative.me/v2/ticker/Bitcoin/?convert=USD". 
        - eth_url = "https://api.alternative.me/v2/ticker/Ethereum/?convert=USD"
    - parse the json data for the BTC and ETH prices and calculate the total value of the crypto wallet
* Evaluate the Stock & Bond Portfolio
    - Use ALPACA SDK
    - obtain the ALPACA_API_KEY and ALPACA_SECRET_KEY fetched from the .env file
    - make an **Alpaca REST object** using the API and SECRET keys.
    - use the **Alpaca get_bars** function to get the SPY and AGG data for the given date
    - calculate the total stock & bond portfolio from the SPY and AGG closing prices and the number of respective shares in the portfolio.  
* Create a **pie chart** showing the crypto vs stocks/bonds portfolio  
* Evaluate the Emergency Fund -  
    - set the **emergency fund** amount to **3*monthly_income**  
    - using just the **stock & bond** portfolio, evaluate:  
        - if the portfolio value > emergency funds, implying more than enough funds  
        - if the portfolio value = emergency funds, implying just enough funds  
        - if the portfolio value < emergency funds, implying need more funds 

### Part 2: Financial Planner for Retirement  
* Assumptions:
    - Use **Alpaca SDK** for fetching 3 years of historical financial data
    - 30 years Monte Carlo simulation with 60/40 (SPY/AGG) split
    - 10 years Monte Carlo simulation with 80/20 (SPY/AGG) split
* make Alpaca **get_bars** call to get the 3 yrs historical data
* reorganize the data to get ready for **MCSimulation**.
* Monte Carlo Simulation for a 30 year period, with 500 samples and a 60/40 portfolio
    - run the simulation
    - visualize the simulation by plotting the simulation **overlay line plot**
    - visualize the probability distribution by plotting the **histogram**
    - generate the **summary statistics**
* Monte Carlo Simulation for a 10 year period, with 500 samples and a 80/20 portfolio
    - run the simulation
    - visualize the simulation by plotting the simulation **overlay line plot**
    - visualize the probability distribution by plotting the **histogram**
    - generate the **summary statistics**
* analyze the two simulations identifying the lower and upper bounds of the **95% CI** values and calculating the portfoiio values. Compare the two scenarios and answer if he/she can retire after 10 years.

---

## Technologies
The application is developed using:  
* Language: Python 3.7,   
* Packages/Libraries: Pandas, os, Alpaca SDK, Resources, json, MCForecastTools for MCSimulation, matplotlib
* Development Environment: VS Code and Terminal, Anaconda 2.1.1 with conda 4.11.0, Jupyterlab 3.2.9  
* OS: Mac OS 12.1

---
## Installation Guide
Following are the instructions to install the application from its Github respository.  

### Clone the application code from Github as follows:
copy the URL link of the application from its Github repository      
open the Terminal window and clone as follows:  

    1. $cd to_your_preferred_directory_where_you want_to_store_this_application  
    
    2. $git clone URL_link_that_was_copied_in_step_1_above   
    
    3.  $ls     
        Module-5-Challenge    
        
    4. $ cd Module-5-Challenge     

At this point you will have the the entire application files in the current directory as follows:

    * README.md                   (this file that you are reading)
    * financial_planning_tools.ipynb      (the application jupter lab notebook)
    * MCForecastTools.py                       (Monte Carlo Simulation library)
    * SAMPLE.env                       (sample env file - came with starter code)
    * Images                           (images folder - came with starter code)

---

## Usage
The following details the instructions on how to run the application.  

### Setup the environment to run the application
Setup the environment using conda as follows:

    5. $conda create dev -python=3.7 anaconda  
    
    6. $conda activate dev  
    
    7. $jupyter lab  

---

### Run the Application
THIS ASSUMES FAMILIARITY WITH JUPYTER LAB. If not, then [click here for information on Jupyter Lab](https://jupyterlab.readthedocs.io/en/stable/).  

After step 7 above, this will take you to the jupyter lab window, where you can open the application notebook **risk_return_analysis.ipynb** and run the application.  

**NOTE**:
>Your $ prompt will look something like __(dev) ashokpandey@Ashoks-MBP loan_qualifier_app$__ ,  with:  
    - '(dev)' indicating the activated 'dev' environment,   
    - ' ashokpandey@Ashoks-MBP ' will be different for you as per your environment, and   
    - 'loan_qualifier_app' directory is where app.py is located.  
    - '$' sign is the dollar prompt  

---

## Contributors
Ashok Pandey - ashok.pragati@gmail.com   
www.linkedin.com/in/ashok-pandey-a7201237

---

## License
The source code is the property of the developer. The users can copy and use the code freely but the developer is not responsible for any liability arising out of the code and its derivatives.

---