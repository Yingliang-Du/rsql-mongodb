[![Build Status](https://travis-ci.org/RutledgePaulV/rsql-mongodb.svg)](https://travis-ci.org/RutledgePaulV/rsql-mongodb)

## What

An open source implementation for converting [rsql](https://github.com/jirutka/rsql-parser) to mongo queries for spring
data. RSQL is a flexible and readable query language based off of apache's FIQL. Providing this adapater for mongo queries
makes RSQL a natural choice for APIs that want to provide flexible querying and whose underlying datastore is mongodb.


```
# basic equality
firstName==joe -> { "firstName" : "joe"}

# basic inequality
firstName!=joe -> { "firstName" : { "$ne" : "joe"}}

# basic greater than
createDate=gt=300 -> { "createDate" : { "$gt" : "300"}}

# basic greater than or equal
createDate=ge=300 -> { "createDate" : { "$gte" : "300"}}

# basic less than
createDate=lt=300 -> { "createDate" : { "$lt" : "300"}}

# basic less than or equal
createDate=le=300 -> { "createDate" : { "$lte" : "300"}}

# basic element appears in list
firstName=in=(billy,bob,joel) -> { "firstName" : { "$in" : [ "billy" , "bob" , "joel"]}}

# basic element does not appear in list
firstName=out=(billy,bob,joel) -> { "firstName" : { "$nin" : [ "billy" , "bob" , "joel"]}}

# anding of two basic conditions
firstName!=joe;lastName==dummy -> { "$and" : [ { "firstName" : { "$ne" : "joe"}} , { "lastName" : "dummy"}]}

# oring of two basic conditions
firstName!=joe,lastName==donovan -> { "$or" : [ { "firstName" : { "$ne" : "joe"}} , { "lastName" : "donovan"}]}

# anding of two oring conditions of anding conditions
((firstName==joe;lastName==donovan),(firstName==aaron;lastName==carter));((age==21;height==90),(age==30;height==100)) -> 

    {
       "$and":[
          {
             "$or":[
                {
                   "$and":[
                      {
                         "firstName":"joe"
                      },
                      {
                         "lastName":"donovan"
                      }
                   ]
                },
                {
                   "$and":[
                      {
                         "firstName":"aaron"
                      },
                      {
                         "lastName":"carter"
                      }
                   ]
                }
             ]
          },
          {
             "$or":[
                {
                   "$and":[
                      {
                         "age":"21"
                      },
                      {
                         "height":"90"
                      }
                   ]
                },
                {
                   "$and":[
                      {
                         "age":"30"
                      },
                      {
                         "height":"100"
                      }
                   ]
                }
             ]
          }
       ]
    }
    
```


## License
MIT