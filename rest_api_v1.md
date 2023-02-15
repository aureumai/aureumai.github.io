---
title: API V1
layout: default
nav_order: 2
---

## Rest API

The following endpoints are available in the Volland v1 Rest API.

**Base URL:**

`https://api.vol.land/greek-exposure`

### Get Greek Exposure

#### Authentication

Your API key is passed in the request headers under the "x-api-key".

`"x-api-key": "YOUR-API-KEY"`

____________________________________________________________________________

#### Greek Exposure

**GET** _/volland-greek-exposure?greek={desired-greek}&ticker={desired-ticker}_
{: .label } 


Get the greek exposure for a given ticker-greek combo.

##### Parameters


| **greek**  | any of the greeks available on volland|


| **ticker** | any of the ticker available on volland|


##### Response Object

```json
{
	"ticker": "AAPL",
	"greek": "charm",
	"exposure": {
		"230217": {"100": {"call": 0, "put": 0}},
		...
	} 
}
```