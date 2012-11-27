mailVU.com API 
Version 1.4






Revision History

Version
Date
Modified By
Change
0.1
August 5, 2010
Addy Kapur
Initial draft
0.2
Oct 11, 2010
Addy Kapur
Updated
0.3
Nov 24, 2010
Addy Kapur
Added Example
0.4
Feb 2, 2011
Addy Kapur
Thumbnail
0.5
Feb 6, 2011
Addy Kapur
Additional Parms
0.6
May 7, 2011
Addy Kapur
Additional Parms
0.7
June 14, 2011
Addy Kapur
User Management
0.8
June 28, 2011
Addy Kapur
EMail Parms
1.0
July 7, 2011
Addy Kapur
Updated API
1.1
Oct 12, 2011
Addy Kapur
Added Template
1.2
Feb 12, 2012
Addy Kapur
Msg History & D/l
1.3
May 25, 2012
Addy Kapur
Added Contacts
1.4
Jun 22, 2012
Addy Kapur
Upload Item

TABLE OF CONTENT
Revision History  1
Version	1
Date	1
Modified By	1
Change	1
Environment	5
URL	5
Parameter name	5
Type	5
Description	5
Value	7
Parameter name	8
Type	8
Description	8
Value	10
Parameter name	11
Type	11
Description	11
Value	11
Environment	12
URL	12
Parameter name	13
Type	13
Description	13
Parameter name	14
Type	14
Description	14
Parameter name	15
Type	15
Description	15
Parameter name	16
Type	16
Description	16
Parameter name	17
Type	17
Description	17
Parameter name	18
Description	18
Parameter name	19
Type	19
Description	19
Parameter name	20
Description	20
Environment	22
URL	22
Parameter name	22
Type	22
Description	22
Value	23
Parameter name	24
Type	24
Description	24
Value	24
Appendix A: Generating a timestamp	26
Appendix B:Social media icon URLS (or use your own)	26
Icon	26
URL	26

1.  Introduction

1.1.  Prerequisites

When requesting the API key, please provide us the following
1. Domain name where the widget will be hosted/called from.
2. Text for the title bar and the button of the widget.
3. Number of minutes of recording you would like up to 10 minutes.
4. Callback URL. If you want to get notification of each recording, you will have to provide us with a callback URL
2.  User Management

2.1.  User Management API Endpoints

Environment
URL
Test
http://apitest.mailvu.com/api/v1/manage
Production
http://api.mailvu.com/api/v1/manage

2.2.  Add User
			
To Add/Remove Users you should call the above URL using HTTP protocol and pass the following parameters as POST or GET variables

Parameter name
Type
Description
api-key
Req
ID of the partner. Given during setup by mailVU.

action
Req
ADD_USER: to add a user to the system
user-id
Req
A unique ID (Unique for your account) that identifies a user
timestamp
Req
Unix Timestamp is number of seconds since January 1, 1970, 00:00:00 GMT. See Appendix A on how to generate this timestamp. If the timestamp is more than 30 mins old, this message will be rejected. 
hash
Req
hexdigest(MD5(action+api-key+user-id+timestamp+partner-secret-key))
This is used to validate that the api request is coming from a valid partner and URL is not being reused/changed.
The partner-secret-key is assigned to the partner at the time of setup. It is never sent in plaintext.

name
opt
Name of the user
email
opt
Email address of the user
plan
opt
Plan used by the user. This will be required if your users get different limits per your contract with mailvu.
Please contact support@mailvu.com to agree on the possible values for this field.
security-level
opt
If your plan requires dashboard access instead of just widget, add this parameter to indicate proper security level
Leave it empty for for Widgets only
Possible Values:-
BASE_USER
USER
ADMINISTRATOR
signature
Opt
Signature text in HTML that will appear in the footer of the email and the landing page.
icon1_image_url
Opt
URL for social media icon. See appendix B for defaults
icon1_item_url
Opt
URL for users social media account
icon2_image_url
Opt
URL for social media icon. See appendix B for defaults
icon2_item_url
Opt
URL for users social media account
icon3_image_url
Opt
URL for social media icon. See appendix B for defaults
icon3_item_url
Opt
URL for users social media account
icon4_image_url
Opt
URL for social media icon. See appendix B for defaults
icon4_item_url
Opt
URL for users social media account
icon5_image_url
Opt
URL for social media icon. See appendix B for defaults
icon5_item_url
Opt
URL for users social media account
icon6_image_url
Opt
URL for social media icon. See appendix B for defaults
icon6_item_url
Opt
URL for users social media account
template-code
Opt
specific to your account. Default mailvu-business
template-logo-url
Opt
URL for the user’s logo.
template-color1
Opt
user defined field. Used to define color in the template
template-color2
Opt
user defined field. Used to define color in the template
template-color3
Opt
user defined field. Used to define color in the template
template-color4
Opt
user defined field. Used to define color in the template
template-color5
Opt
user defined field. Used to define color in the template
template-color6
Opt
user defined field. Used to define color in the template

