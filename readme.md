AWS S3 Multipart Upload from Browser
====================================

What was done here
------------------
Slight modification of @hridayeshgupta's code to clean up some bugs.

WARNING
-------
My caveat:
I did not clean up this code a lot, but rather just fixed some bugs that prevented it from working properly for me. I have a Python back end instead of PHP, but this script works very well.

Original caveat:
The codes are not well tested, poorly written, and kind of a mess.
You should get inspiration (!) from the code and make your own version.
Server need to have some validation which it currently lacks. Just go
though the code and you will understand the situation :p
This is just like a demonstration, you should customize it as your own
need.

How to use it
-------------
1. set the constants in config.php
2. Enable CORS in S3 bucket where you want to upload files. Essentially through web console in s3 bucket propreties->permissions set CORS to the following XML.
  - Note that the exposed Etag header is critical to making this script work.
```
<?xml version="1.0" encoding="UTF-8"?>
<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
    <CORSRule>
        <AllowedOrigin>yourdomain.com</AllowedOrigin>
        <AllowedMethod>GET</AllowedMethod>
        <AllowedMethod>POST</AllowedMethod>
        <AllowedMethod>PUT</AllowedMethod>
        <AllowedMethod>DELETE</AllowedMethod>
        <MaxAgeSeconds>3000</MaxAgeSeconds>
        <ExposeHeader>Etag</ExposeHeader>
        <AllowedHeader>*</AllowedHeader>
    </CORSRule>
</CORSConfiguration>
```

3. Open upload.html to see demo.
Following are options can be configured when making upload object.
```
	PART_SIZE: 5 * 1024 * 1024,
	SERVER_LOC: 'server.php',
	MAX_PARALLEL_UPLOADS: 2,
	onServerError: function(){},
	onProgressChanged: function(){},
	onUploadCompleted: function(){}
```

References
-------------
1. Overview on aws multipart upload http://docs.aws.amazon.com/AmazonS3/latest/dev/mpuoverview.html
2. Multipart API http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingRESTAPImpUpload.html
3. S3 authentication of REST calls http://docs.aws.amazon.com/AmazonS3/2006-03-01/dev/RESTAuthentication.html
4. Cross Origin Request Sharing(CORS) overview https://developer.mozilla.org/en-US/docs/HTTP/Access_control_CORS
5. Enabling CORS in s3 http://docs.aws.amazon.com/AmazonS3/latest/dev/cors.html

Files
-----

* server.php - The server file, it does the creation, completion of
multipart upload. And also it signs the requests to make the browser to
upload the file parts.

* upload.js - An attempt to make an object out of the javascript part,
the smallest documentation is present in the file

* upload.html - Demonstration of upload.js, if you are too lazy, you can
use this as your starting point.

* Libraries - they are helpers. jquery, firebug_lite, etc. You should
respect their licenses.

License
-------
MIT

Contributors
------------
@cjshawMIT

forked from:
@hridayeshgupta - Hridayesh Gupta - https://github.com/hridayeshgupta

@thecolorblue - Brad Davis - https://github.com/thecolorblue
@ienzam - Md. Enzam Hossain - https://github.com/ienzam
