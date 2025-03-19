### S3 Bucket with CloudWatch Logging - Step-by-Step Guide
#### Task Breakdown & Completion Status:
- Step 1: Created an S3 bucket with no public access.
- Step 2: Uploaded files to the private S3 bucket.
- Step 3: Enabled CloudTrail to track S3 activities.
- Step 4: Configured CloudWatch Logs to store and view logs.
- Step 5: Verified file upload (PutObject) and delete (DeleteObject) logs in CloudWatch.

#### Step 1: Create an S3 Bucket (Private)
      - Log in to AWS Console → Navigate to S3.
      - Click "Create bucket".
      - Enter a Bucket Name (e.g., my-private-bucket).
      - Choose a Region (same as your AWS resources).
      - Block all public access →  Enable (this ensures the bucket remains private).
      - Object Ownership → Keep it ACLs disabled (recommended).
      - Click "Create bucket".
      -  Bucket is now created with no public access.
      
![image](https://github.com/user-attachments/assets/b82d35d9-e21a-4887-afa1-f07420859f62)

#### Step 2: Upload Files to S3
      - Open S3 → Click on your bucket (my-private-bucket).
      - Click "Upload" → "Add files".
      - Select a file from your system (e.g., an image or text file).
      - Click "Upload".
      - ✅ File is successfully uploaded to S3.
 
![image](https://github.com/user-attachments/assets/53afda2b-88b4-4a88-83b5-d15cac9be59e)
  
- Create bucket 

new 

new

upload the file
- ![image](https://github.com/user-attachments/assets/53afda2b-88b4-4a88-83b5-d15cac9be59e)

create the tail
- ![image](https://github.com/user-attachments/assets/e1bf5ed5-8b63-4bfc-a7f4-77a9b4d816c2)
next step 
- ![image](https://github.com/user-attachments/assets/b52c4fe8-b977-4f6c-985f-b8e544dcbf1a)
- review and proceed
![image](https://github.com/user-attachments/assets/9d0a3d8b-1ed3-4b0d-b748-a1b86ab775f4)


enable the "cloudWatch Log" 
![image](https://github.com/user-attachments/assets/676f60c2-ae52-429b-8853-366c42d4582c)
![image](https://github.com/user-attachments/assets/e878eda9-3ad2-40b0-9ef3-a3e47aed9e24)

deleted
![image](https://github.com/user-attachments/assets/b831bd14-33f7-4fc4-b4cd-e230f5d3f9d9)

=====================================================================================================

![image](https://github.com/user-attachments/assets/5fb8872c-cb4b-41dc-a8c6-2338d677b04f)

![image](https://github.com/user-attachments/assets/c0005a3c-24ce-46b3-82cd-a608f90e36f8)

- Block Public Access Settings
![image](https://github.com/user-attachments/assets/20eebe84-3c10-4cc5-92e1-2fd1680f17ce)
- Bucket Versioning
- Default Encryption
Final Step: Create the Bucket!
Once all settings are configured:
Click Create Bucket ✅
![image](https://github.com/user-attachments/assets/e8be0752-2feb-4bdf-a673-f9a212f43a3f)

## Step 1: Upload a File to your S3 Bucket
- 1 Go to the S3 Console.
- 2 Click on your bucket (my-private-bucket).
- 3 Click Upload.
- 4 Click Add files, then select a file from your computer.
- 5 Click Upload.
![image](https://github.com/user-attachments/assets/88fc31fa-098c-4213-ad10-f352506b63d0)
![image](https://github.com/user-attachments/assets/8644ca90-5655-4074-8f81-9affe25abe04)

## Step 2: Enable CloudTrail for S3 Logging
- Create a CloudTrail for S3 Events
 - Go to AWS CloudTrail Console.
 - Click Create trail.
 - Trail Name: s3-activity-trail
 - ![image](https://github.com/user-attachments/assets/b19b17a0-5f9c-4102-8699-3f23a47301c7)

