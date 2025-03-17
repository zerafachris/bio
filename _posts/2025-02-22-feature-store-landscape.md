---
title: "The Current Landscape of Feature Stores"
tags:
  - Productionisation
  - Vector Store
  - MLOps
  - Feature Engineering
  - Platform
toc: true
---

<figure>
	<a href=""><img src="https://images.pexels.com/photos/30820142/pexels-photo-30820142/free-photo-of-abstract-futuristic-digital-tunnel-illusion.jpeg?auto=compress"></a>
</figure>

The current landscape of feature stores reflects a significant evolution in the field of data management and machine learning, driven by the increasing need for efficient data pipelines and model deployment. Feature stores serve as central repositories for storing, sharing, and managing features—data attributes used in machine learning models—facilitating collaboration among data scientists and engineers.

### Definition and Purpose of Feature Stores

Feature stores are designed to provide a systematic way to manage features across various machine learning projects. They enable teams to:

-   **Centralise Feature Management**: By storing features in a single location, feature stores reduce redundancy and promote reusability, allowing teams to leverage existing features rather than creating new ones from scratch.

-   **Ensure Consistency**: They help maintain consistency between training and production environments, ensuring that the same features are used during model training and inference.

-   **Facilitate Collaboration**: Feature stores enhance collaboration among data teams by providing a shared resource where features can be documented, discovered, and accessed by various stakeholders.

### Current Trends in Feature Stores

The landscape of feature stores is diverse, with options ranging from open-source to vendor-managed solutions, and in-house builds. Some notable trends include:

-   **Diverse Offerings**: Feature stores are available as managed platforms, on-premises solutions, and open-source projects.
-   **Varied Data Source Support**: Most feature stores support a range of data sources, including batch and streaming data.
-   **Feature Engineering Approaches**: Feature engineering can be done using SQL, Spark, Python, or Flink, depending on the feature store.

### Feature Store Providers

The feature store landscape includes a mix of vendor solutions, open-source projects, and in-house builds. Here is an overview of some of the providers, incorporating details from the Feature Store Summit 2024 and other sources:

