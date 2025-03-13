### **Google Cloud Storage (`google-cloud-storage`) Guide**

The `google-cloud-storage` Python library is used to interact with  **Google Cloud Storage (GCS)** , enabling file uploads, downloads, and management of cloud storage buckets.

---

## **1️⃣ Install `google-cloud-storage`**

```bash
pip install google-cloud-storage
```

✅  **Dependencies** : Requires  **Python 3.7+** .

---

## **2️⃣ Set Up Authentication**

You need a  **Google Cloud Service Account Key** .

1. Go to [Google Cloud Console](https://console.cloud.google.com/).
2. Navigate to  **IAM & Admin → Service Accounts** .
3. Create a service account and download the  **JSON key file** .

Then, set the environment variable:

```bash
export GOOGLE_APPLICATION_CREDENTIALS="path/to/service-account.json"
```

✅ **Use Case:** Required for authenticated access to GCS.

---

## **3️⃣ Upload a File to GCS**

```python
from google.cloud import storage

def upload_to_gcs(bucket_name, source_file, destination_blob):
    client = storage.Client()
    bucket = client.bucket(bucket_name)
    blob = bucket.blob(destination_blob)

    blob.upload_from_filename(source_file)
    print(f"File {source_file} uploaded to {destination_blob}.")

upload_to_gcs("your-bucket-name", "local_file.txt", "uploaded_file.txt")
```

✅ **Use Case:** Uploads a file to a  **GCS bucket** .

---

## **4️⃣ Download a File from GCS**

```python
def download_from_gcs(bucket_name, blob_name, destination_file):
    client = storage.Client()
    bucket = client.bucket(bucket_name)
    blob = bucket.blob(blob_name)

    blob.download_to_filename(destination_file)
    print(f"File {blob_name} downloaded to {destination_file}.")

download_from_gcs("your-bucket-name", "uploaded_file.txt", "downloaded.txt")
```

✅ **Use Case:** Downloads a file from  **GCS to local storage** .

---

## **5️⃣ List Files in a Bucket**

```python
def list_files(bucket_name):
    client = storage.Client()
    bucket = client.bucket(bucket_name)

    blobs = bucket.list_blobs()
    for blob in blobs:
        print(blob.name)

list_files("your-bucket-name")
```

✅ **Use Case:** Lists all files in a  **GCS bucket** .

---

## **6️⃣ Delete a File from GCS**

```python
def delete_from_gcs(bucket_name, blob_name):
    client = storage.Client()
    bucket = client.bucket(bucket_name)
    blob = bucket.blob(blob_name)

    blob.delete()
    print(f"Deleted {blob_name} from {bucket_name}.")

delete_from_gcs("your-bucket-name", "uploaded_file.txt")
```

✅ **Use Case:** Deletes a file from  **GCS** .

---

## **7️⃣ Generate a Signed URL (Temporary Access)**

```python
from datetime import timedelta

def generate_signed_url(bucket_name, blob_name, expiration_minutes=60):
    client = storage.Client()
    bucket = client.bucket(bucket_name)
    blob = bucket.blob(blob_name)

    url = blob.generate_signed_url(expiration=timedelta(minutes=expiration_minutes))
    print(f"Signed URL: {url}")

generate_signed_url("your-bucket-name", "uploaded_file.txt", 60)
```

✅ **Use Case:** Grants **temporary access** to a file.

---

## **8️⃣ Interview Questions on `google-cloud-storage`**

### **1️⃣ Basic Questions**

✔ What is  **Google Cloud Storage (GCS)** ?

✔ How do you authenticate to GCS in Python?

✔ How do you upload/download a file using `google-cloud-storage`?

### **2️⃣ Advanced Questions**

✔ What is a  **signed URL** , and how do you use it?

✔ How can you improve performance when working with **large files** in GCS?

✔ What is the difference between  **Coldline, Nearline, and Standard storage classes** ?

✔ How do you **stream data to/from GCS** without saving it locally?

---

## **🚀 Next Steps**

Would you like an **end-to-end GCS integration** with FastAPI or Flask? 🎯
