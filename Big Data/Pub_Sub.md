# Pub/Sub

  - Asychronous messaging  - *many to many*
  - Decouples senders and receivers  = greater flexibility 
    - No need to think about how to connect senders with receivers
    - Acts as  middleware between the 2
  - Sources **publish** messages, and the other services **subscribe** to the published messages
  - Global, infinite capacity data ingestion
  - Similar to Apache Kafka
  - Serverless
  - No Ops


## What problem does it solve?

  - Ingest streaming data from anywhere in the world without worrying about capacity, regardless of how large the incoming ingest streaming data is
  - Thousands of IoT devices uploading data for example 


### Role in the data lifecycle?

  - Data ingest
  - Often paired with Dataflow for processing after ingest - Dataflow is often the subscriber for the puiblished data
