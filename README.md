# Tesla-Rev-Web-Scrape

import yfinance as yf

tsla=yf.Ticker("tsla")
tsla_data = tsla.history(period="max")

tsla_data.reset_index(inplace=True)
tsla_data.head()

#results showed for this


url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.html"

html_data = requests.get(url).text


soup = BeautifulSoup(html_data,"html.parser")




tesla_revenue = pd.DataFrame(columns = ["Date","Revenue"])

for result in soup.find_all('table', attrs={'class':'historical_data_data table table'}):
    if result.find("th").getText().startswith("Tesla Quarterly Revenue"):
       for row in table.find("tbody").find_all("tr"):
            col = row.find_all("td")
            if len(col) != 2: continue
            Date = col[0].text
            Revenue = col[1].text.replace("$","").replace(",","")
            tesla_revenue = tesla_revenue.append({"Date":Date, "Revenue":Revenue}, ignore_index=True)  
            
tesla_revenue.head()

#results did not show for this
