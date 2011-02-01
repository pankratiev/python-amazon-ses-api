Python API for Amazon Simple Email Service
http://aws.amazon.com/ses/
===============

Description
===============
Here is an example of how to send an email using the API:
(Note that you should specify correct values of your AccessKeyID, SecretAccessKey and source/destionation email addresses)

from amazon_ses import AmazonSES, EmailMessage

AccessKeyID = '--YourAccessKeyID--'
SecretAccessKey = '--YourSecretAccessKey--'

amazonSes = AmazonSES(AccessKeyID, SecretAccessKey)

message = EmailMessage()
message.subject = 'Hello from Amazon SES! Test subject'
message.bodyText = 'This is body text of test message.'

result = amazonSes.sendEmail('username@yourdomaintest.com', 'testmail@yourdomaintest.com', message)    
print result.requestId
print result.messageId

I want you to notice that in case Amazon returns some error, the API will raise an exception AmazonError which will contain errorType, code and message. 

If your Amazon SES account is not switched to production use, you can send a message only from/to verified email addresses. Here is an example of how to verify the email using the API:

result = amazonSes.verifyEmailAddress('username@yourdomaintest.com')
print result.requestId

You will receive the confirmation with a link which you should click to verify your email. 

An example of how to receive information about SendQuota:

result = amazonSes.getSendQuota()
print result.requestId
print result.max24HourSend, result.maxSendRate, result.sentLast24Hours

===============
Currently the API supports the following Amazon SES actions:
SendEmail
VerifyEmailAddress
DeleteVerifiedEmailAddress
GetSendQuota
ListVerifiedEmailAddresses
Methods return instances of AmazonResult or derived class (for example, method amazonSes.getSendQuota() returns the instance of AmazonSendQuota). 

Author
===============
Vladimir Pankratiev
http://tagmask.com

