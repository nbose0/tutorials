## Overview
This repository contains small tutorials and/or tips while developing using different technologies.

### AWS Lambda
#### Dependencies
* Dependencies should be zipped in */python directory and uploaded as a lambda layer. For example, if you want to use the `requests` package, do the following:
    1. On your local machine, open terminal
    2. Create a directory called `python` and enter the directory : `mkdir python && cd python`
    3. Install the dependency into the `python` directory created in step 2 : `pip3 install <name_of_dependency> -t .` for example, `pip3 install requests -t .`
    4. Zip the contents of the `python` directory : `cd .. && zip -r9 ../depedencies.zip python`
    5. Upload the zip file to aws as a lambda layer : `aws lambda publish-layer-version --layer-name dependencies --zip-file fileb://../dependencies.zip  --compatible-runtimes python3.8`
Now you can use your dependencies in your lambda function. For example, after doing the above and adding `dependencies` as a layer to your lambda function, you can call `requests`:
```
import requests

def lambda_handler(event, context):
    requests.get("https://www.google.com")
    return {
        'statusCode': 200
    }
```
