
# My Data Analytic project to decode 95,107 vins into nice vehicle infos.

### 1. Data: i download FHV data from data: https://data.cityofnewyork.us/Transportation/For-Hire-Vehicles-FHV-Active/8wbx-tsch

### 2. Python: to scrape the infos from the website (tooks over 18hrs just to extract datas) and export xlsx/csv
****sample codes: for Full codes go to jupiternotebook/script.ipynb
  ```      
        import requests #
        from bs4 import BeautifulSoup #read the webpage
        webtarget = "https://     e?vin="  # missing
        all_cars= []
        for car in fhv:
            try:
                    source = requests.get(webtarget+car)
                    source.raise_for_status()
                    soup = BeautifulSoup(source.text)
                    info = soup.find('h2').text
                    all_cars.append(car+' ' +info)
                    #print(info)
            except Exception as e:
                    print(e)
         
         #print(all_cars)
         all_cars=pd.Series(all_cars)
         
         all_cars.to_csv('all_cars.csv',header=False, index=False)  # export to all_cars.csv file

```
example:

      JN8AZ2NE9J9194149 INFINITI QX80 2018 Base
      4T1BF1FK2HU438475 TOYOTA Camry 2017
      5TDKK3DC0DS371798 TOYOTA Sienna 2013 LE
      ..........

### 3. SQL - data cleaning and created new Column for Trim and Fuel-type: (gas, hybrid or EV)
*** new column example
                      
                      | vin number        | Make     | Model | Year |Trim | Fuel-Type  | 
                      | ----------        | ----     | ----- | ---- | ----|      ----  | 
                      |JN8AZ2NE9J9194149  | INFINITI | QX80  | 2018 | Base|  Gas       | 
      
### 4. Tableau: to create dashboard

