# Create Website 1

## Create a bucket

```sh
aws s3 mb s3://cors-fun-ks-36252
```

## Change block public access

```sh
aws s3api put-public-access-block \
--bucket cors-fun-ks-36252 \
--public-access-block-configuration "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=false,RestrictPublicBuckets=false"
```

## Create a bucket policy

```sh
aws s3api put-bucket-policy --bucket cors-fun-ks-36252 --policy file://bucket-policy.json
```

## Turn on static website hosting

```sh
aws s3api put-bucket-website --bucket cors-fun-ks-36252 --website-configuration file://website.json
```

## Upload our index.html file and include a resource that would be cross-origin

aws s3 cp index.html s3://cors-fun-ks-36252

## View the website and see if the index.html is there.

http://cors-fun-ks-36252.s3-website.ap-south-1.amazonaws.com

# Create Website 2

```sh
aws s3 mb s3://cors-fun2-ks-36252
```

## Change block public access

```sh
aws s3api put-public-access-block \
--bucket cors-fun2-ks-36252 \
--public-access-block-configuration "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=false,RestrictPublicBuckets=false"
```

## Create a bucket policy

```sh
aws s3api put-bucket-policy --bucket cors-fun2-ks-36252 --policy file://bucket-policy2.json
```

## Turn on static website hosting

```sh
aws s3api put-bucket-website --bucket cors-fun2-ks-36252 --website-configuration file://website.json
```

## Upload our javascript file

aws s3 cp hello.js s3://cors-fun2-ks-36252

## Create API Gateway with mock response and then test the endpoint


curl -X POST -H "Content-Type: application/json" https://jzjb1irwii.execute-api.ap-south-1.amazonaws.com/prod/hello


## Set CORS on our bucket

aws s3api put-bucket-cors --bucket cors-fun-ks-36252 --cors-configuration file://cors.json

## Remove Buckets and Objects
aws s3 rm s3://cors-fun2-ks-36252/hello.js
aws s3 rb s3://cors-fun2-ks-36252
aws s3 rm s3://cors-fun-ks-36252/index.html
aws s3 rb s3://cors-fun-ks-36252
