# Logging Amazon Connect API Calls with AWS CloudTrail<a name="logging-using-cloudtrail"></a>

Amazon Connect is integrated with AWS CloudTrail, a service that provides a record of the Amazon Connect API calls that a user, role, or AWS service makes\. CloudTrail captures Amazon Connect API calls as events\. For more information about CloudTrail, including how to configure and enable it, see the [AWS CloudTrail User Guide](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html)\.

Using the information that CloudTrail collects, you can identify a specific request to an Amazon Connect API, the IP address of the requester, the requester's identity, the date and time of the request, and so on\. If you configure a trail, you can enable continuous delivery of CloudTrail events to an Amazon S3 bucket\. If you don't configure a trail, you can view the most recent events in **Event History** in the CloudTrail console\. For more information, see [Creating a Trail For Your AWS Account](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-create-and-update-a-trail.html)\.

## Amazon Connect Information in CloudTrail<a name="connect-info-in-cloudtrail"></a>

CloudTrail is enabled on your AWS account when you create the account\. When supported event activity occurs in Amazon Connect, that activity is recorded in a CloudTrail event along with other AWS service events in **Event history**\. You can view, search, and download recent events in your AWS account\. For more information, see [Viewing Events with CloudTrail Event History](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events.html)\. 

For an ongoing record of events in your AWS account, including events for Amazon Connect, create a trail\. A *trail* enables CloudTrail to deliver log files to an Amazon S3 bucket\. By default, when you create a trail in the console, the trail applies to all AWS Regions\. The trail logs events from all AWS Regions and delivers the log files to the Amazon S3 bucket that you specify\. Additionally, you can configure other AWS services to further analyze and act upon the event data collected in CloudTrail logs\. For more information, see the following: 
+ [Creating a Trail For Your AWS Account](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-create-and-update-a-trail.html)
+ [CloudTrail Supported Services and Integrations](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-aws-service-specific-topics.html#cloudtrail-aws-service-specific-topics-integrations)
+ [Configuring Amazon SNS Notifications for CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/getting_notifications_top_level.html)
+ [Receiving CloudTrail Log Files from Multiple Regions](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html) and [Receiving CloudTrail Log Files from Multiple Accounts](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-receive-logs-from-multiple-accounts.html)

Amazon Connect supports logging both the request parameters and the responses for the following APIs as events in CloudTrail log files:
+ [CreateUser](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateUser.html)
+ [DeleteUser](https://docs.aws.amazon.com/connect/latest/APIReference/API_DeleteUser.html)
+ [StartOutboundVoiceContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartOutboundVoiceContact.html)
+ [StopContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StopContact.html)
+ [TagResource](https://docs.aws.amazon.com/connect/latest/APIReference/API_TagResource.html)
+ [UntagResource](https://docs.aws.amazon.com/connect/latest/APIReference/API_UntagResource.html)
+ [UpdateContactAttributes](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateContactAttributes.html)
+ [UpdateUserHierarchys](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateUserHierarchy.html)
+ [UpdateUserIdentityInfo](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateUserIdentityInfo.html)
+ [UpdateUserPhoneConfig](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateUserPhoneConfig.html)
+ [UpdateUserRoutingProfile](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateUserRoutingProfile.html)
+ [UpdateUserSecurityProfiles](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateUserSecurityProfiles.html)

For the following APIs, the request parameters are logged, but the responses are redacted:
+ [DescribeUser](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribeUser.html)
+ [DescribeUserHierarchyGroup](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribeUserHierarchyGroup.html)
+ [DescribeUserHierarchyStructure](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribeUserHierarchyStructure.html)
+ [GetContactAttributes](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetContactAttributes.html)
+ [GetCurrentMetricData](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html)
+ [GetFederationToken](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetFederationToken.html)
+ [GetMetricData](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetMetricData.html)
+ [ListContactFlows](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListContactFlows.html)
+ [ListHoursOfOperations](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListHoursOfOperations.html)
+ [ListPhoneNumbers](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListPhoneNumbers.html)
+ [ListQueues](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListQueues.html)
+ [ListRoutingProfiles](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListRoutingProfiles.html)
+ [ListSecurityProfiles](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListSecurityProfiles.html)
+ [ListTagsForResource](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListTagsForResource.html)
+ [ListUserHierarchyGroups](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListUserHierarchyGroups.html)
+ [ListUsers](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListUsers.html)

Every event or log entry contains information about who generated the request\. The identity information helps you determine the following: 
+ Whether the request was made with root or AWS Identity and Access Management \(IAM\) user credentials\.
+ Whether the request was made with temporary security credentials for a role or federated user\.
+ Whether the request was made by another AWS service\.

For more information, see the [CloudTrail userIdentity Element](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\.

## Example: Amazon Connect Log File Entries<a name="understanding-connect-entries"></a>

 A trail is a configuration that enables delivery of events as log files to an Amazon S3 bucket that you specify\. CloudTrail log files contain one or more log entries\. An event represents a single request from any source and includes information about the requested action, the date and time of the action, request parameters, and so on\. CloudTrail log files aren't an ordered stack trace of the public API calls, so they don't appear in any specific order\.

The following example shows a CloudTrail log entry that demonstrates the `GetContactAttributes` action\.

```
{
        "eventVersion": "1.05",
        "userIdentity": {
         "type": "AssumedRole",
         "principalId": "AAAAAAA1111111EXAMPLE",
         "arn": "arn:aws:sts::123456789012:assumed-role/John",
         "accountId": "123456789012",
         "accessKeyId": "AAAAAAA1111111EXAMPLE",
         "sessionContext": {
            "attributes": {
                "mfaAuthenticated": "false",
                "creationDate": "2019-08-15T06:40:14Z"
            },
            "sessionIssuer": {
                "type": "Role",
                "principalId": "AAAAAAA1111111EXAMPLE",
                "arn": "arn:aws:iam::123456789012:role/John",
                "accountId": "123456789012",
                "userName": "John"
            }
        }
    },
    "eventTime": "2019-08-15T06:40:55Z",
    "eventSource": "connect.amazonaws.com",
    "eventName": "GetContactAttributes",
    "awsRegion": "us-west-2",
    "sourceIPAddress": "205.251.233.179",
    "userAgent": "aws-sdk-java/1.11.590 Mac_OS_X/10.14.6 Java_HotSpot(TM)_64-Bit_Server_VM/25.202-b08 java/1.8.0_202 vendor/Oracle_Corporation",
    "requestParameters": {
        "InitialContactId": "00fbeee1-123e-111e-93e3-11111bfbfcc1",
        "InstanceId": "00fbeee1-123e-111e-93e3-11111bfbfcc1"
    },
    "responseElements": null,
    "requestID": "be1bee1d-1111-11e1-1eD1-0dc1111f1ac1c",
    "eventID": "00fbeee1-123e-111e-93e3-11111bfbfcc1",
    "readOnly": true,
    "eventType": "AwsApiCall",
    "recipientAccountId": "123456789012"
}
```