<base target="_blank">

# Single Sign On (SSO) Integration:

## Overview:
SSO Integrations uses SAML2 (Security Assertion Markup Language).

- The customer will provide an Identity Provider (IDP) - for example, Azure Active Directory. The IDP will be responsible to authenticate and authorize the user.
- Typsy will act as the Service Provider (SP).
- The client (IDP) will authenticate and authorize the user and redirect the user to Typsy (SP) along with the claims required to allow the user to access the Typsy site.

## Claims
The following claims will be passed by client (IDP) to Typsy (SP): 

- **Unique identifier for the user (Required)** - This identifier is unique to the user in the IDP
- **Account identifier (Required)** - This identifier will be used to map the user to an account in Typsy. For example - the client might have one account per region in Typsy. So this claim would pass the region value so that the user can be mapped to the correct account in Typsy.
- ***Email address (Required)** - A user is created in Typsy using the email address. If the user does not have an email address, then a fictitious email address can be passed for the user - e.g. {unique-identifier-for-user}@acme.com.
- **Structure (Optional)** - Department or Venue or Group (known in Typsy as a Structure) - If this value is passed, then the corresponding Structure will be created in Typsy in the account linked to the account identifier and the user will be added to this Structure.
- **Team (Optional)** - If this value is passed, then the team will be created in Typsy in the account linked to the account identifier and the user will be added to this team.
- **Job Roles (Optional)** (should map to Typsy job role) - If this value is passed, then the user will be mapped to the corresponding job role in Typsy.

Note: Department or Venue or Group (Structure) is an optional claim. But if this claim value is not passed as part of the sign in process and the user in Typsy is not already assigned to any department or Venue or Group in the account, then the user will be displayed the workflow to select the Department or Venue or Group when the user is redirected to Typsy (SP) from the LMS (IDP).
   
## Setup and testing requirements:
- Client will setup the IDP with the required and optional claims and then create the IDP metadata file and provide it to Typsy.
- Using the IDP metadata file provided by the client, Typsy will complete the setup at their end and provide the SP metadata file to the client.
- Client can then use the SP metadata file to complete the IDP setup at their end. For example - configure the SP reply url in the IDP.
- Client will let Typsy know that the IDP configuration is complete.
- If client is able to provide a test login to the Client LMS, then Typsy can test the SSO login process for the test login and let the client know if the testing was successful.
- If client is not able to provide a test login to the Client LMS, then the client LMS IDP setup team and Typsy can get on a call and test the SSO login process for the test login and verify that it is successful.

## Initiating SSO
There are multiple ways that the SSO process can be initiated.

### Login with an email from known domain name
If the user is logging in with an email address that uses a company domain name then the authentication process will automatically redirect to the IDP.

For example, if SSO is connected to an account that has the acmehotel.com domain name and a user has the email address name@acmehotel.com then the Typsy login screen will recognize that the user must be redirected to their IDP.

### Force login with SSO
Some customers provide a link on their Intranet or Learning Management System (LMS) to Typsy.  This link can be used to force the SSO process.

- A user will access Typsy via the url - https://member.typsy.com?idp=[unique-idp-created-for-the-client-by-Typsy]
- When the user enters the above url in the browser, Typsy (SP) will redirect the user to the client LMS (IDP).

Alternatively a customer can setup https://typsy.company.com with a redirect to https://member.typsy.com?idp=[unique-idp-created-for-the-client-by-Typsy]
