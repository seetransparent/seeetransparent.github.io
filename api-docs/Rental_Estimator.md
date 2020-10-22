# Welcome

Welcome to the documentation for the Transparent Rental Estimator API. 

Through this API, Transparent intends to provide data-based rental estimations for Short Term Rentals.

We believe a broad span of players in the Short Term Rental industry could benefit from it and use cases are many, from finding a potential investment by estimating its potential return to tracking competitors' performance. If you want to explore how to make the most out of this API, please reach out to us.

Having a clear and up-to-date API Documentation is one of the numerous ways we serve our clients. So if you have any questions or you spot a mistake, just send us a note.

# Key Principles

> Overview

Transparent Rental Estimaor API relies on Transparent Short Term Rental proprietary data. It benefits from a worldwide coverage on the four main Online Travel Agencies (OTA) and it goes back to 2017.

The Rental Estimator API allows you to estimate the performance of a current or potential Short Term Rental property.

Having worked closely with Property Managers, Investors and other players in the Short Term Rental industry, we designed this API using a fairly common model. Based on the location and property characteristic inputs in the API, we look at the rental performance of the previous years on surrounding Short Term Rental properties with similar characteristics.

It delivers Short Term Rental estimations on revenue, occupancy and ADR aggregated annually and broken down by each month of the year. 

The API has a second endpoint delivering a sample of up to 50 surrounding Short Term Rental properties used in the estimations including their respective listing URLs and indivudual performance. Both endpoints require the same inputs.



# Endpoint 1: aggregate metrics

Returns market aggregate metrics for the full year of 2019, with yearly and monthly metrics including ADR, revenue and occupancy.

```
https://listingroiapi.seetransparent.com/aggregated?latitude=40.410754&longitude=-3.700917&radius_meters=5000&type=ENTIRE_HOME&subtype=APARTMENT
```


| Params | Required | Description |
| ------ | ------ | ------ |
| API Key | `Required` | {{transparent_api_key}} |
| latitude | `Required`  | The latitude of the property or geographical area to be queried. Number values are expected. |
| longitude | `Required`  | The longitude of the property or geographic area to be queried. Number values are expected. |
| radius_meters | `Required`  | Refers to the radius around the coordinates you want to include in the search result. Minimum radius allowed is 500 meter, maximum radius allowed is 10000 meter. Number values are expected. |
| type | `Required`  | Relevant to define the type of properties to be included in the search result. Allowed values: ENTIRE_HOME, PRIVATE_ROOM, SHARED_ROOM |
| subtype | `Required`  | Relevant to define the subtype of properties to be included in the search result. Allowed values: APARTHOTEL, APARTMENT, BED & BREAKFAST, BOAT, BUNGALOW, CASTLE, CHALET, DORM, GLAMPING, GUEST_HOUSE, HOSTEL, HOTEL, HOUSE, OTHER, RV, TOWNHOUSE, VILLA |
| bedrooms | Optional | Relevant to define the size of properties to be incuded in the search result. Inputs are optional and multiple integer values are possible. |
| bathrooms | Optional | Relevant to define the size of properties to be incuded in the search result. Inputs are optional and multiple integer values are possible. | 
| capacity | Optional | Relevant to define the size of properties to be incuded in the search result. Inputs are optional and multiple integer values are possible. | 
| pool | Optional | Relevant to define the amenities available at the properties you want to include in your search result. Inputs are optional and 0 and 1 values are expected (0 for NO, 1 for YES) | 
| air_conditioning | Optional | Relevant to define the amenities available at the properties you want to include in your search result. Inputs are optional and 0 and 1 values are expected (0 for NO, 1 for YES) | 
| kid_friendly | Optional | Relevant to define the amenities available at the properties you want to include in your search result. Inputs are optional and 0 and 1 values are expected (0 for NO, 1 for YES) | 
| pool | Optional | Relevant to define the amenities available at the properties you want to include in your search result. Inputs are optional and 0 and 1 values are expected (0 for NO, 1 for YES) | 
| parking | Optional | Relevant to define the amenities available at the properties you want to include in your search result. Inputs are optional and 0 and 1 values are expected (0 for NO, 1 for YES) | 
| hot_tub | Optional | Relevant to define the amenities available at the properties you want to include in your search result. Inputs are optional and 0 and 1 values are expected (0 for NO, 1 for YES) | 
| min_active_days | Optional | Relevant to define the minimum number of days the properties were available for rent, on the Short Term Rental market over the year, that you want to include in the search result. This is to ensure that you only include properties with a certain level of Short Term Rental activity in the estimation. Number values are expected. |



