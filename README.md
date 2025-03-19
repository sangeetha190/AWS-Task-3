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
===================================================================================================
## Task 2 
### 📌 Step 1: Launch Two EC2 Instances
   - We need two servers (EC2 instances) that will run behind the Load Balancer.
  - Navigate to AWS EC2 Console..
  - Choose Amazon Linux 2 as the AMI.
  - Select t2.micro instance type.
  - Configure instance details and ensure both instances are in the same VPC.
  - Add User Data to install a web server:
  - ![image](https://github.com/user-attachments/assets/baeadc62-0a7b-4136-9bcb-31e919712810)
  - Repeat the process for the second instance, but modify the HTML content:
  - ![image](https://github.com/user-attachments/assets/7c8de6da-984a-4f29-ba5d-059d6fb2521e)
  - ![image](https://github.com/user-attachments/assets/d43bfa57-d545-4f4c-8853-ffec73e46460)
  - Configure Security Group:
  - Allow HTTP (Port 80) from Anywhere (0.0.0.0/0).
  - Allow SSH (Port 22) from Your IP.
  - Launch the Instances and note their Public IPs.

![image](https://github.com/user-attachments/assets/cead4134-abbc-425e-97cf-508d05768dfc)
![image](https://github.com/user-attachments/assets/baaa6488-d6f1-4773-837a-b745c6044bcb)
![image](https://github.com/user-attachments/assets/31bbfb75-4f8d-450a-ba75-f02444b1b5fc)
## 📌 Steps to Create web-server-2 (Same as web-server-1, with a small change)

![image](https://github.com/user-attachments/assets/64fd1d8d-01cb-4af9-a190-16525671fe7b)
![image](https://github.com/user-attachments/assets/46217138-e358-42b4-8a47-31a4c06fc5ff)
![image](https://github.com/user-attachments/assets/f2987931-7493-4440-8435-7cd8e7b297dd)


## After Lanuch the Both the Instances the Output is 
![image](https://github.com/user-attachments/assets/46617a2f-6a62-4a7f-b942-eb3341a97420)
![image](https://github.com/user-attachments/assets/4e621f41-8e53-4266-b571-936074f3a1aa)


### Create an Application Load Balancer (ALB)
  - Go to AWS Load Balancers Console.
  - Click Create Load Balancer → Select Application Load Balancer.
![image](https://github.com/user-attachments/assets/1244e716-1b07-446f-9701-dc90eb6b2d30)
  - Configure
      - Scheme: Internet-facing.
      - IP Address Type: IPv4.
      - Availability Zones: Select at least two subnets.

 - Configure Security Group
     - Allow HTTP (Port 80) from Anywhere.
 - Create a Target Group:
     - Choose Instance Type as target.
     - Port: 80.
     - Health Check Path: /index.html (change from / to avoid failure).
![image](https://github.com/user-attachments/assets/99eae7c2-70ff-4995-aa0c-8c834d32638a)

 - Register Targets (EC2 Instances):
     - Select both instances and register them.

![image](https://github.com/user-attachments/assets/6c0356bd-ccec-4d94-8cc6-c112836e7f2d)
##  Testing the Load Balancer
  - Wait for the ALB status to become Active.
  - Open the Load Balancer DNS Name in a browser.
  
      - [Scheme: Internet-facing.](http://web-alb-xxxxxx.ap-south-1.elb.amazonaws.com/)
      
 - Expected Output:
      - Welcome to Web Server 1
      - Welcome to Web Server 2
## (Load Balancer is distributing traffic between both servers)
![image](https://github.com/user-attachments/assets/59b29663-5b1e-42c3-8866-5a6d0e01798b)

![image](https://github.com/user-attachments/assets/de6e9a92-8c0e-4c31-a0f3-c43c5b730d52)


🎯 Final Confirmation
- ✅ Web Servers are running
- ✅ Load Balancer is distributing traffic
- ✅ DNS is accessible and responding correctly
