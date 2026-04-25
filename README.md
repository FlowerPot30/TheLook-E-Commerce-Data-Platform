# 🛒TheLook E-Commerce-Data-Platform
A end-to-end Data Engineering Project built on Databricks and AWS S3, demonstrating a production-style Lakehouse architecture using the TheLook eCommerce public dataset. 

---

## 📐 Data Architecture
![Data Architecture](docs/data_architecture)
- **Incremental ingestion** via Databricks Auto Loader, picks up new files automatically without reprocessing old data
- **Delta Lake** for ACID transactions and time travel all layers
- **Star Schema** on Gold layer optimized for analytical queries
- **Delta Live Tables** for pipeline orchestration with built-in quality expectations

---

## 📂 Dataset ##
**Original Source**: [TheLook E-Commerce](https://www.kaggle.com/datasets/mustafakeser4/looker-ecommerce-bigquery-dataset), but we would like to show Streaming Ingestion method, so we split the datas by year. You can get the splited dataset from datasets folder.

A fictional eCommerce clothing store developed by the Google Looker team, containing 7 tables:
| Table | Type | Split Strategy |
|---|---|---|
| `orders` | Fact | By year |
| `order_items` | Fact | By year |
| `inventory_items` | Fact | By year |
| `events` | Fact | By year |
| `users` | Dimension | By year |
| `products` | Dimension | Single file |
| `distribution_centers` | Dimension | Single file |

Files are split by year to simulate **Incremental data arrival** - mimicking how data lands in a real production environment.

---

## 🛠️ Tech Stack
| Layer | Tool |
| --- | --- | 
| Cloud Storage | AWS S3 |
| Compute & Platform | Databricks (Free Edition) |
| Ingestion | Databricks Auto Loader |
| Storage Format | Delta Lake | 
| Transformation | PySpark, Spark SQL |
| Pipeline | Delta Live Tables |
| Data Modeling | Star Schema |
| Visualization | Power BI |
| Data Quality | Delta Live Tables Expectations |

---

## 📂 Project Structure
```bash
thelook-data-platform/
├── notebooks/
│   ├── 01_bronze_ingestion.py
│   ├── 02_silver_transformation.py
│   ├── 03_gold_modeling.py
│   └── 04_data_quality.py
├── docs/
│   └── data_architecture.png
├── datasets/
│   ├── events
│   ├── products
│   ├── inventory_items
│   ├── orders
│   ├── distribution_centers
│   ├── order_items
│   └── users
└── README.md
```

---

## 🔐 AWS IAM Policy
**S3DataAccess**
- s3:PutObject
- s3:GetObject
- s3:GetObjectVersion
- s3:DeleteObject
- s3:DeleteObjectVersion
- s3:AbortMultipartUpload
- s3:ListBucketMultipartUploads
  
**S3BucketLevel**
- s3:ListBucket
- s3:GetBucketLocation
  
---

## 🚀 Getting Started
### Prerequisites
- Databricks Free Edition Account
- AWS account with S3 bucket

### Steps
1. Upload datasets to S3 under raw/ folder
2. Create IAM Role and attach policy above
3. Create Credential in Databricks
4. Create External Location in Databricks
5. Run notebooks in order
   - 01_bronze_ingestion
   - 02_silver_transformation
   - 03_gold_modeling
   - 04_data_quality

**Note**: Using AvailableNow trigger instead of Continuous due to Databricks Free Edition limitation.
   

     
