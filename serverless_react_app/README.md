## Servless React App using AWS (API Gateway, Lambda, DynamoDB, S3)

- font awesome used for icons

- AWS S3 Bucket created

- AWS Bucket Policy
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::invprocessing-aws/*"
            ]
        }
    ]
}
```
$ aws configure
$ aws s3 sync build s3://invprocessing-aws

API Gateway - New REST API created.

- Lambda Function creation with GET - Method Test 
Index.js
```
const AWS = require('aws-sdk');
const docClient = new AWS.DynamoDB.DocumentClient({region : 'eu-west-2'});


exports.handler = function (event, context, callback) {
    
    let scanningParameters = {
        TableName : 'InvoiceTable'
    };
    
    docClient.scan(scanningParameters, function(err, data){
        if (err) {
            callback(err, null);
        } else {
            callback(null, data.Items);
        }
    });

};
```
- Simple Table with DynamoDB created

- Enabled CORS on API Gateway Get Method