Example response:

```
{
  "num_listings": 54,
  "year_average_revenue": 19402.703703703704,
  "year_average_adr": 86.31481481481481,
  "year_average_occupancy": 0.7725925909148322,
  "monthly_metrics": [
    {
      "month": "january",
      "average_revenue": 951.2037037037037,
      "average_adr": 51.833333333333336,
      "average_occupancy": 0.4933333319646341
    },
    {
      "month": "february",
      "average_revenue": 1028.7407407407406,
      "average_adr": 67.48148148148148,
      "average_occupancy": 0.6414814816304931
    },
    {
      "month": "march",
      "average_revenue": 1549.4074074074074,
      "average_adr": 76.85185185185185,
      "average_occupancy": 0.7364814800244791
    },
    {
      "month": "april",
      "average_revenue": 1718.5,
      "average_adr": 85.18518518518519,
      "average_occupancy": 0.8083333315120803
    },
    {
      "month": "may",
      "average_revenue": 1844.8703703703704,
      "average_adr": 83.42592592592592,
      "average_occupancy": 0.8212962934264431
    },
    {
      "month": "june",
      "average_revenue": 1845.888888888889,
      "average_adr": 87.18518518518519,
      "average_occupancy": 0.8472222200146428
    },
    {
      "month": "july",
      "average_revenue": 1496.611111111111,
      "average_adr": 78.22222222222223,
      "average_occupancy": 0.6790740727274506
    },
    {
      "month": "august",
      "average_revenue": 1153.9259259259259,
      "average_adr": 60.074074074074076,
      "average_occupancy": 0.5805555542034132
    },
    {
      "month": "september",
      "average_revenue": 1829.4259259259259,
      "average_adr": 87.29629629629629,
      "average_occupancy": 0.8279629689123895
    },
    {
      "month": "october",
      "average_revenue": 2123.6666666666665,
      "average_adr": 82.57407407407408,
      "average_occupancy": 0.8938888907432556
    },
    {
      "month": "november",
      "average_revenue": 1837.1666666666667,
      "average_adr": 81.48148148148148,
      "average_occupancy": 0.8064814822541343
    },
    {
      "month": "december",
      "average_revenue": 2024.5740740740741,
      "average_adr": 92.81481481481481,
      "average_occupancy": 0.7692592602085184
    }
  ]
}
```

> Outputs:

- num listings: number of listings used in the estimation based (listing set) based on the applied inputs

- year average revenue: average yearly revenue (USD) across the listing set

- year average adr: average daily rate (USD) over the year across the listing set

- year avaerage occupancy: average yearly occupancy across the listing set

- month: month

- month average revenue: average monthly revenue (USD) across the listing set for specified month

- moth average adr: average daily rate (USD) across the listing set for specified month

- month average occupancy: average monthly occupancy across the listing set for specified month



# Endpoint 2: similar listings

Returns a list of similar properties with 2019 estimates for each property, including estimated average ADR, yearly revenue and occupancy.

```
https://listingroiapi.seetransparent.com/listings?latitude=40.410754&longitude=-3.700917&radius_meters=5000&type=ENTIRE_HOME&subtype=APARTMENT
```