| Provider            | Type                  | Notes                                                                                                                                                                                                                                                                                                                                                                |
| :------------------ | :-------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Hopsworks**        | Vendor/Open Source/On-Prem     | The first open-source Feature Store and the first with a DataFrame API. Most data sources (batch/streaming) supported. Ingest features using SQL, Spark, Python, Flink. The only feature store supporting stream processing for writes. Available as managed platform and on-premises.                                                        |
| **Vertex AI**         | Vendor                | A centralized repository for organizing, storing, and serving ML features on the GCP Vertex platform. Vertex AI Feature Store supports BigQuery, GCS as data sources. Separate ingestion jobs after feature engineering in BigQuery. Offline is BigQuery, Online BigTable.                                                                    |
| **SageMaker**         | Vendor                | Sagemaker Feature Store integrates with other AWS services like Redshift, S3 as data sources and Sagemaker serving. It has a feature registry UI in Sagemaker, and Python/SQL APIs. Online FS is Dynamo, offline parquet/S3.                                                                                                                           |
| **Databricks**        | Vendor                | A Feature Store built around Spark Dataframes. Supports Spark/SQL for feature engineering with a UI in Databricks. Online FS is AWS RDS/MYSQL/Aurora. Offline is Delta Lake.                                                                                                                                                                           |
| **Chronon**           | In-House              | One of the first feature stores from 2018, orginially called Zipline and part of the Bighead ML Platform. Feature engineering is using a DSL that includes point-in-time correct training set backfills, scheduled updates, feature visualizations and automatic data quality monitoring.                                                           |
| **Michelangelo**      | In-House              | The mother of feature stores. Michelangelo is an end-to-end ML platfom and Palette is the features store. Features are defined in a DSL that translates into Spark and Flink jobs. Online FS is Redis/Cassandra. Offline is Hive.                                                                                                                  |
| **FBLearner**         | In-House              | Internal end-to-end ML Facebook platform that includes a feature store. It provides innovative functionality, like automatic generation of UI experiences from pipeline definitions and automatic parallelization of Python code.                                                                                                                       |
| **Overton**           | In-House              | Internal end-to-end ML platform at Apple. It automates the life cycle of model construction, deployment, and monitoring by providing a set of novel high-level, declarative abstractions. It has been used in production to support multiple applications in both near-real-time applications and back-of-house processing.                         |
| **Featureform**       | Vendor/Open Source/On-Prem   | Virtual feature store platfrom - you plug in your offline and online data stores. It supports Flink, Snowflake, Airflow Kafka, and other frameworks.                                                                                                                                                                                             |
| **Twitter**           | In-House              | Twitter's first feature store was a set of shared feature libraries and metadata. Since then, they moved to building their own feature store, which they did by customizin feast for GCP.                                                                                                                                                          |
| **Feast**             | Open Source           | Originally developed as an open-source feature store by Go-JEK, Feast has been taken on by Tecton to be a minimal, configurable feature store. You can connect in different online/offline data stores and it can run on any platform. Feature engineering is done outside of Feast.                                                                   |
| **Tecton**            | Vendor                | Managed feature store that uses PySpark or SQL (Databricks or EMR) or Snowflake to compute features and DynamoDB to serve online features. It provides a Python-based DSL for orchestration and feature transformations that are computed as a PySpark job. Available on AWS.                                                                       |
| **Jukebox**           | In-House              | Spotify built their own ML platform that leverages TensorFlow Extended (TFX) and Kubeflow. They focus on designing and analyzing their ML experiments instead of building and maintaining their own infrastructure, resulting in faster time from prototyping to production.                                                                       |
| **Intuit**            | In-House              | Intuit have built a feature store as part of their data science platform. It was developed for AWS and uses S3 and Dynamo as its offline/online feature serving layers.                                                                                                                                                                                 |
| **Iguazio**           | Vendor/Open Source/On-Prem   | Centralized and versioned feature storre built around their MLRun open-source MLOps orchestration framework for ML model management. Uses V3IO as it offline and online feature stores.                                                                                                                                                         |
| **Abacus.ai**         | Vendor                | The platform allows to build real-time machine and deep learning features, upload ipython notebooks, monitor model drift, and set up CI/CD for machine learning systems.                                                                                                                                                                           |
| **Doordash**          | In-House              | A ML Platform with an effective online prediction ecosystem. It serves traffic on a large number of ML Models, including ensemble models, through their Sibyl Prediction Service.They extended Redis with sharding and compression to work as their online feature store.                                                                      |
| **Salesforce**        | In-House              | ML Lake is a shared service that provides the right data, optimizes the right access patterns, and alleviates the machine learning application developer from having to manage data pipelines, storage, security and compliance. Built on an early version of Feast based around Spark.                                                              |
| **H2O Feature Store** | Vendor/On-Prem        | H2O.ai and AT&T co-created the H2O AI Feature Store to store, update, and share the features data scientists, developers, and engineers need to build AI models.                                                                                                                                                                                   |
| **Feathr**            | Open Source           | Feathr automatically computes your feature values and joins them to your training data, using point-in-time-correct semantics to avoid data leakage, and supports materializing and deploying your features for use online in production.                                                                                                        |
| **Nexus**             | In-House              | Nexus supports batch, near real-time, and real-time feature computation and has global scale for serving online and offline features from Redis and Delta Lake-s3, respectively.                                                                                                                                                                   |
| **Qwak**              | Vendor                | Qwak's feature store is a component of the Qwak ML platform, providing transformations, a feature registry and both an online and offline store.                                                                                                                                                                                                 |
| **Beast**             | In-House              | Robinhood built their own event-based real-time feature store based on Kafka and Flink.                                                                                                                                                                                                                                                            |
| **Feature Byte**      | Vendor                | FeatureByte is a solution that aims to simplify the process of preparing and managing data for AI models, making it easier for organizations to scale their AI efforts.                                                                                                                                                                               |
| **Fennel**            | Vendor                | Fennel is a fully managed realtime feature platform from an-Facebook team. Powered by Rust, it is built ground up to be easy to use. It works natively with Python/Pandas, has beautiful APIs, installs in your cloud in minutes, and has best-in-class support for data/feature quality.                                                         |
| **OpenMLDB**          | Open Source           | Open-source feature computing platform that offers unified SQL APIs and a shared execution plan generator for both offline and online engines, eliminating the need for cumbersome transformation and consistency verification.                                                                                                                  |
| **Chalk**             | Vendor                | Chalk is a platform for building real-time ML applications that includes a real-time feature store.                                                                                                                                                                                                                                                |

**Note:** This table is not exhaustive but represents a selection of feature store providers.

### Challenges Facing Feature Stores

Despite their advantages, feature stores face several challenges:

-   **Data Quality Management**: Ensuring high-quality features is essential for effective machine learning. Poor data quality can lead to inaccurate models, necessitating robust validation and monitoring processes.

-   **Scalability**: As organisations scale their machine learning efforts, feature stores must be able to handle large volumes of data and support numerous concurrent users without performance degradation.

-   **Governance and Compliance**: With increasing regulations around data privacy and security, feature stores must implement governance frameworks to manage access controls and ensure compliance with relevant laws.

### Conclusion

Feature stores are becoming an indispensable component of modern machine learning infrastructure. They streamline the process of feature management, enhance collaboration among teams, and improve the overall efficiency of machine learning workflows. As the field continues to evolve, addressing challenges related to data quality, scalability, and governance will be crucial for organisations looking to leverage the full potential of their data assets.
