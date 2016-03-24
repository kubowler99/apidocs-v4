## In-Network Pharmacies

The In-Network Pharmacy Endpoint returns in-network pharmacies for a plan and
identifies them as retail or mail order pharmacies.

| Endpoint               | HTTP Method | Description                                                              |
|:-----------------------|:------------|:-------------------------------------------------------------------------|
| /pharmacy/network/     | GET         | Get a list of pharmacies meeting certain search criteria                 |
| /pharmacy/network/{id} | GET         | Retrieve the data for a specified pharmacy; the ID is the provider’s NPI |

To use the In-Network Pharmacy Endpoint with a medicare member, use the Eligibility Endpoint
to submit an eligibility request for a member using medicare_national trading partner id. 
Medicare members with Part D coverage will have pharmacy.is_eligible set to true and the 
pharmacy.plan_number will contain the member’s Medicare Part D plan_number. This number can be 
used to access the member’s benefits.
 
A list of pharmacies will be returned for a given location and radius. The search can also be 
filtered with a pharmacy name. Ex. All in-network Walgreens for a given area.
 
The /pharmacy/network endpoint accepts the following parameters:
 
| Field       | Type     | Description                                                                                                                                 |
|:------------|:---------|:--------------------------------------------------------------------------------------------------------------------------------------------|
| trading_partner_id | {string} | Unique id for the intended trading partner, as specified by the [Trading Partners](https://platform.pokitdok.com/documentation/v4/#trading-partners) endpoint. |
| plan_number        | {string} | Member’s plan identification number. Note: If unknown can use X12 270/271 eligibility                                                |
| zipcode | {string} | Zip code for location      |
| radius        | {string} | Radius of area (miles)                                                                                                                    |
| pharmacy_name        | {string} | Name of pharmacy                                                                                                                   |
| state | {string} | Name of U.S. state in which to search for providers (e.g. “CA” or “SC”)                                                                           |
| sort | {string} | Accepted values include ‘distance’ (default) or 'rank’. 'distance’ sort requires city & state or zipcode parameters otherwise sort will be 'rank’. |

Example fetching pharmacy information by NPI:

```python
pd.pharmacy_network(npi=`1467560003`)
```

Example searching for in-network pharmacies by plan and zip code:

```python
pd.pharmacy_network(trading_partner_id=`medicare_national`, plan_number=`S5820003`, zipcode=`29307`, radius=`15mi`)
```

Example request for in-network pharmacies by plan, zipcode, and pharmacy name:

```python
pd.pharmacy_network(trading_partner_id=`medicare_national`, plan_number=`S5820003`, zipcode=`29307`, radius=`15mi`, pharmacy_name=`walgreens`)
```

The /pharmacy/network response contains the following parameters:

| Field                            | Type     | Description                            |
|:---------------------------------|:---------|:---------------------------------------|
| pharmacy.pharmacy_name           | {string} | Name of pharmacy                       |
| pharmacy.locations.address_lines | {array}  | Address lines                          |
| pharmacy.locations.city          | {string} | City                                   |
| pharmacy.locations.country       | {string} | Optional: Country                      |
| pharmacy.locations.geo_location  | {array}  | GeoJSON array of [longitude, latitude] |
| pharmacy.locations.phone         | {string} | Optional: Phone number                 |
| pharmacy.locations.state         | {string} | State                                  |
| pharmacy.locations.zipcode       | {string} | Zip code                               |  
| pharmacy.type                    | {string} | Mail or retail pharmacy                |