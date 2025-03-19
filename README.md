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
      - Enter a Bucket Name (sangeethacloud-my-private-bucket).
      - Choose a Region (same as your AWS resources).
      - Block all public access →  Enable (this ensures the bucket remains private).
      - Object Ownership → Keep it ACLs disabled (recommended).
      - Click "Create bucket".
      -  Bucket is now created with no public access.
      
![image](https://github.com/user-attachments/assets/b82d35d9-e21a-4887-afa1-f07420859f62)

#### Step 2: Upload Files to S3
      - Open S3 → Click on your bucket (sangeethacloud-my-private-bucket).
      - Click "Upload" → "Add files".
      - Select a file from your system (e.g., an image or text file).
      - Click "Upload".
      - ✅ File is successfully uploaded to S3.
 
![image](https://github.com/user-attachments/assets/53afda2b-88b4-4a88-83b5-d15cac9be59e)

#### Step 3: Enable CloudTrail to Log S3 File Activities
To track uploads, downloads, and deletions, we need to enable CloudTrail.

      - Go to AWS CloudTrail → Click "Create trail".
      - Enter Trail Name: s3-logging-trail.
      - Storage Location:
           - Select "Use existing S3 bucket" and choose sangeethacloud-my-private-bucket 
           - This will store CloudTrail logs inside your bucket.
- create the tail
- ![image](https://github.com/user-attachments/assets/e1bf5ed5-8b63-4bfc-a7f4-77a9b4d816c2)
- ![image](https://github.com/user-attachments/assets/ae62537f-7a55-4250-b49f-a0611990ad47)

      - Enable Logging for S3:
           - Scroll to Data events → Select S3.
           - Choose "Specify bucket" and select sangeethacloud-my-private-bucket.
           - Enable "Read & Write" (to log uploads & deletions).
       -  Click "Next", review the settings, and click "Create Trail".
       - ✅ CloudTrail is now tracking S3 file activities.

next step 
  ![image](https://github.com/user-attachments/assets/ee59b5e9-4ac4-4314-8c6a-bf1358e2d710)
- review and proceed
  !![image](https://github.com/user-attachments/assets/4f9e3320-2010-422a-8565-17af339dab8a)


#### Step 4: Enable CloudWatch Logs for Easy Viewing
        - Open AWS CloudTrail → Click on your trail (s3-logging-trail).
        - Click "Edit" → Scroll to CloudWatch Logs.
        - Enable CloudWatch Logs → Choose "Create new Log Group" (e.g., S3-Log-Group).
        - Click "Save Changes".
        - ✅ Now, S3 logs will be visible in CloudWatch Logs.

![image](https://github.com/user-attachments/assets/676f60c2-ae52-429b-8853-366c42d4582c)
![image](https://github.com/user-attachments/assets/e878eda9-3ad2-40b0-9ef3-a3e47aed9e24)


### Step 5: View Logs in CloudWatch
      - Go to AWS CloudWatch → Click "Log Groups".
      - Open the Log Group (S3-Log-Group).
      - Click on the latest Log Stream.
      - Search for event types:
          - "PutObject" → When a file is uploaded
          - "DeleteObject" → When a file is deleted
          - "GetObject" → When a file is downloaded
      - ✅ Now, you can track all file activities in CloudWatch.

![image](https://github.com/user-attachments/assets/b831bd14-33f7-4fc4-b4cd-e230f5d3f9d9)

### Task 1 is Done.
