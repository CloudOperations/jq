jq - JSON Parser
================

*Testing Environment/System: AWS Engineering AMI (Linux AMI)*

####What is JQ?

It is a command-line **JSON processor**. It is used to slice and **filter** and
map and **transform structured data** with the same ease that sed, awk, grep


####Installation
```
wget http://stedolan.github.io/jq/download/linux64/jq
chmod +x ./jq
export PATH=${PATH}:$pwd`
```

The PATH is an environment variable. It is a colon delimited list of directories that your shell searches through when you enter a command. 
1-Download jq
2- Make jq executable
3-Add jq directory to $PATH (where $pwd is the current directory)


####Now Let's play

*[Sample of JSON file](https://s3.amazonaws.com/jqdemo/jqdemo.txt)*
*([Reference](http://aws-assets-pricing-prod.s3.amazonaws.com/pricing/ec2/linux-od.js))*

1- Check the file format
```
curl 'https://s3.amazonaws.com/jqdemo/jqdemo.txt'
```

2- Get all fields
```
curl 'https://s3.amazonaws.com/jqdemo/jqdemo.txt' | jq '.'
```

3- Get the value of 'rate'
```
curl 'https://s3.amazonaws.com/jqdemo/jqdemo.txt' | jq '.config | .rate'
```
3- Get all the 'sizes' of the EC2 instances featured in the document
```
curl 'https://s3.amazonaws.com/jqdemo/jqdemo.txt' | jq '.config | .regions[] |.instanceTypes[] |. sizes[] |.size'
```
4- Get the price of 'm1.large'
```
curl 'https://s3.amazonaws.com/jqdemo/jqdemo.txt' | jq '.config | .regions[] |.instanceTypes[] |. sizes[] |select(.size=="m1.small") |.valueColumns[] |.prices |.USD'
```
4- Get the price of 'm1.large'
```
curl 'https://s3.amazonaws.com/jqdemo/jqdemo.txt' | jq '.config | .regions[] |.instanceTypes[] |. sizes[] |select(.size=="m1.small") |.valueColumns[] |.prices |.USD'
```
5- add more details (more columns) to #4  
```
curl 'https://s3.amazonaws.com/jqdemo/jqdemo.txt' | jq -r ".config | .regions[] |.instanceTypes[] |. sizes[] |select(.size=="\"m1.small"\") | [.size,.vCPU,.ECU,.memoryGiB,.storageGB,(.valueColumns[] |.prices |.USD)] | @csv"
```
Other variants
```
curl 'https://s3.amazonaws.com/jqdemo/jqdemo.txt' | jq  '.config | .regions[] |.instanceTypes[] |. sizes[] |select(.size=="m1.small") | [.size,.vCPU,.ECU,.memoryGiB,.storageGB,(.valueColumns[] |.prices |.USD)] | @csv'
```

####Wnat to know more?

jq can do a lot more!! Please check http://stedolan.github.io/jq/manual/



####Appendix:

JSON Snippet
```
"config":{
      "rate":"perhr",
      "valueColumns":[
         "vCPU",
         "ECU",
         "memoryGiB",
         "storageGB",
         "linux"
      ],
      "currencies":[
         "USD"
      ],
      "regions":[
         {
            "region":"us-east",
            "instanceTypes":[
               {
                  "type":"generalCurrentGen",
                  "sizes":[
                     
                            {
                                "size": "m3.medium",
                                "vCPU": "1",
                                "ECU": "3",
                                "memoryGiB": "3.75",
                                "storageGB": "1 x 4 SSD",
                                "valueColumns": [
                                    {
                                        "name": "linux",
                                        "prices": {
                                            "USD": "0.113"
                                        }
                                    }
                                ]
                            }
'''


