---
title: Hosting Static Website on AWS S3
date: 2018-11-01 21:30:56
tags: [aws, s3, static, website]
---

How to upload your static website onto AWS S3.

## Getting Started
----------------

##### tl;dr

1. Create AWS Account
2. Create new bucket
    2.1 Name it `www.name-of-your-website.com`
    2.2 Grant public read access
3. Upload static files
4. Go to Properties
    4.1 *Static website hosting*, and select first choice
    4.2 Enter `index.html`
    4.3 Endpoint is your URL
5. Go to Permissions
    5.1 Allow public to read
    5.2 Copy/paste code into Bucket Policy (Code below)
6. URL is accessible to the public

##### Create An Account

First things first, you have to create an account on [AWS](https://aws.amazon.com/). Can't start without one. They will ask for a payment method. You'll get charged a dollar to check if it's a real card and they'll return the money.

##### Setup AWS

###### Bucket Creation

Head over to S3 on the AWS console and create a new bucket. The bucket name is very important. It should be the name of the website you will be creating. If you already bought a domain name, then the bucket name should be that. Example: `www.google.com`. Make sure to include the *www* as that is important as well. If not, then any name is fine until you buy a domain name. Select a region that's closest to you and click next. Don't worry about the Configure Options step and click next again. Select "Grant public read access to this bucket" under *Manage public permissions*. Click next and then create bucket.

###### Bucket Overview

The new bucket should be listed on the table. Select it and it should take you to an overview of the bucket. Select upload. Drag and drop your files (everything from index.html to assets folders) into the window. After everything is uploaded, head over to the Properties tab.

###### Properties

Select the *Static website hosting* card and choose *Use this bucket to host a website*. Under Index document, enter `index.html` so it knows that is your main file for the website. Save and then move onto the Permissions tab.

###### Permissions

Hit the radio button under *Public access*. Checkbox the *List objects* and *Read bucket permissions* to allow the public to access your website. Next click on *Bucket Policy* and copy/paste the code:
``` yml
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AddPerm",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3::[www.name-of-your-website.com/*"
        }
    ]
}
```
 Hit save and that should be it.

##### What's my URL?

If you already bought a domain name from another website or Route53 then you would need to hook that up with the provided URL AWS hands you. Head back to the Properties tab and in the *Static website hosting* card is where you will find the URL. That URL is ready and live. You should be able to navigate to that link and see your website running live.