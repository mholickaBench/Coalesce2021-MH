# Coalesce 2021 - Notes

# Monday - 6/12/2021 

## How to build a mature dbt project from scratch - Dave Matthews - dave@dbtlabs.com

### Items to investigate 
    -  Metadata API  

- a number of distince stages
- maturity :
    - feature completeness : does your project use features [ tests / documentation]
- Depth
    - are you effectively using DBT's features for you ?
    - medium : testing => mature : unified /standardized testing.


###  DBT maturity 
Repo :https://github.com/dbt-labs/dbt-project-maturity     
![DBT Maturity Table](2021-12-06-10-15-06.png)

* Jinja allows us to modularize our code
* The DAG becomes more complex, but is way more modularized.

#### L3 -  Childhood 

- scaleable as goal, using standards which makes sure you have quality as you scale. High tech debt if you don't.
- meta regarding the project [linting / PR template, etc. ]
- codification of the features.
- Every single project should get here
![Layers](2021-12-06-10-22-23.png)

#### L4 - Adolescence 

- newest additions - packages 
- not needed, and will depend on the specific data needs
- more dimensions, flexibility, context, and speed
- expand scope, model optimizations, and source metadata. Engage with the dbt community. This will increase dbts surface areas and influence in the org. You will lose stakeholder buy in if you don't

#### L5 - Adulthood 
- answer some of the big questions 
- improve the product itself, with more metadata, relationships with other stack tools. This will incrase observality and more control. 
- Hooks and macros become more complex. Introspective queries. Project starts to self-reflect.
- test / docuementation coverage. 
- **Metadata API ?????**
![L5-DAG](2021-12-06-10-29-21.png)


--- 

## Identity Crisis: Navigating the Modern Data Organization -  Panel

* **lots of fluff here, not really a great talk.. was expecting more**

* going from consuming data to building the platform to find the insights in the data. 
* Lots about coming into the career and being unsure about the opportunities. 
* Less about title, but moreso about the team and thier experiences, each with an area of focus. 
* lots of relationship building and cultural building when in a startup. 
* the title of analytics engineer coming in made it much easier to self-identify professionaly.

--- 
# Tuesday
---

## Tailoring dbt's incremental_strategy to Artsy's data needs - Abhiti Prabahar 

### Items to investigate 
    -  build time graph 

- Artsy : basically Etsy for art? [ scaled @ 1M visitors a week]
- Before : 
    * 16 hr build with Looker [ 100 users] 
    * 100% ownership of the pipeline
    * no testing.
- After
    * Graph migration 
    * CircleCI testing [end to end pipeline]
    * transparency with  alerting in slack 
- Transform step was taking 7 hrs [same with Extract]
    - micro-optimization of the transform step

* 50% of the build time comes from a model of `sessions`. 
* Sessions are super imprortant to this business. 
    - what is the converstation rate of email vs search ?
![Aggregated Session model](2021-12-07-09-53-11.png)
- This data can be super wide, important to keep an eye on this. 

![](2021-12-07-09-55-14.png)

- incrementalization
    - transforming data from 1 day, rather than the entire table.
    - entire sessions pipeline has been incrementalized
- **graph for build time ? - should research** 

- activities that can change in the future. All these activities needed to take place 180 days  in the past.

![Open Session concept](2021-12-07-10-04-33.png)


    - instead of rebilding the world, only rebuild those rows with the session_open
    - Instead of 17hrs => 5.5Hrs
        - Immutable : rebuild for the past day 
        - Mutablle : rebuild all rows that are open session or all data in the past 1 day .

![Now](2021-12-07-10-09-30.png)

--- 

## Smaller Black Boxes: Towards Modular Data Products - Stephen Bailey 

---

## Operationalizing Column-Name Contracts with dbtplyr - Emily Riederer 

    more detail : https://emilyriederer.netlify.app/post/convo-dbt/

- each step in the pipeline relies on human input [ with some amount of expectations for them . ]
- column names are contracts [ persists throughout the stack]
    - Interfaces ,configs, code = > dev:user, dev:dev,dev:machine 

![](2021-12-07-10-38-39.png)

- interfaces : universal symbols [ save button] / grouping [ arrow keys] / aesthetics [ submit in green / cancel in red ]

![](2021-12-07-10-43-23.png)

- changing the names on the variables might help to better understand the data [`LOGIN` vs `BIN_LOGIN` where `BIN` : `BINARY- NULL `]

![](2021-12-07-10-47-07.png)

- standardization allows for a shared understanding between data analysts and engineers
- `change once, update everywhere`

![](2021-12-07-10-51-33.png)

![](2021-12-07-10-55-51.png)


very neat concept. Operationalizing it will be difficult and time consuming. It has some nice items in it, but I am not sure about the time investment that would be needed. 

--- 

## Batch to Streaming in One Easy Step - Emily Hawkins & Arjun Narayan

    - https://materialize.com/introducing-dbt-materialize/
    - marketing pitch.  Quite good, but very challenging to implement, and needs a culture surrounding the streaming architecture.. Additionally, not very mature ( seems like a startup). Forces the upkeep of 2 DWH and 2 DBT projects. seems like a bit of pipedream 

- batch : reads data, calculates, then spits out results
- streaming : new data comes in and gets new results. 
- realtime data > not realtime data 

![Use cases](2021-12-07-11-37-20.png)

- streaming does not support SQL and that is why it is not used as much.


![](2021-12-07-11-47-33.png)

![24-hour ](2021-12-07-11-50-33.png)

- down to 30 mins instead of 24 hours on cart abandonment 

![cart abandonment - streaming](2021-12-07-11-52-05.png)

![Data Architecture](2021-12-07-11-54-59.png)

