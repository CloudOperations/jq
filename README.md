jq
==

System: Tested on Mac 10.8.5

####What is JQ?

It is a command-line *JSON processor*. It is used to slice and *filter* and
map and *transform structured data* with the same ease that sed, awk, grep


####Installation
```
wget http://stedolan.github.io/jq/download/linux64/jq
chmod +x ./jq
export PATH=${PATH}:$WORKING_DIR`
```

The PATH is an environment variable. It is a colon delimited list of directories that your shell searches through when you enter a command. 
We need to add JQ directory to $PATH.

####Now Let's play

SAMPLE OF A JSON FILE
- Access EC2 on-demand pricing JSON document for Linux
http://aws-assets-pricing-prod.s3.amazonaws.com/pricing/ec2/linux-od.js

1-
```
curl 'http://aws-assets-pricing-prod.s3.amazonaws.com/pricing/ec2/linux-od.js'
```

2-
```
curl 'http://aws-assets-pricing-prod.s3.amazonaws.com/pricing/ec2/linux-od.js' | jq '
```