Example 
 
http://apitest.mailvu.com/api/v1/manage?api-key=test-api&action=ADD_USER&&timestamp=1308000648&user-id=testuser123&hash=e822736279ef28072d4ecf85a88921cc

Return Values

Value
Description
ok
Action successful. User was added to the system
Error 301
When certain required parameters are missing
Error 304
When the hash generated by mailvu does not match the hash passed in the parameter.
Error 321
User ID already exists in the system

2.3. Change User
			
To change certain parameters of the user (plan/security etc.) you can call the endpoints with the following parameters

Parameter name
Type
Description
api-key
Required
ID of the partner. Given during setup by mailVU.

action
Req
CHANGE_USER: to add a user to the system
user-id
Req
A unique ID (Unique for your account) that identifies a user
timestamp
Req
Unix Timestamp is number of seconds since January 1, 1970, 00:00:00 GMT. See Appendix A on how to generate this timestamp. If the timestamp is more than 30 mins old, this message will be rejected. 
hash
Req
hexdigest(MD5(action+api-key+user-id+timestamp+partner-secret-key))
This is used to validate that the api request is coming from a valid partner and URL is not being reused/changed.
The partner-secret-key is assigned to the partner at the time of setup. It is never sent in plaintext.

name
opt
Name of the user
email
opt
Email address of the user
plan
opt
Plan used by the user. This will be required if your users get different limits per your contract with mailvu.
Please contact support@mailvu.com to agree on the possible values for this field.
security-level
optional
If your plan requires dashboard access instead of just widget, add this parameter to indicate proper security level
Leave it empty for for Widgets only
Possible Values:-
BASE_USER
USER
ADMINISTRATOR
signature
Opt
Signature text in HTML that will appear in the footer of the email and the landing page.
icon1_image_url
Opt
URL for social media icon. See appendix B for defaults
icon1_item_url
Opt
URL for users social media account
icon2_image_url
Opt
URL for social media icon. See appendix B for defaults
icon2_item_url
Opt
URL for users social media account
icon3_image_url
Opt
URL for social media icon. See appendix B for defaults
icon3_item_url
Opt
URL for users social media account
icon4_image_url
Opt
URL for social media icon. See appendix B for defaults
icon4_item_url
Opt
URL for users social media account
icon5_image_url
Opt
URL for social media icon. See appendix B for defaults
icon5_item_url
Opt
URL for users social media account
icon6_image_url
Opt
URL for social media icon. See appendix B for defaults
icon6_item_url
Opt
URL for users social media account
template-code
Opt
specific to your account. Default mailvu-business
template-logo-url
Opt
URL for the user’s logo.
template-color1
Opt
user defined field. Used to define color in the template
template-color2
Opt
user defined field. Used to define color in the template
template-color3
Opt
user defined field. Used to define color in the template
template-color4
Opt
user defined field. Used to define color in the template
template-color5
Opt
user defined field. Used to define color in the template
template-color6
Opt
user defined field. Used to define color in the template

Example 
 
http://apitest.mailvu.com/api/v1/manage?api-key=test-api&action=CHANGE_USER&&timestamp=1308000648&user-id=testuser123&hash=e822736279ef28072d4ecf85a88921cc

Return Values

Value
Description
ok
Action successful. User was added to the system
Error 301
When certain required parameters are missing
Error 304
When the hash generated by mailvu does not match the hash passed in the parameter.
Error 324
User does not exist in the system.

2.4.  Delete User
Warning: When a user is deleted, all the videos stored in the system are also deleted. Videos recorded earlier for this user will not play anymore

Parameter name
Type
Description
api-key
Required
ID of the partner. Given during setup by mailVU.

action
Required
DELETE_USER: to delete a user from the system.
user-id
Required
MAILVU User Id that was passed back while adding user
timestamp
Required
Unix Timestamp is number of seconds since January 1, 1970, 00:00:00 GMT. See Appendix A on how to generate this timestamp. If the timestamp is more than 30 mins old, this message will be rejected. 
hash
Required
hexdigest(MD5(action+api-key+user-id+timestamp+partner-secret-key))
This is used to validate that the api request is coming from a valid partner and URL is not being reused/changed.
The partner-secret-key is assigned to the partner at the time of setup. It is never sent in plaintext.


