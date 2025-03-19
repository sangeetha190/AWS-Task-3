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
==================================================================================================================================
## Task 2 
📌 Step 1: Launch Two EC2 Instances
We need two servers (EC2 instances) that will run behind the Load Balancer.

#### Create EC2 Instance 1 (web-server-1)
       - Go to AWS Console → Search "EC2" → Click "Instances".
   !\[image\](https://github.com/user-attachments/assets/cead4134-abbc-425e-97cf-508d05768dfc)
       - Click "Launch Instance" → Give it a name "web-server-1".
       - Choose Amazon Machine Image (AMI):
            - Select Amazon Linux 2 (or Ubuntu if you prefer).
       - Choose Instance Type:
           - Select t2.micro (Free Tier eligible).
       - Key Pair:
           - Select an existing key pair or create a new one (Save the private key .pem file).
       - Network Settings:
           - Choose "Default VPC" or create a new VPC (default is fine).
           - Select "Public Subnet" (so we can access it).
           - Enable Auto-Assign Public IP.
       - Security Group:
          - Create a new security group:
          - Allow SSH (port 22) (for connecting to the instance).
          - Allow HTTP (port 80) (to allow web traffic).
       - Add User Data (This script will set up a web server automatically):
          - Click Advanced details → User Data → Paste this script:
                 - #!/bin/bash
                 - yum update -y
                 - yum install -y httpd
                 - echo "<h1>Welcome to Web Server 1</h1>" > /var/www/html/index.html
                 - systemctl start httpd
                 - systemctl enable httpd
                 - Click "Launch Instance".
         - ✅ Instance 1 (web-server-1) is now running! 🎉


create instance
![image](https://github.com/user-attachments/assets/cead4134-abbc-425e-97cf-508d05768dfc)

![image](https://github.com/user-attachments/assets/baaa6488-d6f1-4773-837a-b745c6044bcb)

![image](https://github.com/user-attachments/assets/31bbfb75-4f8d-450a-ba75-f02444b1b5fc)

## 📌 Steps to Create web-server-2 (Same as web-server-1, with a small change)
1️⃣ Go to AWS EC2 → Click "Launch Instance".
2️⃣ Instance Name: web-server-2.
3️⃣ AMI (OS): Choose Amazon Linux 2 (or Ubuntu if you prefer).
4️⃣ Instance Type: t2.micro (Free Tier eligible).
5️⃣ Key Pair: Use the same key pair as web-server-1.
6️⃣ Network Settings:

Select the same VPC as web-server-1.
Choose a different subnet (for high availability).
Enable Auto-Assign Public IP.
7️⃣ Security Group:
Use the same security group as web-server-1 (allow SSH & HTTP).
## 📌 User Data (Change the Message for web-server-2)
- Under "Advanced Details" → Paste this User Data script:
    - #!/bin/bash
    - yum update -y
    - yum install -y httpd
    - echo "<h1>Welcome to Web Server 2</h1>" > /var/www/html/index.html
    - systemctl start httpd
    - systemctl enable httpd

![image](https://github.com/user-attachments/assets/d5cbfe33-9cc3-4ac7-b9ae-eb7481d3e7a8)

![image](https://github.com/user-attachments/assets/87745904-dc37-40e3-b067-202ee381ef0a)

![image](https://github.com/user-attachments/assets/081a4de7-3a5f-44ec-a71f-d30b392c650f)

After Lanuch the Both the Instances the Output is 
![image](https://github.com/user-attachments/assets/46617a2f-6a62-4a7f-b942-eb3341a97420)

![image](https://github.com/user-attachments/assets/4e621f41-8e53-4266-b571-936074f3a1aa)

#### ✅ 1. Go to AWS Console → Create Load Balancer
- 1️⃣ Go to EC2 Dashboard → Click "Load Balancers" (on the left panel).
- 2️⃣ Click "Create Load Balancer".
![image](https://github.com/user-attachments/assets/ab044c6f-3721-41ab-a9cf-c5204c7d3b72)

- 3️⃣ Choose "Application Load Balancer".
- 4️⃣ Enter Load Balancer Name: web-alb.
- 5️⃣ Scheme: Select Internet-facing.
- 6️⃣ Listeners:
Select HTTP (Port 80).


Create the target Group and
![image](https://github.com/user-attachments/assets/045c4b44-d597-4256-82aa-027f039e9e80)
![image](https://github.com/user-attachments/assets/b276d2f1-d231-4474-84bc-c90389aee956)

![image](https://github.com/user-attachments/assets/67ff92c7-96f8-4f32-8692-9961f19b3353)

![image](https://github.com/user-attachments/assets/bd6f6bf2-6a2f-48a4-ae88-de2011aef744)



