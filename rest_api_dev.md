---
title: API Development
layout: default
nav_order: 3
---

## Rest API

The following development endpoints are available in the Volland v1 Rest API.

**Base URL:**

`https://gtioutaqt3.execute-api.us-east-1.amazonaws.com/v1`

#### Authentication

For testing purposes, your JWT key is passed in the request headers under the "authorization". Normally that key would be passed by the FE whenever data is called.

`"authorization": "jwt-key"`

____________________________________________________________________________

#### 

**GET** _/volland-live-api-strikes-dev?ticker={desired-ticker}_


Get the list of strikes and expirations for a given ticker.

##### Parameters

| **ticker** | any of the ticker available on volland|


##### Response Object

```json
{"TQQQ": 
	{
		"strikes": [3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0, 10.0, 11.0, 12.0, 13.0, 14.0, 15.0, 16.5, 16.0, 18.5, 19.5, 20.5, 21.0, 19.0, 23.0, 24.5, 25.0, 26.5, 27.5, 24.0, 27.0, 26.0, 28.0, 29.0, 31.0, 32.0, 34.0, 35.0, 30.5, 37.0, 38.0, 39.0, 40.0, 33.0, 42.5, 36.0, 37.5, 45.0, 47.5, 50.0, 52.5, 55.0, 57.5, 60.0, 62.5, 65.0, 67.5, 68.5, 69.0, 70.0, 71.5, 71.0, 73.5, 74.0, 75.0, 72.0, 77.0, 78.0, 79.5, 80.0, 79.0, 82.5, 81.5, 80.5, 85.0, 17.0, 17.5, 87.5, 81.0, 90.0, 18.0, 92.5, 95.0, 97.5, 100.0, 20.0, 102.5, 105.0, 21.5, 107.5, 110.0, 22.5, 22.0, 112.5, 115.0, 23.5, 117.5, 120.0, 122.5, 125.0, 25.5, 127.5, 130.0, 132.5, 135.0, 28.5, 29.5, 30.0, 31.5, 32.5, 69.5, 70.5, 14.5, 72.5, 73.0, 74.5, 75.5, 15.5, 76.0, 76.5, 77.5, 78.5, 82.0, 83.0], 
		"expirations": ["2023-04-14", "2023-03-24", "2023-04-21", "2023-04-28", "2023-04-06", "2024-01-19", "2023-03-17", "2023-03-31", "2023-09-15", "2023-06-16", "2025-01-17"]
	}
}
```

____________________________________________________________________________

#### 

**GET** _/volland-live-api-exposure-dev?ticker={desired-ticker}&greek={desired_greek}&expirations={}&kind={kind}_


Get the exposure for the requested ticker

##### Parameters

| **ticker**      | Any of the ticker available on volland| 'SPY'                             |
| **greek**       | The desired greek                     | 'charm'                           |
| **expirations** | A list of expirations or *            | '*', ["2023-03-31", "2023-04-06"] |
| **kind**        | Designate call or put                 | 'call', 'put', or '*'             |


##### Response Object

```json
{
  "statusCode": 200,
  "body": {"SPY": 
  			{"exposure": 
  				{"charm": 
  					{"230331": 
  						{"255.0": {"call": 1854.5504258826006},
  						 "260.0": {"call": -3090.917376471003},
  						 "265.0": {"call": -6800.0182282362075},
  						 "270.0": {"call": -2472.7339011768026},
  						 ...
  						}
  					}
  				}
  			}
		"underlying": 402.5,
  		"last_update": timestamp
}
```


____________________________________________________________________________

#### 

**GET** _/volland-live-api-agg_charm-dev?ticker={desired-ticker}_


Get the aggregate charm exposure for the requested ticker

##### Parameters

| **ticker** | any of the ticker available on volland|


##### Response Object

```json
{
	"SPY": {
		"agg_charm": 103638757.20335546, 
		"last_update": 1679411110
	}
}
```


____________________________________________________________________________

#### 

**GET** _/volland-live-api-ges_strike_list-dev?ticker={desired-ticker}


This end-point is to be used in conjunction with the end-point immediately following. It provides a list of possible theoretical underlyings for generating a theoretical gamma curve were the price of the underlying to reach that level. These are the only valid values for the underlying parameter below.

##### Parameters

| **ticker** | any of the ticker available on volland|


##### Response Object

```json
{
		"ticker": "SPY", 
		"theoretical_gamma_strikes": [515.0, 520.0, 525.0, 530.0, 535.0, 540.0, 545.0, 550.0, 555.0, 560.0, 565.0, 570.0, 575.0, 580.0, 585.0, 590.0, 595.0, 600.0, 605.0,...]
}
```

____________________________________________________________________________

#### 

**GET** _/volland-live-api-gamma_exposure_strike-dev?ticker={desired-ticker}&underlying={590.0}_


This one is a bit unique. If you provide it with a ticker and a 'strike' that you want considered as the underlying, hypothetically, it will return the institutional DAG and Gamma exposure for that case.

##### Parameters

| **ticker** | any of the ticker available on volland|
| **underlying** | hypothetical strike to consider as the underlying


##### Response Object

```json
{
		"ticker": "SPY",
		"theoretical_exposure": {
													"gamma": {
																		"2023-04-11": {"330.0": {"call": 0.0, "put": 0.0}, 
																									"336.0": {"put": 0.0},
																									"337.0": {"put": 0.0},
																									...
																								}
																		...
																	}
														}
}
```


____________________________________________________________________________

#### 

**GET** _/volland-live-api-eod-dev?ticker={desired-ticker}


Provide this endpoint a ticker and it will return the EOD status for that ticker.

##### Parameters

| **ticker** | any of the ticker available on volland|


##### Response Object

```json
{
		"gamma_exp": 0.0236956443872193,
		"vanna_exp": 41.39826201178064,
		"theta_exp": 99.77985528692405,
		"delta_exp": 64.26425897855798,
		"vega_exp": 0.1499460067449947
}
```


____________________________________________________________________________

#### 

**GET** _/volland-live-api-summary-dev?ticker={desired-ticker}

Provide this endpoint a ticker and it will return the current price, notional equity volume and most recent VIX calculation.


##### Parameters

| **ticker** | any of the ticker available on volland|


##### Response Object

```json
{
		"notionalVolume": 236719724429.53055,
		"vix": 18.232903496278553,
		"price": 407.63
}
```