Return Values

Value
Description
ok
Action successful. User was added to the system
Error 301
When certain required parameters are missing
Error 304
When the hash generated by mailvu does not match the hash passed in the parameter.
Error 322
User does not exist in the system
Error 323
User is already deleted

3.  Message

3.1. Workflow



3.2.  Message API Endpoints

Environment
URL
Test
http://apitest.mailvu.com/api/v1/message
Production
http://api.mailvu.com/api/v1/message


3.3. Record Message

This action will allow users to record a message and when the message is done recording, they click on the “Save Video” and they will be redirected to the page passed in the redirect URL parameter. When the video is done encoding, you get a callback on your callback server with the details of the video.

Parameter name
Type
Description
action
Required
RECORD_MSG
api-key
Required
ID of the partner. Given during setup by mailVU.
request-id
Required
REQUEST-ID that is unique for each request.
This could be alpha numeric upto 40 chars length. This value will be returned in the callback.
If the same request id is sent again, the message will be rejected.
user-id
required
user id of the subscriber requesting this recording
timestamp
Required
Unix Timestamp is number of seconds since January 1, 1970, 00:00:00 GMT. See Appendix A on how to generate this timestamp. If the timestamp is more than 30 mins old, this message will be rejected. 
hash
Required
hexdigest(MD5(action+api-key+timestamp+user-id+partner-secret-key+request-id))
This is used to validate that the api request is coming from a valid partner and URL is not being reused/changed.
The partner-secret-key is assigned to the partner at the time of setup. It is never sent in plaintext.

redirect-url
optional
After the recording is complete When the user clicks on the “Save Video” button, the app will redirect to this page. This could be a dynamic URL specific to this user.

 
3.4. Record and Send Message
This action allows you to record a message and email it out to email addresses passed as parameters.

Parameter name
Type
Description
action
Required
RECORD_MSG
api-key
Required
ID of the partner. Given during setup by mailVU.

request-id
Required
REQUEST-ID that is unique for each request.
This could be alpha numeric upto 20 chars length. This value will be returned in the callback.
If the same request id is sent again, the message will be rejected.
user-id
required
user id of the subscriber requesting this recording
timestamp
Required
Unix Timestamp is number of seconds since January 1, 1970, 00:00:00 GMT. See Appendix A on how to generate this timestamp. If the timestamp is more than 30 mins old, this message will be rejected. 
hash
Required
hexdigest(MD5(action+api-key+timestamp+user-id+partner-secret-key+request-id))
This is used to validate that the api request is coming from a valid partner and URL is not being reused/changed.
The partner-secret-key is assigned to the partner at the time of setup. It is never sent in plaintext.

redirect-url
optional
After the recording is complete and a message is displayed, the app will redirect to this page. This could be a dynamic URL specific to this user.

from-email
optional
From Email address of the sender
from-name
optional
Name of the sender
to-email
optional
email address of the recipient 
cc-email
optional
email address to be cc’ed
email-subject
optional
Subject of the message
email-body
optional
Body of the message
 
3.5.  Send Message
This action allows you to (re) send an already recorded message to some email address passed as parameters
 
Parameter name
Type
Description
action
Required
SEND_MSG
api-key
Required
ID of the partner. Given during setup by mailVU.

request-id
Required
REQUEST-ID that is unique for each request.
This could be alpha numeric upto 20 chars length. This value will be returned in the callback.
If the same request id is sent again, the message will be rejected.
user-id
required
user id of the subscriber requesting this recording
timestamp
Required
Unix Timestamp is number of seconds since January 1, 1970, 00:00:00 GMT. See Appendix A on how to generate this timestamp. If the timestamp is more than 30 mins old, this message will be rejected. 
msg-id
Required
This is the message ID that was passed as parameter when the video was recorded
hash
Required
hexdigest(MD5(action+api-key+timestamp+user-id+partner-secret-key+request-id+msg-id))
This is used to validate that the api request is coming from a valid partner and URL is not being reused/changed.
The partner-secret-key is assigned to the partner at the time of setup. It is never sent in plaintext.

redirect-url
optional
After the recording is complete and a message is displayed, the app will redirect to this page. This could be a dynamic URL specific to this user.

from-email
Required
From Email address of the sender
from-name
Required
Name of the sender
to-email
Required
email address of the recipient 
cc-email
optional
email address to be cc’ed
email-subject
Required
Subject of the message
email-body
Required
Body of the message

