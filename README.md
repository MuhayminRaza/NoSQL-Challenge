# NoSQL-Challenge

Challenge Background: 
The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating. You've been contracted by the editors of a food magazine, Eat Safe, Love, to evaluate some of the ratings data in order to help their journalists and food critics decide where to focus future articles.

This challenge required us to:
Part 1: Database and Jupyter Notebook Set Up
Part 2: Update the Database
Part 3: Exploratory Analysis

The following questions needed to be answered as part of the Exploratory Analysis: 
Question 1: Which establishments have a hygiene score equal to 20?
Question 2: Which establishments in London have a RatingValue greater than or equal to 4?
Question 3: What are the top 5 establishments with a RatingValue of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?
Question 4: How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to lowest, and print out the top ten local authority areas. 

The following code was written with the help of a TA in office hours and ASKBCS: 

query_3 = {'RatingValue' : '5', 'geocode.latitude' : 
    {'$gte' : latitude - degree_search, '$lte' : latitude + degree_search},
    'geocode.longitude': {'$gte' : longitude - degree_search, '$lte' : longitude + degree_search}}
sort = [('scores.Hygiene', 1)]
RV_top5 = list(establishments.find(query_3).sort(sort).limit(5))

match = {'$match' : {'scores.Hygiene' : 0}}
group = {'$group': {'_id': "$LocalAuthorityName", 'count': { '$sum': 1 }}}
sort = {'$sort': { 'count': -1 }}

business_type_id = {"BusinessType": "Restaurant/Cafe/Canteen"}
business_type_fields = {"BusinessTypeID", "BusinessType"}
business_type = establishments.find_one(business_type_id, business_type_fields)
pprint(business_type)

establishments.update_many({}, [{'$set': {'geocode.longitude': {'$toDouble': '$geocode.longitude'}, 
                                         'geocode.latitude': {'$toDouble': '$geocode.latitude'}}}])
