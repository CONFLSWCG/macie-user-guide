# Concepts and Terminology<a name="macie-concepts"></a>

As you get started with Amazon Macie, you can benefit from learning about its key concepts\. 

**Account**  
A standard AWS account that contains your AWS resources\. When you sign up for Amazon Web Services \(AWS\), your AWS account is automatically signed up for all services in AWS, including Macie\. The account that you use to sign in to AWS at the time when you first enable Macie is designated as the **master** account\.  
You can also integrate other accounts with Macie\. These other accounts are called **member** accounts\.   
No users from the member accounts are granted access to the Macie console\. Only the master account users have access to the Macie console where they can configure Macie and monitor and protect the resources in both master and member accounts\. 

**Alert**  
A notification about a potential security issue that is discovered by Macie\. Alerts are displayed on the Macie console and provide a comprehensive narrative about all activity that occurred over the last 24 hours\.  
Macie provides the following types of alerts:  

+ *Basic alerts* \- alerts that are generated by the security checks that Macie performs\. There are two types of basic alerts in Macie:

  + Managed \(Macie\-curated\) basic alerts which you cannot modify\. You can only enable or disable the existing managed basic alerts\. 

  + Custom basic alerts which you can create and modify to your exact specifications\.

+ *Predictive alerts* \- automatic alerts based on activity within your AWS infrastructure that deviates from the established normal activity baseline\. More specifically, Macie continuously monitors IAM user and role activity within your AWS infrastructure and builds a model of the normal behavior\. It then looks for deviations from that normal baseline and when such activity is detected, it generates automatic predictive alerts\. For example a user uploading or downloading a large number of S3 objects in a single day might trigger an alert if that user typically downloads one or two S3 objects over the course of a week\. 
For more information about alerts, including alert categories and details about the contents of Macie alerts, see [Amazon Macie Alerts](macie-alerts.md)\. 

**Data source**  
The origin or location of a set of data\. To classify and protect your data, Macie analyzes and processes information from the following data sources:     
**AWS CloudTrail event logs, Including Amazon S3 Object\-Level API Activity**  
AWS CloudTrail provides you with a history of AWS API calls for your account, including API calls made using the AWS Management Console, the AWS SDKs, the command line tools, and higher\-level AWS services\. AWS CloudTrail also allows you to identify which users and accounts called AWS APIs for services that support CloudTrail, the source IP address that the calls were made from, and when the calls occurred\. For more information, see [What is AWS CloudTrail?](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html)  
For data classification purposes, Macie utilizes CloudTrail's ability to capture object\-level API activity on S3 objects \(data events\)\. For more information, see [Logging Data and Management Events for Trails](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/logging-management-and-data-events-with-cloudtrail.html#logging-data-events)\.   
**Amazon S3**  
In this release, Macie analyzes and processes data stored in the Amazon S3 buckets\. You can select the S3 buckets that contain objects that you want Macie to classify and monitor\.  
Amazon Simple Storage Service \(Amazon S3\) is storage for the Internet\. Amazon S3 stores data as objects within buckets\. An object consists of a file and optionally any metadata that describes that file\. To store an object in Amazon S3, you upload the file you want to store to a bucket\. Buckets are the containers for objects\. For more information, see [Getting Started with Amazon Simple Storage Service](http://docs.aws.amazon.com/AmazonS3/latest/gsg/GetStartedWithS3.html)\.

**User**  
In the context of Macie a user is the AWS Identity and Access Management \(IAM\) identity that makes the request\. Macie uses the CloudTrail `userIdentity` element to distinguish the following user types\. For more information, see [CloudTrail userIdentity Element](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\.   

+ Root – The request was made with your AWS account credentials\.

+ IAM user – The request was made with the credentials of an IAM user\. 

+ Assumed role – The request was made with temporary security credentials that were obtained with a role via a call to the AWS Security Token Service \(AWS STS\) AssumeRole API\. 

+ Federated user – The request was made with temporary security credentials that were obtained via a call to the AWS STS GetFederationToken API\.

+ AWS account – The request was made by another AWS account\. 

+ AWS service – The request was made by an AWS account that belongs to an AWS service\. 
When specifying a user in the Macie console, for example searching for a user in the **Users** tab or constructing a query in the **Research** tab, or whitelisting a user in a basic alert with the index of **Cloudtrail data**, you must use a special Macie format called **macieUniqueId**\. The macieUniqueId is a combination of the IAM UserIdentity element and the recipientAccountId\. For more information, see the list of UserIdentity elements above and the definition of recipientAccountId in the [CloudTrail Record Contents](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-record-contents.html)\. The examples below list various structures of macieUniqueId, depending on the user identity type:  

+ 123456789012:root

+ 123456789012:user/Bob

+ 123456789012:assumed\-role/Accounting\-Role/Mary
For more detailed examples, see [Users in Macie](macie-users.md)\.