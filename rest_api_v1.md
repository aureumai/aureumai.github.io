---
title: API V1
layout: default
nav_order: 2
---

## Rest API

The following endpoints are available in the Volland v1 Rest API.

**Base URL:**

`https://p9w2ycklv5.execute-api.us-east-1.amazonaws.com/beta`

#### Authentication

For testing purposes, your JWT key is passed in the request headers under the "authorization". Normally that key would be passed by the FE whenever data is called.

`"authorization": "jwt-key"`

____________________________________________________________________________

#### 

**GET** _/volland-live-api-strikes?ticker{desired-ticker}_


Get the list of strikes and expirations for a given ticker.

##### Parameters

| **ticker** | any of the ticker available on volland|


##### Response Object

```json
{
	"ticker": "AAPL",
	{
		"strikes": [10, 15, 20, ...]
		"expirations": [\"2024-12-20\", \"2023-06-16\", \"2023-12-29\",...]
	} 
}
```
