## 🛠️ Step-by-Step Implementation: Automating Receipt Processing Using AWS

This guide walks you through the full setup of a serverless receipt processing pipeline using AWS services.

---

## 1️⃣ Create the S3 Bucket (for uploading receipts)

### ✅ Steps:
1. Go to the **S3 Console** → Click **Create Bucket**
2. Name your bucket (e.g., `storage-receipt-komalanand2004`)
3. Choose a region (e.g., `ap-south-1`)
4. Click **Create bucket**
5. Create Organizational folder inside bucket.
6. Name it **incoming** inside this you will upload files.
   
<img width="1894" height="814" alt="Screenshot 2025-07-15 214103" src="https://github.com/user-attachments/assets/d4b622ab-b251-4a16-854b-6013edb105cd" />

<img width="1909" height="916" alt="Screenshot 2025-07-15 215616" src="https://github.com/user-attachments/assets/ae63327a-fb6d-4000-b45b-bf30dd6573a6" />


## 2️⃣ Create a DynamoDB Table (to store extracted data)

### ✅ Steps:
1. Go to the **DynamoDB Console** → Click **Create Table**
2. Table name: `Receipts-table`
3. Partition key: `receipt_id` (String)
4. Sort-key: `date` (String)
5. Click **Create**

<img width="1258" height="543" alt="image" src="https://github.com/user-attachments/assets/0bc6620a-9c16-4de4-9ae9-a5a2fe2f367b" />

<img width="1919" height="912" alt="image" src="https://github.com/user-attachments/assets/8ea8deee-32a5-46b0-95da-c4bab39541a4" />


## 3️⃣ Set Up Amazon SES (to send emails)

### ✅ Steps:
1. Go to **Amazon SES Console**
2. Verify your sender email under **Verified Identities**
3. (Optional) Verify recipient email if your account is in sandbox mode
4. Note the region (e.g., `ap-south-1`) – you’ll need it in your Lambda

<img width="1919" height="872" alt="Screenshot 2025-07-15 225331" src="https://github.com/user-attachments/assets/f9ea7385-a000-483d-8a18-0f2e0abe231e" />

## 4️⃣ Create IAM Role for Lambda Execution

### ✅ Steps:
1. Go to the **IAM Console** → Roles → Create Role
2. Choose **Lambda** as the use case
3. Attach the following policies:
  
```
   - `AmazonS3ReadOnlyAccess`
   - `AmazonTextractFullAccess`
   - `AmazonDynamoDBFullAccess`
   - `AmazonSESFullAccess`
   - `AWSLambdaBasicExecutionRole`
```
4. Name the role: `LambdaReceiptProcessingRole`

<img width="1262" height="537" alt="image" src="https://github.com/user-attachments/assets/b7dccf9d-c7ed-4235-9ebe-3b98aec99a01" />

<img width="1255" height="523" alt="image" src="https://github.com/user-attachments/assets/b66e33d5-1ff6-4c00-b508-c34667462ae5" />


## 5️⃣ Create Lambda Function (processing engine)

### ✅ Steps:
1. Go to **AWS Lambda Console** → Click **Create Function**
2. Name: `ProcessReceiptFunction`
3. Runtime: **Python 3.9** or **Node.js**
4. Choose existing role → Select `LambdaReceiptProcessingRole`
5. Go to **configuration** tab inside **environment** varibales add this.
6. Go to the **Code** tab and add the pyhton code that I provide in **python.py** file and click **Deploy**.
7. Go to configuration tab > General configuration  > edit
8. Increase the timeout from 0.3 sec to 2 min for complex file.

<img width="1269" height="511" alt="image" src="https://github.com/user-attachments/assets/c2a23715-b8c0-49a1-9b14-27943ba27d70" />


<img width="1536" height="796" alt="Screenshot 2025-07-15 235403" src="https://github.com/user-attachments/assets/d3cab3f9-06f7-4b6d-9604-ee71f9b9087d" />


<img width="1536" height="796" alt="Screenshot 2025-07-15 235403" src="https://github.com/user-attachments/assets/1980c773-fe1e-466c-954b-f29e973c8ea9" />


<img width="1545" height="839" alt="Screenshot 2025-07-15 235602" src="https://github.com/user-attachments/assets/7d9a98af-a468-42a2-aee8-8664f3632ee3" />


<img width="1265" height="536" alt="image" src="https://github.com/user-attachments/assets/f413887b-5273-4cbb-abf4-d214553a64f4" />



## 6️⃣ Again go to S3 Bucket.
✅ Steps:
1. In the `Properties` Tab
2. Add the Event Notification 
3. Prefix : incoming/
4. Object creation : Select All object create events


<img width="1259" height="532" alt="image" src="https://github.com/user-attachments/assets/d0fc01b3-8de8-4c93-910c-6b18f02685b1" />



<img width="1893" height="853" alt="Screenshot 2025-07-16 000044" src="https://github.com/user-attachments/assets/1d9949b9-96d4-43ec-9e51-020461972037" />



<img width="1919" height="866" alt="Screenshot 2025-07-16 123553" src="https://github.com/user-attachments/assets/a9ae5a55-22f7-40b7-be62-a0c31eee42b8" />



<img width="1919" height="951" alt="Screenshot 2025-07-16 123614" src="https://github.com/user-attachments/assets/697992ed-e12f-40c2-97b3-308b3190d97c" />



<img width="1915" height="871" alt="Screenshot 2025-07-16 122917" src="https://github.com/user-attachments/assets/e3617bee-4075-4372-894c-6bae95df72c8" />



<img width="1919" height="913" alt="Screenshot 2025-07-16 123709" src="https://github.com/user-attachments/assets/87b68920-a3c1-42f9-931c-cb3843137a56" />








