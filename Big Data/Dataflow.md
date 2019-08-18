 # Dataflow
 
 Similar to Dataproc except it is not part of the hadoop ecosystem.
 
  - Batch and streaming data processing
  - Change and transform data from one format into another
  - Can process both streaming and batch data in the same pipeline
  - Built on Apache Beam

## Streaming/Batch data

Streaming data and batch data is different types of data. The differences are how it is ingested, what type of format and what frequency that data is collected.

  - Stream = continuous stream, asychronous
    - Small bits
    - Many sources
    - Continuous flow
    - Examples: Sensor data, user events, IoT devices
    - **Pub/Sub** is the primary method of ingesting that massive, continuous streaming data

  - Batch = large amounts of stored data
    - Transferred in bulk
    - Large *chunks* of data
    - Few sources
    - Once in a while
    - **Cloud Storage** - Transfering large amounts of data from Cloud Storage into some other service


## What problem does this solve?

  - Need to transform data before storing/using in another source
  - Unique in the sense that you can have multiple streaming and batch data sources processing together in the same pipeline



### Role in the data lifecycle?

  - Data processing


## Dataflow vs Dataproc (Apache Beam vs Apache hadoop)

  - Lot of overlap
    - Both same role of processing data or transforming it to become more useful
  - Google's recommendation - use Dataproc if you are tied to Hadoop ecosystem or want to go morie *hands on* with a devops approach otherwise use dataflow
  - For a serverless approach, use Dataflow


