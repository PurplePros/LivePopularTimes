

# Live Popular Times

A library that extends the populartimes module to include support for **Live** *Google Maps* popular times data, which is currently inaccessible via Google's API.
## Getting Started

### Requirements
Google Maps API key https://developers.google.com/places/web-service/get-api-key 

### Installation: 

##### Options:
1. `python3 -m pip install --upgrade git+https://github.com/GrocerCheck/LivePopularTimes`
2. `clone` the repository, `cd` into the populartimes directory and run `pip install .`
3. **Note**: The library is not *yet* available via PyPI

## Usage  

- Please note that certain functions of this module use the Google Places Web API, which is billable to Google.
- Functions that accept api keys in their arguments will make API calls, and vice versa (self-explanatory)

## livepopulartimes.get_populartimes_by_address(formatted_address)

Retrieves information for a given address and adds populartimes, wait, time_spent and other data not accessible via Google Places by scraping and with API call, given a formatted address.
+ `livepopulartimes.get_populartimes_by_address(formatted_address)`
    + **formatted_address** 
        + str; address of location you are looking for, preferably in the following format:
            + "(*location name*) , *full address*, *city*, *province/state/etc*, *country*"
    + **proxy**
        + default = False
        + proxies ip in format 
                    `{
                    "http" : "http://10.10.1.10:2138",
                    "https" : "http://10.10.1.10:1080",
                    `}
                    
    :type formatted_address: string
    :type proxy: dict/json
    
    + **Example call**
        + `livepopulartimes.get_populartimes_by_address("(H-Mart Dunbar) 5557 Dunbar Street, Vancouver BC, Canada", proxy=proxy)`

+ **Response**
    + The information present for places can vary. Therefore *popularity*, *current_popularity*, *rating*, *rating_n*, *time_wait*, *time_spent* and *phone* are optional return parameters and only present if available.
    + *time_wait* and *time_spent* are in minutes
    + **Note**: The *time_wait* and *time_spent* parameters were only added recently to Google Maps and are only present as a language specific string. The extracted values may therefore be incorrect and you might have to parse the raw string yourself, depending on your language settings.
    + Returns dictionary of the following parameters:
        + `name`
        + `place_id`
        + `populartimes` *populartimes is "cleaned up" data, please refer to example output for details*
        + `current_popularity`
        + `popular_times` *popular_times is "raw" data, please refer to example output for details*
        + `address`
        + `location`
            + `lat`
            + `lng`
        + `categories`
        + `place_types`
    + **Refer to `example_output(get_populartimes_by_address).json)` for example output**
    

## livepopulartimes.get_populartimes_by_PlaceID(api_key, place_id)

Retrieves information for a given address and adds populartimes, wait, time_spent and other data not accessible via Google Places via Places API call & scraping, given a place_id.

+ `livepopulartimes.get_populartimes_by_PlaceID(api_key, place_id)`
    + **api_key**
        + str; your Google Places API key
    + **place_id**
        + str; Unique Google Places place identifier, can be obtained via `get_places_by_search` or Google Places javascript API
        + more details here: [https://developers.google.com/places/place-id]
    
    + **Example call**
        + `livepopulartimes.get_populartimes_by_PlaceID(API_KEY, "ChIJtW0qSJp0hlQRj22fXuPh7s4")`

+ **Response**
    + The information present for places can vary. Therefore *popularity*, *current_popularity*, *rating*, *rating_n*, *time_wait*, *time_spent* and *phone* are optional return parameters and only present if available.
    + *time_wait* and *time_spent* are in minutes
    + **Note**: The *time_wait* and *time_spent* parameters were only added recently to Google Maps and are only present as a language specific string. The extracted values may therefore be incorrect and you might have to parse the raw string yourself, depending on your language settings.
    + Returns dictionary of the following parameters:
        + `name`
        + `place_id`
        + `populartimes` *populartimes is "cleaned up" data, please refer to example output for details*
        + `current_popularity`
        + `popular_times` *popular_times is "raw" data, please refer to example output for details*
        + `address`
        + `location`
        + `hours`
            + `lat`
            + `lng`
        + `categories`
        + `place_types`
    + **Refer to `example_output(get_populartimes_by_PlaceID).json)` for example output**


## livepopulartimes.get_places_by_search(query)

Retrives Google Maps location data from search query

+ `livepopulartimes.get_populartimes_by_PlaceID(api_key, place_id)`
    + **query**
        + str; Google search query
    + **Example call**
        + `livepopulartimes.get_places_by_query("restaurants open in London")`

+ **Response**
    + The information present for places can vary
    + Returns dictionary with the following fields:
        + `name`
        + `place_id`
        + `address`
        + `location`
            + `lat`
            + `lng`
        + `categories`
        + `place_types`
    + **Refer to `example_output(get_places_by_search).txt)` for example output**


Special thanks to m-wrzr's populartimes module for the framework upon which this is built.
