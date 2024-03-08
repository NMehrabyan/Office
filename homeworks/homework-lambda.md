## Homework

* Via aws cli create DynamoDB table
* Via aws cli create simple Lambda function (Hello World!)
* Via aws cli create API GW (REST API)
* Integrate API GW with Lambda

### Via aws cli create DynamoDB table
  ```sh
    aws dynamodb create-table \
    --table-name UserTable \
    --attribute-definitions \
    AttributeName=UserID,AttributeType=S \
    --key-schema \
    AttributeName=UserID,KeyType=HASH \
    --provisioned-throughput \
    ReadCapacityUnits=5,WriteCapacityUnits=5 \
    --no-verify-ssl
  ```

### Via aws cli create simple Lambda function (Hello World!)
  ```sh
    aws lambda create-function \
    --function-name HelloWorldFunction \
    --runtime nodejs16.x \
    --handler helloWorld.handler \
    --role arn:aws:iam::814976642708:role/RoleLambda \
    --cli-binary-format raw-in-base64-out \
    --zip-file fileb://D:/function.zip \
    --no-verify-ssl
  ```
### Via aws cli create API GW (REST API)
  ```sh
    aws apigateway create-rest-api --name HelloWorldAPI \
	--no-verify-ssl
  ```
### Integrate API GW with Lambda
* apigateway create-resource
```sh
   aws apigateway create-resource \
    --rest-api-id nos1wm8wd0 \
    --parent-id k9ida7o76h \
    --path-part hello \
    --no-verify-ssl
```	
* apigateway put-method

```sh
	aws apigateway put-method \
    --rest-api-id nos1wm8wd0 \
    --resource-id k9ida7o76h \
    --http-method POST \
    --authorization-type NONE \
    --api-key-required \
	--no-verify-ssl
```
* apigateway put-integration
```sh
	aws apigateway put-integration \
    --rest-api-id nos1wm8wd0 \
    --resource-id k9ida7o76h \
    --http-method POST \
    --type AWS_PROXY \
    --integration-http-method POST \
    --uri arn:aws:apigateway:us-east-1:lambda:path/2015-03-31/functions/arn:aws:lambda:us-east-1:814976642708:function:HelloWorldFunction/invocations  \
    --no-verify-ssl
```

* apigateway create-deployment
```sh	
    aws apigateway create-deployment \
    --rest-api-id nos1wm8wd0 \
    --stage-name prod \
    --no-verify-ssl
  ```












