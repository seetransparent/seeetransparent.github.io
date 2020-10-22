# Rate Recommendation Methodolody


API Summary 

See three pagers: https://docs.google.com/presentation/d/1RFZ0nA1OlQlmxAow8BbasLj_3BmLy9055hadq_A8b_c/edit#slide=id.g957e639487_1_99
 
# Welcome

Welcome to the documentation for the Transparent Rate Recommendation API. 

Through this API, Transparent intends to provide data-based Revenue Management recommendations. 

We believe a broad span of players in the Short Term Rental industry could benefit from it and use cases are many. If you want to explore how to make the most out of this API, please reach out to us.

Having a clear and up-to-date API Documentation is one of the numerous ways we serve our clients. So if you have any questions or you spot a mistake, just send us a note.


# Key Principles

> Overview

Transparent Rate Recommendation API relies on Transparent Short Term Rental proprietary data. It benefits from a worldwide coverage or the four main Online Travel Agencies (OTA) and it goes back to 2017.

For any property listed on one of these OTAs, the API will provide a substiantated rate recommendation for the next 365 days. 

Having worked closely with Property Managers, we designed this API using a fairly common model. Every property has an intrinsic Base Price which remains stable over time. This Base Price is adjusted every day based on a combination of criteria deemed significant. 


It delivers the Base Price, and the next 365 daily adjustments with the final recommended rate. 

> Base Price

In order to determine the listing Base Price, we proceed as follows: 
- We identify the 500 nearest neighbors to the input listing
- We pull up the most impactful property characteristics - number of bedrooms, number of bathrooms, capacity, amenities etc.
- We retrieve historical reservations for these 500 properties
- We train a Machine Learning model on the neighbors to capture the different effects of every characteristic on the Base Price
- We use that model to estimate the Base Price for the input listing

The Base Price is static overtime, which is why you will always see only one base price in your API response.

> Day of the Week Variation

Working from the historical reservations of the 500 listings, we capture the typical price seasonality for every day of the week. 

> Week number Variation

Working from the historical reservations of the 500 listings, we capture the typical price seasonality for every week of the year. 

> Monthly Year on Year Variation

We pull up the future reservations of the 500 neighbors to capture the difference of every month's prices relative to the historical seasonality.

> Event Adjustment

As events can be a major driver in Short Term Rental Property rates, we developed a tailored model to detect those events and adjust the rates accordingly. 

Based on proprietary data, Transparent will be able to qualify certain events and not others. Everytime the event could be qualified, the event name will be specified.
An event adjustment will only be applied if it is shown to have a significant effect on normal seasonality. Should such an adjustment be recommended, it would match the market top performers’ rates.

> Booking Window Variation

In order to ensure that your property will not be booked too early, potentially leaving money on the table, we include in our rate recommendation an adjustment for the Booking Window. Closer nights will be discounted. And further out available nights will be marked up.

> Recommended Rate Calculation

Once these different adjustments are inferred, the final rate recommendation is calculated for the following 365 days. It follows the simple formula below:  

Recommended Rate(d) = Base Price x (1+Day of the Week Variation(d)+Week Number Variation(d)+Monthly Year on Year Variation(d)+Event Adjustment(d)+Booking Window Variation(d))

> Caveats and Limitations

`Limitation #1:` The API relies on the listing URL. It means our system needs to have captured it at least once so the API works. Therefore, the API may give null results for listings made public less than 3 weeks ago.
 
`Limitation #2:` The API does not run for listings that are in rural areas and do not have sufficient numbers of neighbors to use for the calculations.

`Caveat #1:` In case two listings of different platforms, but representing the same property, are queried, the Rate Recommendation API may return different results. This happens if the two listings are not perfectly identical across the platforms. This is usually the case when platforms randomize the listing coordinates within a certain radius. In addition to this, a difference in the number of decimals in the coordinates or in the number of bedrooms or bathrooms can also cause discrepancies. 

`Caveat #2:` On Booking.com, a property can have multiple room types. Currently, the API generates a recommendation based on the first room type on the property page. 


# Rate Recommendation Endpoint: Aggregate

Returns rate recommendations for the next 365 days for a given listing url. 

```
https://listingroiapi.seetransparent.com/aggregated?latitude=40.410754&longitude=-3.700917&radius_meters=5000&type=ENTIRE_HOME&subtype=APARTMENT
```


| Params |  |
| ------ | ------ |
| API Key | {{transparent_api_key}} |
| Listing URL | https://www.airbnb.com/rooms/45390946 |

Example response:

```
  {"data": {
    "query": {
      "url": "https://www.airbnb.com/rooms/45390946"
    },
    "prices": {
      "2020-09-14": {
        "base_price": 87,
        "day_of_week": "Saturday",
        "day_of_week_variation": 0.01,
        "week_number": 47,
        "week_number_variation": 0.02,
        "month_year": 12,
        "monthly_year_on_year_variation": 0.14,
        "event_name": "",
        "event_adjustment": 0,
        "booking_window_lower": 1,
        "booking_window_upper": 4,
        "booking_window_variation": 0.01,
        "recommended_price": 88
      }
    }
  }
}
```

# Test it

👉 Test the API with its swager page: https://yield-manager.pltp.us/api/docs/

# Free report generator

You can also use the API to power a free report generator that we have built for our clients:

[![N|Solid](https://i.imgur.com/a8PLsCh.gif)](https://docs.google.com/spreadsheets/d/15rfU5YRuS3qnSKX6VIqdlm53MQW8klVmcpGFLU-ba-8/edit?usp=sharing)

To use this report, simply copy [this](/https://docs.google.com/spreadsheets/d/15rfU5YRuS3qnSKX6VIqdlm53MQW8klVmcpGFLU-ba-8/edit?usp=sharing) free google sheet to make it your own, insert your API key, and the listing URL of your choice.

`⚠️ Do not share the sheet with your key outside of your company.`