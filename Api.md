<base target="_blank">

# API
Typsy provides an API for basic operations on Members (the users within your Account).

## Actions
The supported actions are:
1. Create a member (assign a license to a new user)
2. Depart a member (removes the assigned license and prevents login)
3. Update a member's claims (update the claims attached to a member)

## Authentication
Typsy will provide you with the following items:
1. Typsy Key: A unique key used to generate a hash.  The key is in the following format: 4de6bcec-9ebe-4ba0-8040-48ce64949d31
2. Typsy Account ID: A unique numeric ID that identifies your account. E.g. 213

### Generating the HMAC SHA256 Hash
The following values are required to produce the hash which is included with each request.

1. UTC Timestamp
2. Typsy Account Id
3. Typsy Key

#### UTC Timestamp
The timestamp must be in the following format: yyyy-MM-ddTHH:mm:SS.fffffffZ and must be the current time.

In C# this is generated using the following line of code:

    DateTime.UtcNow.ToString("O");

Failure to provide a current UTC timestamp will result in a 401 status code and the following error message:

	"Timestamp '2018-11-14T11:19:03.7269943Z' outside of acceptable range. Ensure that the timestamp you provide is current UTC time - e.g. now is '2023-08-09T23:18:21.4801739Z'."

#### Typsy Account Id
Typsy will provide a unique Account Id to include with each request.  The value is numeric, e.g. 123

#### Typsy Key
The value for the Typsy-Key header value is a Hash of your Typsy Key and UTC timestamp.  

The value is created by concatenating your **Typsy Key** with the **UTC timestamp**. The hash must be generated for each request as it contains a timestamp.

If your Typsy Key is **4de6bcec-9ebe-4ba0-8040-48ce64949d31** and the UTC timestamp is **2018-11-14T11:19:03.7269943Z** then you concatenate as follows:

	{KEY}:{TIMESTAMP}

	4de6bcec-9ebe-4ba0-8040-48ce64949d31:2018-11-14T11:19:03.7269943Z

This value is then hashed with your Typsy Key to generate your HMAC-SHA-256-SECRET.

The secret generated by the above example is: 
	
	aa46f939cdb152633ed01f4a4b9b5f127430f277f40c72671a68419a4d16618b

This can be demonstrated/tested using the following tool: http://beautifytools.com/hmac-generator.php
1. Where it says 'Enter message here' place: 4de6bcec-9ebe-4ba0-8040-48ce64949d31:2018-11-14T11:19:03.7269943Z
2. Where it says 'Secret key' place: 4de6bcec-9ebe-4ba0-8040-48ce64949d31
3. Select alogorithim: sha256

![image](https://github.com/typsy-dev/documentation/assets/35910839/8e947f0d-a5ad-4426-b6fa-53643649cc8f)

___

##### Generating the encrypted key
Here is a [code sample](https://github.com/typsy-dev/web-player/blob/master/asp-net-core/asp-net-core/Utilities/EncryptionHelper.cs) in C# that demonstrates how to create the encrypted key.

___

These values must be added to the header of each request, see the following example from Postman.

1. Typsy-Timestamp: <INSERT UTC TIMESTAMP>
2. Typsy-Account-Id: <INSERT TYPSY ACCOUNT ID>
3. Typsy-Key: <INSERT HMACSHA256 HASH OF TYPSY KEY AND TIMESTAMP>

![image](https://github.com/typsy-dev/documentation/assets/35910839/52bdb4e2-0b96-4a2b-8ef5-7cbbd7665a3a)

## Validate Authentication
A request can be sent to validate that authentication is working correctly.

### Endpoint
GET to https://api.typsy.com/member/authenticated

### Request
Send an empty request but with all the required parameters for authentication.

### Response
If authentication has been successful you will be returned a 200 status code.  If you receive a 40x status code then investigate if all the required parameters for authentication have been constructed correctly and provided in the request.

## Member create

### Endpoint
POST to https://api.typsy.com/member/create

### Request
Example request to create a member (minimum information).  

	{
        "firstName": "FirstName",
        "lastName": "LastName",
        "email": "first.last@domain.com",
        "structures": [
            {
                "name": "Venue A",
                "roles": [
                    "member"
                ]
            }
        ],
        "options": {
            "sendInvitation": false,
            "createStructuresIfNotExist": true,
            "reactivateIfDeparted": false
        }
    }

Example request to create a member (additional information).  

	{
        "firstName": "FirstName",
        "lastName": "LastName",
        "email": "first.last@domain.com",
        "structures": [
            {
                "name": "Venue A",
                "roles": [
                    "member"
                ]
            },
            {
                "name": "Venue B",
                "roles": [
                    "manager"
                ]
            }
        ],
        "teams": [
            {
                "name": "Team A"
            }
        ],
        "claims": [
            {
                "key": "external_id",
                "value": "12345678910"
            }
        ],
        "options": {
            "sendInvitation": false,
            "createStructuresIfNotExist": true,
            "createTeamsIfNotExist": true,
            "reactivateIfDeparted": false
        }
    }

### Response

If the request is successful it is queued for processing and you will be provided with a receipt with the requestId.

The status is likely to be 'in progress'.

    {
        "statusUrl": "https://api.typsy.com/member/request-status/23365f4b-7ae8-4d4d-bb74-ad8b4bfee647",
        "requestId": "23365f4b-7ae8-4d4d-bb74-ad8b4bfee647",
        "status": "in progress",
        "errors": [],
        "success": true
    }

## Request status
To get the status of the request that has been submitted you must make a call to the request status endpoint.

### Endpoint
GET to https://api.typsy.com/member/request-status/{requestId}

#### Request not processed yet
If the initial request has not yet been processed you will receive a [204 No Content](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/204) result.  Wait a minute and make another request.

#### Request processed successfully
Example response where the member create request has been successful.

    {
        "workspaceId": 123456789,
        "requestId": "23365f4b-7ae8-4d4d-bb74-ad8b4bfee647",
        "status": "success",
        "errors": [],
        "success": true
    }

#### Bad request
If the member create request has failed (for example you attempt to assign to a structure that does not exist) the response will look like the following.

    {
        "workspaceId": null,
        "requestId": "23365f4b-7ae8-4d4d-bb74-ad8b4bfee647",
        "status": "failed",
        "errors": [
            {
                "code": "structure_name_does_not_exist",
                "description": "Venue B does not exist in your account."
            }
        ],
        "success": false
    }

Example response where the user already exists.

    {
        "workspaceId": null,
        "requestId": "23365f4b-7ae8-4d4d-bb74-ad8b4bfee647",
        "status": "failed",
        "errors": [
            {
                "code": "user_already_exists",
                "description": "A user with the email first.last@domain.com already exists within your account."
            }
        ],
        "success": false
    }

If you fail to produce a valid encrypted key then you will receive a 401 status code and the following error message:

	"Account validation failed. Check that the Encrypted Key 'c7ccdb43e6b81b778f7aaeb7f3d9d7be297e6813441e517b8d5fd9f648979452' is a valid HmacSha256."

## Member depart

### Endpoint
POST to https://api.typsy.com/member/depart

### Request
Example request to depart a member where you have the workspaceId (the unique identifier for the user within your account).  

    {
        "workspaceId": 123456789,
        "options": {
            "sendFarewellEmail": true
        }
    }

**COMING SOON:** Example request to depart a member by email.  

    {
        "email": first.last@domain.com,
        "options": {
            "sendFarewellEmail": false
        }
    }
