# KYC.Crypto DeFi API Documentation
![KYC.Crypto](./bdt.png)

# Description
**Note: To use this API, a user must be KYC verified on [BDT DeFi](https://my.kyc-crypto.com) as a party on as a government.**

Once KYC verification is done on [BDT DeFi](https://my.kyc-crypto.com) as a party or as a government, follow the instructions to register for an API account to get an API key.

## Creating an API Account
- Visit [Partner Dashboard](http://partner.kyc-crypto.com)

![PARTNERT API SIGNIN](./signin.png)
- First when you visit dashboard, you will see a signin page. Go to the signup page by clicking on "Signup Here" link shown below the signini button

![PARTNER API SIGNUP](./signup.png)
- In the email field, a user should use the email address that has been used in KYC

- In ethereum address field, a user must use an ethereum address that has been used in KYC. Otherwise, an error will be shown and an API account will not be created.

- Upon providing required and correct details for API account creation a user will need to verify email using OTP that will be sent to an email address provided by a user.

- Once an account is created successfully, a user can sign in into the dashboard.

## Creating new API Key
![partner api dashboard](./createApiKey.png)

- On clicking `GENERATE NEW` button, once again an OTP verification will happen
- Upon successful OTP verification, an API key will be generated and will be ready to use for an API calls

## Making API calls
- Examples provided on this documentation is using .http code. You can test API requests with your API Key, pasting code in .http file and using [VSCODE](https://code.visualstudio.com/) with [REST CLIENT EXTENSION](https://marketplace.visualstudio.com/items?itemName=humao.rest-client).

- **Note:** Every API call requires an Authorization header with a basic authentication scheme.

- **In basic authentication scheme, base64 string must be provided with a combination of a username and an API Key. Below is an example of authorization header.**

  ```http
  Authorization: Basic dXNlcm5hbWU6U0M2V0ZQUy1QNFZNQldKLUpXSlQ2VkgtMFJEOEVBUw==
  ```
- Above base64 encoded string is a combination of a username and an API key. Example: username:SC6WFPS-P4VMBWJ-JWJT6VH-0RD8EAS

## Test API Key

- Request Method: GET

- Request URI: https://partner.kyc-crypto.com/api/dashboard/apiKeyAccessible

- Request Headers: Authorization

  ```http
  GET https://partner.kyc-crypto.com/api/dashboard/apiKeyAccessible HTTP/1.1
  Authorization: Basic dXNlcm5hbWU6U0M2V0ZQUy1QNFZNQldKLUpXSlQ2VkgtMFJEOEVBUw==
  ```

- **Successful Response:** with valid api key
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

## Get a user's KYC status as a partner

- Request Method: GET

- Request URI: https://api.kyc-crypto.com/api/partner/getKycStatus/{emailAddress}

- Request Headers: Authorization, Content-Type

- Request parameters
  - emailAddress: email address of a user

  ```http
  GET https://partner.kyc-crypto.com/api/partner/getKycStatus/starktechservice@gmail.com HTTP/1.1
  Content-Type: application/json
  Authorization: Basic dXNlcm5hbWU6U0M2V0ZQUy1QNFZNQldKLUpXSlQ2VkgtMFJEOEVBUw==
  ```

- **Successful Response:** if a user has completed kyc - (status code 200)
  ```json
  {
    "data": {
      "kycDone": true
    },
    "msg": "User has completed KYC",
    "errorCode": null
  }
  ```

- **Successful Response:** if a user has not completed kyc - (status code 200)
  ```json
  {
    "data": {
      "kycDone": false
    },
    "msg": "User has not completed KYC",
    "errorCode": null
  }
  ```

- **Error Response:** if a user not found - (status code 403)
  ```json
  {
    "data": {},
    "msg": "User not found",
    "errorCode": "EU403"
  }

- **Error Response:** if partner is not allowed access a user detail - (status code 401)
  ```json
  {
    "data": {},
    "msg": "You are not allowed to access the details of this user",
    "errorCode": "EP101"
  }
  ```

- **Error Response:** if a user is blocked - (status code 422)
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

## Get a user's KYC status as a government

- Request Method: GET

- Request URI: https://api.kyc-crypto.com/api/gov/getKycStatus/{emailAddress}

- Request Headers: Authorization, Content-Type

- Request parameters
  - emailAddress: email address of a user

  ```http
  GET https://partner.kyc-crypto.com/api/partner/getKycStatus/starktechservice@gmail.com HTTP/1.1
  Content-Type: application/json
  Authorization: Basic dXNlcm5hbWU6U0M2V0ZQUy1QNFZNQldKLUpXSlQ2VkgtMFJEOEVBUw==
  ```

- **Successful Response:** if a user has completed kyc - (status code 200)
  ```json
  {
    "data": {
      "kycDone": true
    },
    "msg": "User has completed KYC",
    "errorCode": null
  }
  ```

- **Successful Response:** if a user has not completed kyc - (status code 200)
  ```json
  {
    "data": {
      "kycDone": false
    },
    "msg": "User has not completed KYC",
    "errorCode": null
  }
  ```

- **Error Response:** if a user not found - (status code 403)
  ```json
  {
    "data": {},
    "msg": "User not found",
    "errorCode": "EU403"
  }

- **Error Response:** if a user is blocked - (status code 422)
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

