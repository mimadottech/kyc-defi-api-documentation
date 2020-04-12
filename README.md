# Bitdepositary DeFi API Documentation
![BITDEPOSITARY](./bdt.png)

# Description
**Note: To use this API, user must be KYC verified on [BDT DeFi](https://bdt-defi-ecd60.firebaseapp.com/) as a party on as a government.**

Once KYC verification is done on [BDT DeFi](https://bdt-defi-ecd60.firebaseapp.com/) as a party or as a government, follow the instructions to register for an API account to get an API key.

## Creating an API Account

![bdt defi api signup](./signup.png)
- In email field, user should use the email address that has been used in KYC

- In ethereum address field, user must use an ethereum address that has been used in KYC. Otherwise error will be shown and API account will not be created.

- Upon providing required and correct details for API account creation user will need to verify email using OTP that will be sent to email address provided by user.

- Once an account is created successfully, user can sign in into dashboard.

## Creating new API Key
![bdt defi api dashboard](./createApiKey.png)

- On clicking `Create New API Key` button, once again an OTP verification will happen
- Upon successfull OTP verification an API key will be generated and will be ready to use for an API calls

## Making API calls
- Examples provided on this call is using .http code. You can test api requests with your API Key pasting code in .http file and using [VSCODE](https://code.visualstudio.com/) with [REST CLIENT EXTENSION](https://marketplace.visualstudio.com/items?itemName=humao.rest-client).

- **Note:** Every api call requires Authorization header with basic authentication scheme.

- **In basic authentication scheme, base64 string must be provided with combination of username and password. Below is an example of authorization header.**

  ```http
  Authorization: Basic dXNlcm5hbWU6U0M2V0ZQUy1QNFZNQldKLUpXSlQ2VkgtMFJEOEVBUw==
  ```
- Above base64 encoded string is a combination of username and api key. Example: username:SC6WFPS-P4VMBWJ-JWJT6VH-0RD8EAS

## Test API Key

- Request Method: GET

- Request URI: https://bdt-defi-partner-api.herokuapp.com/api/dashboard/apiKeyAccessible

- Request Headers: Authorization

  ```http
  GET https://bdt-defi-partner-api.herokuapp.com/api/dashboard/apiKeyAccessible HTTP/1.1
  Authorization: Basic dXNlcm5hbWU6U0M2V0ZQUy1QNFZNQldKLUpXSlQ2VkgtMFJEOEVBUw==
  ```

- **Successfull Response:** with valid api key
  ```json
  { "msg":"ok" }
  ```

- **Error Response:** with invalid api key
  ```json
  {
    "errors":[],
    "data":{},
    "msg":"Invalid API Key"
  }
  ```

## Get user's KYC status as a partner

- Request Method: GET

- Request URI: https://bdt-defi-partner-api.herokuapp.com/api/partner/getUser/{emailAddress}

- Request Headers: Authorization, Content-Type

- Request parameters
  - emailAddress: email address of a user

  ```http
  GET https://bdt-defi-partner-api.herokuapp.com/api/partner/getUser/abcd@xyz.com HTTP/1.1
  Content-Type: application/json
  Authorization: Basic dXNlcm5hbWU6U0M2V0ZQUy1QNFZNQldKLUpXSlQ2VkgtMFJEOEVBUw==
  ```

- **Successfull Response:** if user has completed kyc - (status code 200)
  ```json
  {
    "data": {
      "kycDone": true
    },
    "msg": "User has completed KYC",
    "errorCode": null
  }
  ```

- **Successfull Response:** if user has not completed kyc - (status code 200)
  ```json
  {
    "data": {
      "kycDone": false
    },
    "msg": "User has not completed KYC",
    "errorCode": null
  }
  ```

- **Error Response:** if user not found - (status code 403)
  ```json
  {
    "data": {},
    "msg": "User not found",
    "errorCode": "EU403"
  }

- **Error Response:** if partner is not allowed access the user detail - (status code 401)
  ```json
  {
    "data": {},
    "msg": "You are not allowed to access the details of this user",
    "errorCode": "EP101"
  }
  ```

- **Error Response:** if user is blocked - (status code 422)
  ```json
  {
    "data": {},
    "msg": "User is blocked, you can not access details of blocked users",
    "errorCode": "EU100"
  }
  ```

- **Error Response:** if you are not registered as a partner - (status code 403)
  ```json
  {
    "data": {},
    "msg": "The given eth address is not registered as a partner",
    "errorCode": "EP403"
  }
  ```

- **Error Response:** internal system error - (status code 500)
  ```json
  {
    "data": {},
    "msg": "Something Went Wrong",
    "errorCode": "EI500"
  }
  ```

## Get user's KYC status as a government

- Request Method: GET

- Request URI: https://bdt-defi-partner-api.herokuapp.com/api/gov/getUser/{emailAddress}

- Request Headers: Authorization, Content-Type

- Request parameters
  - emailAddress: email address of a user

  ```http
  GET https://bdt-defi-partner-api.herokuapp.com/api/partner/getUser/abcd@xyz.com HTTP/1.1
  Content-Type: application/json
  Authorization: Basic dXNlcm5hbWU6U0M2V0ZQUy1QNFZNQldKLUpXSlQ2VkgtMFJEOEVBUw==
  ```

- **Successfull Response:** if user has completed kyc - (status code 200)
  ```json
  {
    "data": {
      "kycDone": true
    },
    "msg": "User has completed KYC",
    "errorCode": null
  }
  ```

- **Successfull Response:** if user has not completed kyc - (status code 200)
  ```json
  {
    "data": {
      "kycDone": false
    },
    "msg": "User has not completed KYC",
    "errorCode": null
  }
  ```

- **Error Response:** if user not found - (status code 403)
  ```json
  {
    "data": {},
    "msg": "User not found",
    "errorCode": "EU403"
  }

- **Error Response:** if user is blocked - (status code 422)
  ```json
  {
    "data": {},
    "msg": "User is blocked, you can not access details of blocked users",
    "errorCode": "EU100"
  }
  ```

- **Error Response:** if you are not registered as a government - (status code 403)
  ```json
  {
    "data": {},
    "msg": "The given eth address is not registered as a partner",
    "errorCode": "EG403"
  }
  ```

- **Error Response:** internal system error - (status code 500)
  ```json
  {
    "data": {},
    "msg": "Something Went Wrong",
    "errorCode": "EI500"
  }
  ```

