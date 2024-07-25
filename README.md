# Food Hygiene Ratings Analysis

## Table of Contents

1. [Introduction](#introduction)
2. [Part 1: Database and Jupyter Notebook Set Up](#part-1-database-and-jupyter-notebook-set-up)
3. [Part 2: Update the Database](#part-2-update-the-database)
4. [Part 3: Exploratory Analysis](#part-3-exploratory-analysis)
5. [Examples](#examples)
6. [Acknowledgements](#acknowledgements)


## Introduction

The UK Food Standards Agency evaluates various establishments across the United Kingdom and assigns them food hygiene ratings. This project involves analyzing the ratings data to assist journalists and food critics from Eat Safe, Love in selecting locations for future articles.

## Part 1: Database and Jupyter Notebook Set Up

Use `NoSQL_setup_starter.ipynb` for this section.

1. **Import the data:**
   - Import the data from `establishments.json` into MongoDB.
   - Database name: `uk_food`
   - Collection name: `establishments`

2. **Set up your notebook:**
   - Import necessary libraries: `PyMongo` and `Pretty Print (pprint)`.
   - Create an instance of the Mongo Client.
   - Verify database and data import:
     - List databases and confirm `uk_food` is listed.
     - List collections and ensure `establishments` is present.
     - Retrieve and display one document using `find_one` and `pprint`.

3. **Prepare for data manipulation:**
   - Assign the `establishments` collection to a variable.

## Part 2: Update the Database

Use `NoSQL_setup_starter.ipynb` for this section.

1. **Add a new establishment:**
   - Insert the following data for a new halal restaurant in Greenwich:
   ```json
   {
       "BusinessName":"Penang Flavours",
       "BusinessType":"Restaurant/Cafe/Canteen",
       "BusinessTypeID":"",
       "AddressLine1":"Penang Flavours",
       "AddressLine2":"146A Plumstead Rd",
       "AddressLine3":"London",
       "AddressLine4":"",
       "PostCode":"SE18 7DY",
       "Phone":"",
       "LocalAuthorityCode":"511",
       "LocalAuthorityName":"Greenwich",
       "LocalAuthorityWebSite":"http://www.royalgreenwich.gov.uk",
       "LocalAuthorityEmailAddress":"health@royalgreenwich.gov.uk",
       "scores":{
           "Hygiene":"",
           "Structural":"",
           "ConfidenceInManagement":""
       },
       "SchemeType":"FHRS",
       "geocode":{
           "longitude":"0.08384000",
           "latitude":"51.49014200"
       },
       "RightToReply":"",
       "Distance":4623.9723280747176,
       "NewRatingPending":True
   }
  2. **Update data:**

    Find the BusinessTypeID for "Restaurant/Cafe/Canteen" and return only the BusinessTypeID and BusinessType fields.
    Update the new restaurant with the BusinessTypeID you found.
    Remove establishments in Dover:
        Count and verify the number of documents for Dover Local Authority.
        Delete these documents and confirm the deletion.

Data type corrections:

    Convert latitude and longitude to decimal numbers.
    Convert RatingValue to integer numbers.

## Part 3: Exploratory Analysis

Use `NoSQL_analysis_starter.ipynb` for this section.

1. **Queries and analyses:**
   - **Hygiene score of 20:**
     - Count and display establishments with a hygiene score of 20.
   - **RatingValue ≥ 4 in London:**
     - Count and display establishments in London with a RatingValue ≥ 4.
   - **Top 5 establishments near Penang Flavours:**
     - Find top 5 establishments with RatingValue of 5, sorted by lowest hygiene score, near "Penang Flavours".
   - **Hygiene score of 0 by Local Authority:**
     - Count establishments with a hygiene score of 0 per Local Authority.
     - Sort and display top ten Local Authorities with the highest counts.

## Examples

## NoSQL Setup File
### 2. Find the BusinessTypeID for "Restaurant/Cafe/Canteen" and return only the `BusinessTypeID` and `BusinessType` fields.
python
```
business_type_id_query = {'BusinessType': 'Restaurant/Cafe/Canteen'}
business_type_fields_query = {'BusinessTypeID': 1, 'BusinessType': 1}

results = db.establishments.find(business_type_id_query, business_type_fields_query)

for result in results:
    pprint(result)
```
## NoSQL Analysis File
### 1. Which establishments have a hygiene score equal to 20?
python
```
# Find the establishments with a hygiene score of 20
query = {"scores.Hygiene": 20}

# Use count_documents to display the number of documents in the result
total_documents = establishments.count_documents(query)
pprint(total_documents)

# Display the first document in the results using pprint
pprint(establishments.find_one(query))
```

### Acknowledgements
- Study Group Members:
  - Gursimran Kaur - kaursimran081999@gmail.com - SimranBoparai
  - Evan Wall - ewall@escoffier.edu - Ewall24
