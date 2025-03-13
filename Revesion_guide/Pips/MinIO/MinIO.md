# **🔹 MinIO with Python (`minio` SDK)**

MinIO is a **high-performance object storage system** that is  **compatible with AWS S3** . It is widely used for  **storing large-scale unstructured data** , such as images, videos, logs, and backups.

✅ **Why Use MinIO?**

* Open-source & lightweight
* **Amazon S3-compatible API**
* High-speed **performance & scalability**
* Deployable on **local, cloud, or Kubernetes**

---

## **🔹 Installing MinIO & Python SDK**

```bash
pip install minio
```

---

## **1️⃣ Setting Up MinIO Server**

### **Start MinIO Locally (Docker)**

```bash
docker run -p 9000:9000 -p 9001:9001 -e "MINIO_ROOT_USER=admin" -e "MINIO_ROOT_PASSWORD=password" quay.io/minio/minio server /data --console-address ":9001"
```

**Access MinIO Web UI:**

* **URL:** `http://localhost:9001`
* **Username:** `admin`
* **Password:** `password`

---

## **2️⃣ Connecting to MinIO using Python**

```python
from minio import Minio

# Create MinIO client
minio_client = Minio(
    "localhost:9000",  # MinIO endpoint
    access_key="admin",
    secret_key="password",
    secure=False  # Use True for HTTPS
)

print("Connected to MinIO!")
```

✅ **Why `secure=False`?**

* If running locally  **without SSL** , set `False`

---

## **3️⃣ Creating a Bucket**

```python
bucket_name = "my-bucket"

# Check if bucket exists, then create
if not minio_client.bucket_exists(bucket_name):
    minio_client.make_bucket(bucket_name)
    print(f"Bucket '{bucket_name}' created!")
else:
    print(f"Bucket '{bucket_name}' already exists!")
```

✅ **Why Check `bucket_exists()`?**

* **Prevents errors** when trying to re-create a bucket

---

## **4️⃣ Uploading a File**

```python
file_path = "test.txt"
object_name = "documents/test.txt"

# Upload file to MinIO
minio_client.fput_object(bucket_name, object_name, file_path)

print(f"File '{file_path}' uploaded to '{bucket_name}/{object_name}'")
```

✅ **Why Use `fput_object()`?**

* **Uploads large files efficiently** using **streaming**

---

## **5️⃣ Downloading a File**

```python
download_path = "downloaded_test.txt"

# Download file from MinIO
minio_client.fget_object(bucket_name, object_name, download_path)

print(f"File downloaded to '{download_path}'")
```

✅ **Why Use `fget_object()`?**

* **Directly saves** the file to disk

---

## **6️⃣ Listing Objects in a Bucket**

```python
objects = minio_client.list_objects(bucket_name, recursive=True)

for obj in objects:
    print(f"Object: {obj.object_name} | Size: {obj.size} bytes")
```

✅ **Why Use `recursive=True`?**

* Lists all **files in subdirectories**

---

## **7️⃣ Deleting Objects**

### **(a) Delete a Single Object**

```python
minio_client.remove_object(bucket_name, object_name)
print(f"Deleted '{object_name}' from '{bucket_name}'")
```

### **(b) Delete Multiple Objects**

```python
objects_to_delete = [obj.object_name for obj in minio_client.list_objects(bucket_name, recursive=True)]
minio_client.remove_objects(bucket_name, objects_to_delete)
print("All objects deleted!")
```

✅ **Why Use `remove_objects()`?**

* Deletes  **multiple files in bulk** , improving performance

---

## **8️⃣ Generating a Presigned URL (For Temporary Access)**

```python
presigned_url = minio_client.presigned_get_object(bucket_name, object_name, expires=3600)
print(f"Presigned URL: {presigned_url}")
```

✅ **Why Use `presigned_get_object()`?**

* **Grants temporary access** to objects **without credentials**

---

## **🔹 Interview Questions on MinIO**

### **1️⃣ Basic Questions**

✔ What is MinIO? How is it different from AWS S3?

✔ How do you  **connect Python to MinIO** ?

✔ What is a  **bucket** , and why is it needed?

### **2️⃣ Advanced Questions**

✔ How do you **securely authenticate** with MinIO?

✔ What is the difference between  **`fput_object()` and `put_object()`** ?

✔ How do you **stream large files** into MinIO without memory issues?

✔ Explain the use of **presigned URLs** in MinIO.

✔ How does MinIO  **ensure high availability and replication** ?

---

## **🚀 Next Steps**

Would you like an **example with FastAPI + MinIO?** 🎯
