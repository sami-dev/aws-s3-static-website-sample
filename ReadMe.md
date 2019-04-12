# Static Website Hosting on Amazon S3

Amazon Simple Storage Service (Amazon S3) can be used to host static Websites without a need for a Web server. S3 buckets can be used to host the HTML files for entire static websites.

You can start by creating an Amazon S3 bucket, enabling the Amazon S3 Website hosting feature, and configuring access permissions for the bucket. After you have uploaded files and setup Website, Amazon S3 takes care of serving your content to your visitors.

You also need to configure Amazon Route 53, a managed Domain Name System (DNS) service to point your domain to your Amazon S3 bucket.

## Advantages of Hosting Website on S3

Here are some of the advantages of hosting site on S3

### Performance

The website will be highly performant and scalable at a fraction of the cost of a traditional Web server.

### Scalability and Availability

Amazon S3 is inherently scalable. For popular websites, the Amazon S3 architecture will scale seamlessly to serve thousands of HTTP requests per second without any changes to the architecture.

In addition, by hosting with Amazon S3, the website is inherently highly available.
 

## Deployment Instructions

Below are the steps to setup static Website on Amazon S3. Open AWS Management console. Select S3 under Storage.

### Create an S3 Bucket

When you first create an S3 bucket, you select the AWS Region in which the files will be geographically stored.

Click on "Create Bucket" button.

Provide a globally unique name for bucket and select Region. 

Leave blank this field "Copy Settings from an existing bucket".

<br/>
<img src="Documentation/Images/Step1-CreateBucket.PNG" alt="Create Bucket"/>

### Upload Content of Website

Upload the website contents to your S3 bucket including sub-folders.

<br/>
<img src="Documentation/Images/Step2-UploadContents.PNG" alt="Upload Contents"/>


### Add a Bucket Policy to Allow Public Reads

Go to Permissions Tab --> Update Public Access Setting:

Uncheck Manage public bucket policies:

a. Uncheck - Block new public bucket policies (Recommended)

b. Uncheck - Block public and cross-account access if bucket has public policies (Recommended) 

<br/>
<img src="Documentation/Images/Step3-BucketPolicy-A.PNG" alt="Create Bucket Policy"/>

Add following bucket policy. Replace [YOUR_BUCKET_NAME] with name of your bucket policy.

```
{ 
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow", 
            "Principal": "*", 
            "Action": "s3:GetObject", 
            "Resource": "arn:aws:s3:::[YOUR_BUCKET_NAME]/*" 
        } 
    ] 
}
```

Click 'Save' button to save changes.

<br/>
<img src="Documentation/Images/Step3-BucketPolicy-B.PNG" alt="Create Bucket Policy"/>

### Enable Website Hosting
In order to serve assets via url, you need to enable Website Hosting

Go to Properties and enable "Static Website Hosting" option

Note the endpoint.
For Example:
http://{bucket-name}.s3-website-us-east-1.amazonaws.com

<br/>
<img src="Documentation/Images/Step4-A.PNG" alt="Enable Website Hosting"/>

<br/>
<img src="Documentation/Images/Step4-B.PNG" alt="Enable Website Hosting"/>

### Validation

Access the site in browser:
http://{bucket-name}.s3-website-us-east-1.amazonaws.com

For Example:
<a href="http://pwdgen.s3-website-us-east-1.amazonaws.com/">http://pwdgen.s3-website-us-east-1.amazonaws.com/</a>

<br/>
<img src="Documentation/Images/SampleWebsite.PNG" alt="Sample Static Website"/>