| Params | Required | Description |
| ------ | ------ | ------ |
| API Key | `Required` | {{transparent_api_key}} |
| latitude | `Required`  | The latitude of the property or geographical area to be queried. Number values are expected. |
| longitude | `Required`  | The longitude of the property or geographic area to be queried. Number values are expected. |
| radius_meters | `Required`  | Refers to the radius around the coordinates you want to include in the search result. Minimum radius allowed is 500 meter, maximum radius allowed is 10000 meter. Number values are expected. |
| type | `Required`  | Relevant to define the type of properties to be included in the search result. Allowed values: ENTIRE_HOME, PRIVATE_ROOM, SHARED_ROOM |
| subtype | `Required`  | Relevant to define the subtype of properties to be included in the search result. Allowed values: APARTHOTEL, APARTMENT, BED & BREAKFAST, BOAT, BUNGALOW, CASTLE, CHALET, DORM, GLAMPING, GUEST_HOUSE, HOSTEL, HOTEL, HOUSE, OTHER, RV, TOWNHOUSE, VILLA |
| bedrooms | Optional | Relevant to define the size of properties to be incuded in the search result. Inputs are optional and multiple integer values are possible. |
| bathrooms | Optional | Relevant to define the size of properties to be incuded in the search result. Inputs are optional and multiple integer values are possible. | 
| capacity | Optional | Relevant to define the size of properties to be incuded in the search result. Inputs are optional and multiple integer values are possible. | 
| pool | Optional | Relevant to define the amenities available at the properties you want to include in your search result. Inputs are optional and 0 and 1 values are expected (0 for NO, 1 for YES) | 
| air_conditioning | Optional | Relevant to define the amenities available at the properties you want to include in your search result. Inputs are optional and 0 and 1 values are expected (0 for NO, 1 for YES) | 
| kid_friendly | Optional | Relevant to define the amenities available at the properties you want to include in your search result. Inputs are optional and 0 and 1 values are expected (0 for NO, 1 for YES) | 
| pool | Optional | Relevant to define the amenities available at the properties you want to include in your search result. Inputs are optional and 0 and 1 values are expected (0 for NO, 1 for YES) | 
| parking | Optional | Relevant to define the amenities available at the properties you want to include in your search result. Inputs are optional and 0 and 1 values are expected (0 for NO, 1 for YES) | 
| hot_tub | Optional | Relevant to define the amenities available at the properties you want to include in your search result. Inputs are optional and 0 and 1 values are expected (0 for NO, 1 for YES) | 
| min_active_days | Optional | Relevant to define the minimum number of days the properties were available for rent, on the Short Term Rental market over the year, that you want to include in the search result. This is to ensure that you only include properties with a certain level of Short Term Rental activity in the estimation. Number values are expected. |





Example response:

```

[
  {
    "url": "https://www.airbnb.com/rooms/18364233",
    "image": "https://a0.muscache.com/im/pictures/deabd657-3ef9-4808-b53e-5accd2ae6836.jpg?aki_policy=large",
    "active_days": 311,
    "year_total_revenue": 12776,
    "year_total_occupancy": 0.77
  },
  {
    "url": "https://www.airbnb.com/rooms/26728391",
    "image": "https://a0.muscache.com/im/pictures/ba3466e4-4298-42cd-8c6d-211bc72f5738.jpg?aki_policy=large",
    "active_days": 319,
    "year_total_revenue": 25698,
    "year_total_occupancy": 0.94
  }
]
```

> Outputs Enpoint 2

- url: listing URL 

- image: listing image URL

- active days: number of days the listing was active over the previous year.

- year total revenue: listing property revenue over the previous year (USD)

- year total occupancy: listing property occupancy over the previous year

> Limitations

The API does not return a result when there are no surrounding Airbnb listings fitting the input criteria.


# Test it

👉 Test the API with its swager page: https://listingroiapi.seetransparent.com/doc/static/index.html#/default/get_listings

# Free report generator

You can also use the API to power a free report generator that we have built for our clients:

[![N|Solid](https://seetransparent.com/blog/wp-content/uploads/2020/10/demo-report-1.gif)](http://bit.ly/vacation-rental-revenue-estimator)

To use this report, simply follow these steps:

>STEP 1
Copy this [sheet](/http://bit.ly/vacation-rental-revenue-estimator) to make it your own.

>STEP 2
Enter your private API Key to active the Transparent Estimator API (if you are a Smart Rental PRO user, this is free!).

>STEP 3
Fill the rest of the yellow cells.

>STEP 4
Hit the “Refresh” button or “Ctrl + R”.

>STEP 5
Check out the results in the Output page.

>STEP 6
Download the result as a pdf by pressing “File > Print” or “Ctrl + p” on the Output Sheet.



`⚠️ Do not share the sheet with your key outside of your company.`
