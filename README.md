# Case-Study-Data-Architec---Kiwibot

# **Entity Relationship Diagram of Kiwi’s main operation database**

![ERD - Kiwi's main operation .svg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3228fae0-d4c8-493d-8ee5-8b69a4e6f98a/ERD_-_Kiwis_main_operation_.svg)

This diagram shows some of the entities present in Kiwibot's business and how they are related through its database.

the entities you will find are:

- Countries
- Cities
- Neighborhoods
- Capus of operation
- Branch offices
- Businesses
- Application users
- Clients
- Location georeference
- integrated service with Pg_routing
- Kiwibots
- Tests on the road
- maintenance verification
- Product
- Ordering
- Agreements
- Type of agreements
- Suppliers
- Supplies and materials
- Employees
- Departments
- Projects
- News reports

For the elaboration of the diagram the LucidChart tool was used.


# Data implementation 👩🏽‍💻

How would you deploy this architecture in Kiwibot?

Considering the good reputation that Kiwibot uses environmentally friendly technologies, the implementation will be through Google Cloud Platform (GCP), as it is nowadays google and its cloud services, made an open, reliable, collaborative, accessible, very secure, and the cleanest platform.

The infrastructure proposal will be:
Considering the entity-relationship diagram elaborated, this **SQL database** relational database will allow consistency, data isolation, and being related the consistency will give a clearer structure. This will be hosted in a cloud instance, **GCP** provides a service called Cloud SQL, we will use Postgresql for data persistence also has excellent support for use cases like search geospatial data, and we could give it a BigData approach using **Serverless** from GCP like BigQuery, serverless give speed and as we are a startup, startups compete on speed.
*CloudSQL + BigQuery*.

## 1. Create an instance of database

we create an instance of our database in Cloud SQL, we choose the Postgresql database.

![1](https://github.com/Giraluna1/Case-Study-Data-Architec---Kiwibot/blob/main/statics/1.png)

and lest's connect to that instance from our local machine.

it will ask for an instance name, password, select a data center that is near to operations for better performance, give the version that you need to create, and click on CREATE

![2](https://github.com/Giraluna1/Case-Study-Data-Architec---Kiwibot/blob/main/statics/2.png)

well the instance is being loaded we can see more the basic details of the instance, CPU, RAM, Storage and we can also see the IP address wich we can use to connect to this instance from our machine

![3](https://github.com/Giraluna1/Case-Study-Data-Architec---Kiwibot/blob/main/statics/3.png)

## 2. Connect to DataBase.

Now our instance is up and running in order to connect to our DB we need a database management tool for Postgres it is pg admin. Open PG admin
Create a new server.

![4](https://github.com/Giraluna1/Case-Study-Data-Architec---Kiwibot/blob/main/statics/4.png)

give a name for this connection

![5](https://github.com/Giraluna1/Case-Study-Data-Architec---Kiwibot/blob/main/statics/5.png)

put in the Host address the IP address for our DB instance, the username is Postgres and the default port is 5432.

![6](https://github.com/Giraluna1/Case-Study-Data-Architec---Kiwibot/blob/main/statics/6.png)

the password is the password of our instance

## 3. Make model migrations

Once we have the connection ready, we do the migration of our ERD model made with the Lucidchart tool, we can export it to our DBMS. Before using the generated commands we may need to add data types, indices or foreign keys and then copy the subsequent commands to your clipboard

![7](https://github.com/Giraluna1/Case-Study-Data-Architec---Kiwibot/blob/main/statics/7.png)

and now we can load the records to the database, through the backend of our software, or from the data previously processed and transformed.

## 4. Load records to database

Starting with basically three main steps which are Extraction, Transformation, and Load (ETL) of the respective data, this process is possible with a very useful tool of our GCP package known as Dataflow. This interface will process the data, it is fully managed and will speed up the development in streaming and batch use cases, also the management and simplified operations and have a basis for future training in ML models.

The proposed diagram needs to create a database extension with [Pg routing](https://docs.pgrouting.org/latest/es/index.html#), this allows to extend the geospatial database from Postgis/Postgresql to provide geospatial routing and network analysis functions.

## 5. Approach Big Data

Considering that the IoT technology of our Kiwibots collects unstructured data, which are more and more, we can make an intermediate NoSQL database for our IoT system, this allows us to have flexibility, to have higher speed, to have a latency writing, it will work to improve scalability. Databases such as **[InfluxDB](https://www.influxdata.com/)** empower developers to build IoT, analytics, and monitoring software. It is purpose-built to handle the massive volumes and countless sources of time-stamped data produced by sensors, applications, and infrastructure.

It can be easily integrated with GCP services or even the GCP itself [Firestore](https://firebase.google.com/docs/firestore/) allows offline data management, in case the robot is not connected to the internet.

### **Implementation with BigQuery:**

Big Query is a fully managed and serverless (without any infrastructure) enterprise data warehouse.

1. We can enter our Data Lake, our data that are in various formats, which may be stored in some storage by means of a federated reading schema.
    - We can use different transformation processing services to connect to the data source and insert it into BigQuery.
    - Preprocessing of this unstructured information, transforming and structuring it to store it in BigQuery.

# Business undesrtanding & Business Evaluation 🤖

What do you think are the business-related questions that would help us build a better data awareness for our company's business?

How would you visualize each of those business questions to materialize them into tangible actions? What tools would you use?

## How can we take advantage of the data in our company to make timely decisions??

To achieve a shared dashboard, to act in terms of data, that the whole company is aligned in front of the data in real-time, it is important to act smarter and this is possible thanks to the data cloud, GCP is for me one of the best tools for that.

## What are the critical points of the IoT?

### How fast does my IoT store data?

if a critical point is speed, we can think about what kind of database I have for my IoT, maybe a NoSQL will help me to have a faster collection, and be more flexible.

### How is the communication of my IoT system?

if my critical point is in the communication between different devices of my IoT system, maybe it is important to review the type of connection protocol of the IoT.

## My georeference logs are growing exponentially, how do I make sure it doesn't take too much time to respond?

For this it is advisable to use a tool like [Elasticsearch](https://www.elastic.co/es/what-is/elasticsearch), it allows to make complex searches in almost real-time.

## How to keep the team or the end customer informed of what is happening during a delivery?

We could use tools like [Apache Kafka](https://kafka.apache.org/), for that transmission of the state by means of a message or [Spark Streaming](https://spark.apache.org/docs/latest/streaming-programming-guide.html).

## How can I know at what time I am going out of my established metric budget?

In case a delay budget has been defined for the course of the delivery, we can create an alert every week in case our bot has not met the budgeted time. This is in order to maintain reliability in times. And this could be done with a tool like [Splunk](https://www.splunk.com/) or [Graphite](https://graphiteapp.org/).

# Authors
<div align='center'>
  <div>
    <table>
      <tr>
        <td valign="top" align='center'>
            <a href="https://github.com/Giraluna1" target="_blank">
            <p>Giraluna Gomez</p>
            <img alt="github_page" src="https://avatars.githubusercontent.com/u/70671381?v=4" height="80" width="80" />
            </a>
            <br />
            <a href="https://www.linkedin.com/in/giralunagomez/" target="_blank" rel="noopener noreferrer">
            <img src="https://img.icons8.com/plasticine/100/000000/linkedin.png" width="35" />
            </a>
            <a href="https://twitter.com/luna_gom" target="_blank" rel="noopener noreferrer">
            <img src="https://img.icons8.com/plasticine/100/000000/twitter.png" width="35" />
            </a>
        </td>