3.6. Get Message History
Parameter name
Type
Description
action
Required
GET_MSG_HISTORY
api-key
Required
ID of the partner. Given during setup by mailVU.

request-id
Required
REQUEST-ID that is unique for each request.
user-id
required
user id of the subscriber requesting this recording
timestamp
Required
Unix Timestamp is number of seconds since January 1, 1970, 00:00:00 GMT. See Appendix A on how to generate this timestamp. If the timestamp is more than 30 mins old, this message will be rejected. 
msg-id
Required
This is the message ID that was passed as parameter when the video was recorded
hash
Required
hexdigest(MD5(action+api-key+timestamp+user-id+partner-secret-key+request-id+msg-id))
This is used to validate that the api request is coming from a valid partner and URL is not being reused/changed.
The partner-secret-key is assigned to the partner at the time of setup. It is never sent in plaintext.


3.7. Download File
Parameter name
Type
Description
action
Required
DOWNLOAD_ORIG (For original uploaded video)
DOWNLOAD_FLV (For flash version)
DOWNLOAD_MP4 (For mp4 version)
api-key
Required
ID of the partner. Given during setup by mailVU.

request-id
Required
REQUEST-ID that is unique for each request.
user-id
required
user id of the subscriber requesting this recording
timestamp
Required
Unix Timestamp is number of seconds since January 1, 1970, 00:00:00 GMT. See Appendix A on how to generate this timestamp. If the timestamp is more than 30 mins old, this message will be rejected. 
msg-id
Required
This is the message ID that was passed as parameter when the video was recorded
hash
Required
hexdigest(MD5(action+api-key+timestamp+user-id+partner-secret-key+request-id+msg-id))
This is used to validate that the api request is coming from a valid partner and URL is not being reused/changed.
The partner-secret-key is assigned to the partner at the time of setup. It is never sent in plaintext.


3.8. Callback

When mailvu calls your callback URL it will post the following parameters
Parameter name
Description
request-id
UNIQUE ID that represent either a user or a request by the user. This is the same ID that was sent during the recording request
playback-url
This is the URL you can use to play back the video. This value is URL encoded.
message-id
This is the Message ID that can be later used for other api activities.
thumbnail-url
URL of the thumbnail image
user-id
User Name sent in the request
width
Width of the video
height
Height of the video
duration
Duration of the video in seconds. e.g. 120 for a 2 min long video



4.  Video Upload
4.1. Process











1. Your client (Mobile phone or browser) uploads the video to our server. It passes a unique request Id that identifies that upload. This request Id could be any string (GUID).
2. Once the upload is complete the server responds with an OK message to the mobile phone client. On a desktop, you can supply a redirect URL in the request so we can redirect the user to that URL. This enables you to add a custom “Thank You” page.
3. mailVU then starts converting the video into other formats and creates a thumbnail image from the video.
4. After processing is complete, mailVU will call your callback server with an HTTP post and pass you details about the video. The details include a play back URL, URL for thumbnail image, video dimensions and length.
5. You can now store this information in your database and serve it up to the user.



4.2.  Upload URL
You can upload video using this URL : http://upload.mailvu.com/app/videoUploadApi.do

4.3.  HTTP Post Parameters 
 
Parameter name
Type
Description
accountId
Required
API-KEY
userName
Required
UserName of the user uploading the video. This username must have been created using the Create user API above. 
requestId
Required
REQUEST-ID that is unique for each request.
fileData
Required
This is the field in which you will send the video file
widthConstraint
Optional
If you want video to be a certain size, you can specify the width constraint. Do not include this field if you want default width
uploadCompleteUrl
Optional
If you want to redirect users to a page after the upload is complete, you include this URL and we will redirect to this URL after the upload is complete.
callbackUrl
Optional
By default the callback is sent to the URL configured at the time of setup. You can optionally include a URL during upload so the callback is sent to this URL instead.
4.4. Callback

When mailvu calls your callback URL it will post the following parameters
Parameter name
Description
request-id
UNIQUE ID that represent either a user or a request by the user. This is the same ID that was sent during the recording request
playback-url
This is the URL you can use to play back the video. This value is URL encoded.
message-id
This is the Message ID that can be later used for other api activities.
thumbnail-url
URL of the thumbnail image
user-id
User Name sent in the request
width
Width of the video
height
Height of the video
duration
Duration of the video in seconds. e.g. 120 for a 2 min long video





 
5.  Contact Management

5.1.  Contact Management API Endpoints

