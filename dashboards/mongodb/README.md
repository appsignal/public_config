# MongoDB magic dashboard

[MongoDB](https://www.mongodb.com/) is a NoSQL, web-scale database that allows easy storage and retrieval of arbitrarily-structured documents.

When using [the MongoDB integration in the AppSignal for Ruby gem](https://docs.appsignal.com/ruby/integrations/mongodb.html), the MongoDB magic dashboard will appear. This README uses the existing MongoDB documentation as reference.

The following graphs are displayed in this magic dashboard:

- [Throughput](#throughput)
- [Query duration](#query-duration)

## Throughput

The "Throughput" graph shows the amount of queries executed on each MongoDB database.

This graph displays values from the `mongodb_query_duration` metric. This graph will show a line for each combination of values of the following metric tags:

- The **database** that the query was executed on. 

## Query duration

The "Query duration" graph shows the 95th percentile and average duration of the queries executed on each MongoDB database.

This graph displays values from the `mongodb_query_duration` metric. This graph will show a line for each combination of values of the following metric tags:

- The **database** that the query was executed on. 
