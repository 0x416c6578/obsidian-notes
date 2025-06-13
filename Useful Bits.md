Removing Linkedin feed and news with uBlock:
```go
www.linkedin.com##[aria-label^="Main Feed"]
www.linkedin.com##[aria-label^="LinkedIn News"]
```
___
Small Python script to retrieve Vanguard index prices:
```python
#!/usr/bin/env python3  
  
from requests import get  
import json  
  
if __name__ == '__main__':  
    funds = {  
        "Life Strategy 20": "https://www.vanguardinvestor.co.uk/api/funds/vanguard-lifestrategy-20-equity-fund-gbp-gross-accumulation-shares",  
        "Life Strategy 40": "https://www.vanguardinvestor.co.uk/api/funds/vanguard-lifestrategy-40-equity-fund-accumulation-shares",  
        "Life Strategy 60": "https://www.vanguardinvestor.co.uk/api/funds/vanguard-lifestrategy-60-equity-fund-accumulation-shares",  
        "Life Strategy 80": "https://www.vanguardinvestor.co.uk/api/funds/vanguard-lifestrategy-80-equity-fund-accumulation-shares",  
        "Life Strategy 100": "https://www.vanguardinvestor.co.uk/api/funds/vanguard-lifestrategy-100-equity-fund-accumulation-shares"  
    }  
  
    fundPrices = {}  
  
    for fund in funds.items():  
        fundName, fundUrl = fund  
  
        httpRes = get(fundUrl)  
        jsonContent = json.loads(httpRes.content)  
  
        fundPrices[fundName] = jsonContent.get("navPrice").get("value")  
  
    fundNames = list(fundPrices.keys())  
    fundValues = list(fundPrices.values())  
  
    print(json.dumps(dict(zip(fundNames, fundValues)), indent="  "))
```