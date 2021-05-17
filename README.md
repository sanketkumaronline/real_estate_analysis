# Real Estate Analysis
We are going to be using data from the 2020 -2021 Toronto Real Estate sold house listings.  We want to answer questions whether the sold listings could predict future house prices based on the house's features (number of washrooms, bedrooms, etc), location.  


## Data:
The data are pdf files which show 26 rows.
* "#" 
* LSC - The listing displays its contract status at the Last Status Change (LSC) field
* EC - Describes whether the property has received the Encumbrance Certificate: certificate of assurance that the property is free from any legal or monetary liability
* St# - The Street number
* Street name - The name of the street.
* Abbr - Abbreviation of Street type.
* Dir - Direction (North, South, East and West).
* Municipality - The name of the city in which the property resides in.
* Community - The name of the locality on which the property resides within a given municipality.
* List Price - The price of the property at the time of listing.
* Sold Price - The price that the property was sold for.
* Type - Describes the type of the property (semi-detached, detached or attached).
* Style - Number of storeys 
* Br - The number of bedrooms 
* "+" - Any other additional rooms
* Wr - The number of washrooms 
* Fam - Indicates if there is a family room in the listed property.
* Kit - Number of kitchens in the listed property.
* Garage type - The type of the garage.
* A/C - The type of A/C (Centralized or non-centralized).
* Heat - The type of Furnace.
* Contract Date - The date the contract was signed.
* Sold Date - The date the property was sold on.
* List Brokerage - Name of brokerage that the listed property was under.
* Co op Brokerage - Buyer's brokerage.
* MLS # - A unique number assigned to a real estate listing.

The pdf files are converted into Excel files, cleaned up then saved as csv.  
Multiple Linear Regression model will be used to predict the future price of the house based on the house features listed above.
We will are using SQLite for the Database.  