Environment
URL
Test
http://apitest.mailvu.com/api/v1/manage
Production
http://api.mailvu.com/api/v1/manage

5.2.  Add Contact
			
To Add/Remove Contacts you should call the above URL using HTTP protocol and pass the following parameters as POST or GET variables

Parameter name
Type
Description
api-key
Req
ID of the partner. Given during setup by mailVU.

action
Req
ADD_CONTACT: to add a contact to the system
user-id
Req
A unique ID (Unique for your account) that identifies a user
timestamp
Req
Unix Timestamp is number of seconds since January 1, 1970, 00:00:00 GMT. See Appendix A on how to generate this timestamp. If the timestamp is more than 30 mins old, this message will be rejected. 
hash
Req
hexdigest(MD5(action+api-key+user-id+timestamp+partner-secret-key))
This is used to validate that the api request is coming from a valid partner and URL is not being reused/changed.
The partner-secret-key is assigned to the partner at the time of setup. It is never sent in plaintext.

contact-id
Req
Primary key of contact which is in your system
email
opt
Email address of the contact
first-name
opt
First name of the contact
middle-name
opt
Middle Name of the contact
last-name
Opt
Last name of the contact
organization
Opt
Organization name
business-phone
Opt
Business Phone number
group1
Opt
Name of Group #1
group2
Opt
Name of Group #2
group3
Opt
Name of Group #3


Return Values

Value
Description
ok
Action successful. User was added to the system
Error 301
When certain required parameters are missing
Error 304
When the hash generated by mailvu does not match the hash passed in the parameter.
Error 321
User ID already exists in the system

5.3.  Delete Contact


Parameter name
Type
Description
api-key
Required
ID of the partner. Given during setup by mailVU.

action
Required
DELETE_CONTACT: to delete a user from the system.
user-id
Required
user-id key of the user whose contact is to be deleted
timestamp
Required
Unix Timestamp is number of seconds since January 1, 1970, 00:00:00 GMT. See Appendix A on how to generate this timestamp. If the timestamp is more than 30 mins old, this message will be rejected. 
hash
Required
hexdigest(MD5(action+api-key+user-id+timestamp+partner-secret-key))
This is used to validate that the api request is coming from a valid partner and URL is not being reused/changed.
The partner-secret-key is assigned to the partner at the time of setup. It is never sent in plaintext.

contact-id
Required
contact-id key in your system

Return Values

Value
Description
ok
Action successful. User was added to the system
Error 301
When certain required parameters are missing
Error 304
When the hash generated by mailvu does not match the hash passed in the parameter.
Error 322
User does not exist in the system
Error 323
User is already deleted
6.  Presenting videos on web or email

6.1. Showing the Video

In order to show the video passed as a link to you.
playback-url, height and width were passed to you as parameters in the callback URL

<iframe src=”{playback-url}” frameborder=”no” height=”{height}” width=”{width}”> </iframe>

6.2. Sending an Email with the video

You can send an email to  a user by embedding following HTML code in the email
<a href=”${playback-url}”><img src=”${thumbnail-url}” border=”0”/></a>




Appendix A: Generating a timestamp

Java:
		private long getTimeStamp()	{
	    		Date now=new Date();
	    		return now.getTime()/1000;
	    	}

PHP: 		time();

ASP:

	function get_unix_timestamp()
	    	current_date_time = now()
		get_unix_timestamp = DateDiff("s", "01/01/1970 00:00:00", current_date_time)
	end function


Appendix B:Social media icon URLS (or use your own)

Icon
URL

http://d2btk5j6rdz454.cloudfront.net/images/social/vector/facebook.png

http://d2btk5j6rdz454.cloudfront.net/images/social/vector/google-plus.png

http://d2btk5j6rdz454.cloudfront.net/images/social/vector/linkedin.png

http://d2btk5j6rdz454.cloudfront.net/images/social/vector/meetup.png

Are you kidding me? Who uses myspace anymore.

http://d2btk5j6rdz454.cloudfront.net/images/social/vector/blogger.png

http://d2btk5j6rdz454.cloudfront.net/images/social/vector/tumblr.png

http://d2btk5j6rdz454.cloudfront.net/images/social/vector/twitter.png

http://d2btk5j6rdz454.cloudfront.net/images/social/vector/twitter-2.png

http://d2btk5j6rdz454.cloudfront.net/images/social/vector/wikepedia.png

http://d2btk5j6rdz454.cloudfront.net/images/social/vector/wordpress.png

http://d2btk5j6rdz454.cloudfront.net/images/social/vector/youtube.png
