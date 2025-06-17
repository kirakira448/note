
## Data wrangling six steps
1. discovering
2. structuring
3. cleaning
4. enriching
5. validating
6. publishing

![[autonomous-driving-data-framework-on-aws_1.png]]

### 1. 
Near real-time ingestion of sensor data, data modeling, indexing, and enrichment through AWS IoT FleetWise and data stored in Amazon Simple Storage Service (Amazon S3).

通过 AWS IoT FleetWise 实现传感器数据的近实时摄取、数据建模、索引和丰富，数据存储在 Amazon Simple Storage Service (Amazon S3) 中。

### 2. 
Near real-time fleet monitoring and alerting with Amazon Redshift, Amazon Managed Grafana, and Amazon Simple Notification Service (Amazon SNS).

使用 Amazon Redshift、Amazon Managed Grafana 和 Amazon Simple Notification Service (Amazon SNS) 进行近实时车队监控和警报。
### 3. 
Bulk upload of recording data from copy stations through AWS Direct Connect, ingestion validation and registry with Amazon API Gateway, and a raw recording staging bucket with Amazon S3.

通过 AWS Direct Connect 从复制站批量上传记录数据，使用 Amazon API Gateway 进行摄取验证和注册，并使用 Amazon S3 作为原始记录暂存存储桶。
### 4. 
Initial data quality checks and data extraction with containers running on AWS Batch. Processed data is stored in Amazon S3.

使用在 AWS Batch 上运行的容器进行初始数据质量检查和数据提取。处理后的数据存储在 Amazon S3 中。
### 5. 
Images are annotated with machine learning models to detect objects and road lanes. Low confidence predictions are set aside for manual annotation. Bounding boxes are used for blurring faces and license plates. Amazon SageMaker Ground Truth is used for labeling.

使用机器学习模型对图像进行注释以检测物体和道路车道。置信度低的预测会被留出进行人工注释。使用边界框来模糊人脸和车牌。使用 Amazon SageMaker Ground Truth 进行标注。
### 6. 
Use Amazon EMR in combination with Amazon S3 and AWS Batch to enrich sensor data with localized weather and map matching info. It also combines image annotations, and sensor data to detect various scenes like traffic intersections or people and objects in the street.

结合使用 Amazon EMR、Amazon S3 和 AWS Batch 来丰富传感器数据，添加本地化天气和地图匹配信息。它还结合图像注释和传感器数据来检测各种场景，如交通路口或街道上的人和物体。
### 7. 
AWS analytics toolchain manages parquet datasets and schema evolution with Apache Iceberg, AWS Glue Data Catalog, querying tools such as Amazon Athena, Amazon Redshift, and OpenSearch.

AWS 分析工具链使用 Apache Iceberg、AWS Glue Data Catalog 管理 Parquet 数据集和架构演化，使用 Amazon Athena、Amazon Redshift 和 OpenSearch 等查询工具。
### 8. 
Data pipeline orchestration with Amazon Managed Workflows for Apache Airflow (Amazon MWAA) observability of distributed workloads with Amazon Managed Grafana, Amazon CloudWatch, and AWS X-Ray. Amazon Neptune is used for data lineage.

使用 Amazon Managed Workflows for Apache Airflow (Amazon MWAA) 进行数据管道编排，使用 Amazon Managed Grafana、Amazon CloudWatch 和 AWS X-Ray 观察分布式工作负载。使用 Amazon Neptune 进行数据血缘追踪。
### 9. 
Build, test, and deploy using GitOps on AWS CodePipeline and AWS CodeBuild.

使用 AWS CodePipeline 和 AWS CodeBuild 上的 GitOps 进行构建、测试和部署。
### 10. 
Host high-performance, on-demand visualization applications on Amazon Elastic Kubernetes Service (Amazon EKS) for engineers. Developer instances use Amazon Elastic Compute Cloud (Amazon EC2) and Amazon DCV to stage and share files with Amazon FSx for Lustre or Amazon S3. Use AWS Step Functions for instance orchestration.

在 Amazon Elastic Kubernetes Service (Amazon EKS) 上为工程师托管高性能、按需可视化应用程序。开发者实例使用 Amazon Elastic Compute Cloud (Amazon EC2) 和 Amazon DCV 来暂存和共享文件，使用 Amazon FSx for Lustre 或 Amazon S3。使用 AWS Step Functions 进行实例编排。
### 11. 
User-facing tools like Python and Spark Notebook infrastructure use Amazon EMR and SageMaker. Custom dashboards can be configured with Grafana, and web applications are built and hosted on AWS Amplify and Amazon CloudFront.

面向用户的工具，如 Python 和 Spark Notebook 基础设施使用 Amazon EMR 和 SageMaker。可以使用 Grafana 配置自定义仪表板，并在 AWS Amplify 和 Amazon CloudFront 上构建和托管 Web 应用程序。
### 12. 
Scalable simulation and KPI calculation modules use Amazon EKS or AWS Batch. Amazon QuickSight is used to analyze KPIs and simulation results.

可扩展的模拟和 KPI 计算模块使用 Amazon EKS 或 AWS Batch。使用 Amazon QuickSight 分析 KPI 和模拟结果。
### 13. 
Drive and file-level metadata can be stored and queried with Amazon DynamoDB at scale for pipeline traceability and to store metadata, manifests, markers, and tags.

可以使用 Amazon DynamoDB 大规模存储和查询驱动器和文件级元数据，以实现管道可追溯性并存储元数据、清单、标记和标签。
