```python
while True:
    print("Enter in a country name: (Type areas for list of areas)")
    user_in = input()
    
    #if user types areas recursively show all areas
    if user_in == 'areas':
        recursive_countries(list=areas, n=0)
    #if the country is in the areas list then its a valid element of the dataframe
    elif user_in in areas:
        country = user_in
    
    #user input is acceptable
    if country == user_in:
        print("You have chosen", country + ", nice choice! Lets see the data.")
        country_df = df[df.countriesAndTerritories == country]

        #fix the order of the data
        country_df = country_df.iloc[::-1]
        
        print("This is the head of the data for " + country )
        print(country_df)

        country_df.loc[:,"dateRep"] = pd.to_datetime(country_df['dateRep'], format="%d/%m/%Y").dt.strftime("%Y-%m-%d")

        #stacked subplots
        fig, ax = plt.subplots(nrows=2, ncols=1)
        fig.suptitle("Cases and Deaths for Data Date Range for " + country)
        plt.setp(ax[0].xaxis.get_majorticklabels(), rotation=25)

        ax[0].plot(country_df.dateRep, country_df.cases)
        ax[0].set_xlabel("Date since data collection in " + country + "(interval: 20 days)")
        ax[0].set_ylabel("Cases in " + country)
        plt.setp(ax[1].xaxis.get_majorticklabels(), rotation=25)
        ax[1].plot(country_df.dateRep, country_df.deaths)

        ax[1].set_xlabel("Date since data collection in " + country + "(interval: 20 days)")
        ax[1].set_ylabel("Deaths in " + country)
        days = mdates.DayLocator(interval=20)
        ax[0].xaxis.set_major_locator(days)
        ax[1].xaxis.set_major_locator(days)
        fig.tight_layout()

        plt.show(block=True)
```
