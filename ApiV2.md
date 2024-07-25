<base target="_blank">

# API V2
Typsy provides an API for basic operations on Users and Accounts.

## Actions
The supported actions are:

Authenticate
1. [Test Authentication with the API](#authentication)

User API
1. [Create a user (assign a license to a new user)](#user-create)
2. [Depart a user (removes the assigned license and prevents login)](#user-depart)
2. [Update a user](#user-update)
3. [Add a user to a Structure](#user-add-structures)
4. [Remove a user from a Structure](#user-remove-structures)
5. [Add a user to a Team](#user-add-teams)
6. [Remove a user from a team](#user-remove-teams)
7. [Add Claims to a user](#user-add-claims)
8. [Remove Claims from a user](#user-remove-claims)
9. [Get Users list](#list-users)
10. [Get a User](#get-user)

Account API
1. [Create a new child account](#account-create)
2. [Add a Role to a User in a child account](#account-role-add)
3. [Remove a Role from a User in a child account](#account-role-remove)
4. [Get Accounts list](#list-accounts)
5. [Get a Account](#get-account)

## Authentication
Typsy will provide you with the following items:
1. Client Id: A unique key which is related to your account within Typsy
2. Client Secret: A secret key (similar to a password) which is needed to authenticate. Note that this value is one way hashed when stored in our database. Once we provide it to you, we will no longer be able to retrieve the value, but a new client secret can be generated.

### Authenticating with OAuth2 and generating the bearer token

#### Endpoint
POST to https://api.typsy.com/connect/token

#### Request
The following information needs to be provided to generate a bearer token.

Header
- Content-Type: application/x-www-form-urlencoded

Form Body
- grant_type : client_credentials
- client_id : The client id provided to you by Typsy
- client_secret : The client secret provided to you by Typsy

#### Response
- access_token : The bearer token which you will use to authenticate requests to the API
- token_type : The token type you have been granted (will always be bearer)
- expires_in : The time to live (TTL) of the token
- scope : Additional scopes granted to your token (will always be offline_access)
- refresh_token : An additional token which can be used to generate further bearer tokens with the same claims and scope

Example response of a successful request
```
{
    "access_token": "eyJhbGciOiJSU0EtT0FFUCIsImVuYyI6IkEyNTZDQkMtSFM1MTIiLCJraWQiOiJCNUE2NzhCNTRFMEIxRUJEMTI4MzMwOEYwRjRCMEY4Q0JCMzFGMjQ4IiwidHlwIjoiYXQrand0IiwiY3R5IjoiSldUIn0.BbU-954CEdwi01dY2IPO1jVkc2WSOlueIYa_VTQkZuXwcvLbZ-KCQxuuciJV2vG3tJj97sRB_n40TUogJY-32KcQrlU_JUcQU6m6UvpQkCad19lLg_0kefakH9NrnGcBi1s7T9Stl4Z3hbu_JYj26h2ELliIR2t4LWXC0D6SY_RgZwbDCnSi4qN1ByaoVGHa-8O6EZMdc1Dpopr3UI2wVFlA4BZOmbsIgQ1xcmjENrKAIHQe-45DeQkz8HdZTNnxdWh_FyYNCi_OAMYqJvoSOhqJSH5_FPL0x2yFyBNnAGwlkAI4yrvnr6oGPJa5QoUGA0UwZCd8uMgotpktvMrPeA.D3Ehq0i6MiNl7TNZtSPoaA.1Xzw7kjkkExw2qro31BMK3o_nSk5V1sz73Qlcs8SksbLucQBKkArBiPTgHky4MHvFv7n81YaXRMb7cPrp5reZYcQLO2CFvj8Qz76m4fn4GxbgFp7cFNtxlnEqcEr6H_ZHL1zWp2mK1b6rPfGIJvAv5UX7PbGYSquQ1za_xmudFb5Eck1oBBBwb9GGyTG8OMc0C5_UnVXdq4TdNBG-obUXckTCSjQCxwkSVjNAVSUnmsjk4eRWNfnCtW1LdzU8m7NHilM3EXLMyo1VLMx3vursZ08oP_tbqDUVjqx3_zu7IKYuA74HBQTP3tg-bC7mYdlaLx2vPA5l-aqunZHxtjBrA30lT3EgoTvsPn9sTzSjlTXAo8CX0EpfjKBKs93RJt9O0iTC-Vy0oRqOkBeH9JWWlGdS37W5NcNHV8mQdsFPekfzOqYNi53sdHb040JsiENCQ_YSz6a5vMg8iSeZvcbuBpn_npwmNFQjpponn4PtShGrdq0fMRxLH_p-MaUICS4Y-DfGJaUTBaNCaucuWV1WejH3zq3zrPoqaqMIPBUUPICThK2lKajLbyUoviq-T-njwYbFtU40c1TFwY3mD2xDdwNMgY400mbV73PkHHiafyE84jxrwWZH_tWXhgzuuVFTn1Md2Hz9OlxN2GCqqNj2LnuR4sk-xa9u3gR0Ce14CFG5LFAr75fEhRw0HaJJI3y-F9nG6n5DUB3JvcFM2X-Jcyi5O30nQ1rmUE-eYV0QamxBM3b-qtBADQpR6G_nHNzvP3DmCS3aD-9xJXceM7b230RZdNf6dCVK6gXgRMEp-V1RCvBeuxBocFCVIZm0q-Y1f1ozBGxGbioM5pUEdKFLgW-PgAWpdeM62odiBv4WvMoIsAKPcmla-dJ3Ckq3NyV1jN7bFyfAtlch2lIcssB8SoBbPlYTXAtdRXf2dM6F23hCV4rrC-OA6D8gIpS6xnG5FmbVXvURjjifCllv__T-B5kqw2VgPTe5fnQzsvbBV3ro3CEhqR05f4irAA25sEgciHcTd6sgH6uw42DSvfIGzsoBNilI9LAnrkhf5NTXg5tVndNY6W-2xSlqRsd9_LEqTY4OgBrGZRsnJRet9MbJHkXHbWu4h3lYu-w0zQj1lhAXvfOyVKUCG5lEEs1i7Sx70pY64sGq9ODe7y6c0paur6HzpKoiLt3V43GD-Tf1l-4AkdiNclJkZB2zj_RjJwPFRdM73qnHxRBDPuCfBjjzqweex19JXqf6gSmgivEWK4PU6WfANdgb0EpBRaE2JYqOt04YcYVkb21HAqFuQD4WAAl73_L2lKmDRcGr2_L8TdpLuSaxDG3MuZ-OVNavvj2.CvM9seoW1LF0-RQ0oMrC01KaIVhQTuehtRGV918UcGA",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "offline_access",
    "refresh_token": "eyJhbGciOiJSU0EtT0FFUCIsImVuYyI6IkEyNTZDQkMtSFM1MTIiLCJraWQiOiJCNUE2NzhCNTRFMEIxRUJEMTI4MzMwOEYwRjRCMEY4Q0JCMzFGMjQ4IiwidHlwIjoib2lfcmVmdCtqd3QiLCJjdHkiOiJKV1QifQ.EgV-ZJMIj1bQIowzoKVIQrKCRpNb_JjftEaddqQPZ4aFbY3wF1p0Tj0yTsapbo7T2W0oVKTerknNpHLTIaAmb1dwH-_ovk_BxIdtH6ZXD4GVshSOpXzTQRCsWuX7bRDYV5Ta-mcX716ReACjV_FfGeCnntU3k9zs3pUR4ZykACrHdJRRv8WG93BzUIwFjVSftl0SFMNMb9CSDg-m7mOab_Z3afYyzrufr0k6GVsgp-kf2mxSZRVclByN3ILVEaoMySypmMMJexzDy381iKLgrx-vyebusKLGoanzT92RM7w-lEyXMlXtVVlA0EuoHAuKe0ltdB5wH9OIOQuH_jwDCg.t7pA-4B9rMeeT3J7SLRaqw.PdWFznPn_IrcTE4lIJ7IzySCg4LValKwVMC_0Lwq4IpK6FE7nRxocGZgJ_ZqBNaqTyxW34iVndbtNXjeVJK7-K4R6i40AyNRbsz75a5x6J2ChGC4RTtfAQ6ZTkUix9sGzwBfeY_BOzs0kkTRly09n8Ua6SkZSlvHBxmU0A7jUB-EpICUu_-09uG7yRtDnGKdHkp6J1amh84kYkHYDlKbfUjvP9jlQWx0wCJCLoXtMOpuhN7q5w2MF0fGGwJgOsJ7FljC6qegF-0lM8KVV7XjdQgH35wiOd7_8aPz-ijWinI1EPyq8o5n_Z3cQb0HhQzrCvIIX2p8lDdMiQzzCo7XuQntIU228pwlvUxhGmPOh1vXM0x5exAey6FOqdDq6z7Xb4yo0H1mm3R8f9iWqIk8XGwYaGcUUD1I9h7Lqfty2E5EtdIrATm7KOfOjoQa3cswa7Ih1R-YTDdTGQ95inTgObMEq8AI9_3koLPffl-9XpD-uatAYNrW-lpCpMQJCY00-nzuTrVQ7xHSijHtQxPdenJNBRPfksBNPUaSujVMQGP3kEFrVZ0XCmBk0ah-EunSPa3fDimPJqdUCLff_2RK_ZJ15VBj5z7VsdnWotR02Tmbd0F6BIe0kZfOlBllkPVYKjTn4hJv9lPOh2aWINYJOcRqmy3E8TwEeABeYKkFnwmRa27rJABDj7nUKYWdCdmnJAhxo2snIUaN6TbvPuA-5ku5UQ7IJYta9YCMAQs2NN070xwBhsq8jdois8a_PdlhNHZGSGg2qfdVDGvCpphqdoqOPxGF7MOXssjY7kWzeaq-T8SwEo3NFg3UasmdZhpj4NQnCIxUwRdOHD8DyBBex2jC4GnTVjXGt9UnICC-3mlUd3Bt5vSEPGWJ_Ez60vW8yhkpST7oA_IvjB6nNzOKvlF7Aad6M3oW3lJc1wL7p1qI7nf2PedM0jnTUjPDigbFq1qdsX_WJ_OTB34382R6kpw6d89yQNgDzfJhjmouC_g4NWDorjourzZhLWw0MhBdS4KganwaJzckGUgnX9zAonbtpYV1Yb6dWlTbxBbn_Qta_q3mVkma8nsHHYZBBS3ekxuWcH3JJO33_NzUt_HsN-GX_2bvqHwEN7pK4qvZi2DcKWyfrrFXDzWrv9qr37plhwzDGBXTuPLe6ORE9Ibro6t6z2Nfl9r-nvhLxBxTsK_08g4all57maGMAkfb4XvEPTizKVFockKTLub0HWJGEcbMjHNYSyuFPvAiUmEXrwo.Rue3ruRy_9eQd-_zBH90v-__feebIi8apYbaEMDOQVs"
}
```

### Using the refresh token

#### Endpoint
POST to https://api.typsy.com/connect/token

#### Request
The following information needs to be provided to generate a bearer token.
- Content-Type: application/x-www-form-urlencoded
- grant_type : refresh_token
- client_id : The client id provided to you by Typsy
- client_secret : The client secret provided to you by Typsy
- refresh_token : The token given to you after generating your original bearer token

#### Response
- access_token : The bearer token which you will use to authenticate requests to the API
- token_type : The token type you have been granted (will always be bearer)
- expires_in : The time to live (TTL) of the token
- scope : Additional scopes granted to your token (will always be offline_access)
- refresh_token : An additional token which can be used to generate further bearer tokens with the same claims and scope

Example response of a successful request
```
{
    "access_token": "eyJhbGciOiJSU0EtT0FFUCIsImVuYyI6IkEyNTZDQkMtSFM1MTIiLCJraWQiOiJCNUE2NzhCNTRFMEIxRUJEMTI4MzMwOEYwRjRCMEY4Q0JCMzFGMjQ4IiwidHlwIjoiYXQrand0IiwiY3R5IjoiSldUIn0.BbU-954CEdwi01dY2IPO1jVkc2WSOlueIYa_VTQkZuXwcvLbZ-KCQxuuciJV2vG3tJj97sRB_n40TUogJY-32KcQrlU_JUcQU6m6UvpQkCad19lLg_0kefakH9NrnGcBi1s7T9Stl4Z3hbu_JYj26h2ELliIR2t4LWXC0D6SY_RgZwbDCnSi4qN1ByaoVGHa-8O6EZMdc1Dpopr3UI2wVFlA4BZOmbsIgQ1xcmjENrKAIHQe-45DeQkz8HdZTNnxdWh_FyYNCi_OAMYqJvoSOhqJSH5_FPL0x2yFyBNnAGwlkAI4yrvnr6oGPJa5QoUGA0UwZCd8uMgotpktvMrPeA.D3Ehq0i6MiNl7TNZtSPoaA.1Xzw7kjkkExw2qro31BMK3o_nSk5V1sz73Qlcs8SksbLucQBKkArBiPTgHky4MHvFv7n81YaXRMb7cPrp5reZYcQLO2CFvj8Qz76m4fn4GxbgFp7cFNtxlnEqcEr6H_ZHL1zWp2mK1b6rPfGIJvAv5UX7PbGYSquQ1za_xmudFb5Eck1oBBBwb9GGyTG8OMc0C5_UnVXdq4TdNBG-obUXckTCSjQCxwkSVjNAVSUnmsjk4eRWNfnCtW1LdzU8m7NHilM3EXLMyo1VLMx3vursZ08oP_tbqDUVjqx3_zu7IKYuA74HBQTP3tg-bC7mYdlaLx2vPA5l-aqunZHxtjBrA30lT3EgoTvsPn9sTzSjlTXAo8CX0EpfjKBKs93RJt9O0iTC-Vy0oRqOkBeH9JWWlGdS37W5NcNHV8mQdsFPekfzOqYNi53sdHb040JsiENCQ_YSz6a5vMg8iSeZvcbuBpn_npwmNFQjpponn4PtShGrdq0fMRxLH_p-MaUICS4Y-DfGJaUTBaNCaucuWV1WejH3zq3zrPoqaqMIPBUUPICThK2lKajLbyUoviq-T-njwYbFtU40c1TFwY3mD2xDdwNMgY400mbV73PkHHiafyE84jxrwWZH_tWXhgzuuVFTn1Md2Hz9OlxN2GCqqNj2LnuR4sk-xa9u3gR0Ce14CFG5LFAr75fEhRw0HaJJI3y-F9nG6n5DUB3JvcFM2X-Jcyi5O30nQ1rmUE-eYV0QamxBM3b-qtBADQpR6G_nHNzvP3DmCS3aD-9xJXceM7b230RZdNf6dCVK6gXgRMEp-V1RCvBeuxBocFCVIZm0q-Y1f1ozBGxGbioM5pUEdKFLgW-PgAWpdeM62odiBv4WvMoIsAKPcmla-dJ3Ckq3NyV1jN7bFyfAtlch2lIcssB8SoBbPlYTXAtdRXf2dM6F23hCV4rrC-OA6D8gIpS6xnG5FmbVXvURjjifCllv__T-B5kqw2VgPTe5fnQzsvbBV3ro3CEhqR05f4irAA25sEgciHcTd6sgH6uw42DSvfIGzsoBNilI9LAnrkhf5NTXg5tVndNY6W-2xSlqRsd9_LEqTY4OgBrGZRsnJRet9MbJHkXHbWu4h3lYu-w0zQj1lhAXvfOyVKUCG5lEEs1i7Sx70pY64sGq9ODe7y6c0paur6HzpKoiLt3V43GD-Tf1l-4AkdiNclJkZB2zj_RjJwPFRdM73qnHxRBDPuCfBjjzqweex19JXqf6gSmgivEWK4PU6WfANdgb0EpBRaE2JYqOt04YcYVkb21HAqFuQD4WAAl73_L2lKmDRcGr2_L8TdpLuSaxDG3MuZ-OVNavvj2.CvM9seoW1LF0-RQ0oMrC01KaIVhQTuehtRGV918UcGA",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "offline_access",
    "refresh_token": "eyJhbGciOiJSU0EtT0FFUCIsImVuYyI6IkEyNTZDQkMtSFM1MTIiLCJraWQiOiJCNUE2NzhCNTRFMEIxRUJEMTI4MzMwOEYwRjRCMEY4Q0JCMzFGMjQ4IiwidHlwIjoib2lfcmVmdCtqd3QiLCJjdHkiOiJKV1QifQ.EgV-ZJMIj1bQIowzoKVIQrKCRpNb_JjftEaddqQPZ4aFbY3wF1p0Tj0yTsapbo7T2W0oVKTerknNpHLTIaAmb1dwH-_ovk_BxIdtH6ZXD4GVshSOpXzTQRCsWuX7bRDYV5Ta-mcX716ReACjV_FfGeCnntU3k9zs3pUR4ZykACrHdJRRv8WG93BzUIwFjVSftl0SFMNMb9CSDg-m7mOab_Z3afYyzrufr0k6GVsgp-kf2mxSZRVclByN3ILVEaoMySypmMMJexzDy381iKLgrx-vyebusKLGoanzT92RM7w-lEyXMlXtVVlA0EuoHAuKe0ltdB5wH9OIOQuH_jwDCg.t7pA-4B9rMeeT3J7SLRaqw.PdWFznPn_IrcTE4lIJ7IzySCg4LValKwVMC_0Lwq4IpK6FE7nRxocGZgJ_ZqBNaqTyxW34iVndbtNXjeVJK7-K4R6i40AyNRbsz75a5x6J2ChGC4RTtfAQ6ZTkUix9sGzwBfeY_BOzs0kkTRly09n8Ua6SkZSlvHBxmU0A7jUB-EpICUu_-09uG7yRtDnGKdHkp6J1amh84kYkHYDlKbfUjvP9jlQWx0wCJCLoXtMOpuhN7q5w2MF0fGGwJgOsJ7FljC6qegF-0lM8KVV7XjdQgH35wiOd7_8aPz-ijWinI1EPyq8o5n_Z3cQb0HhQzrCvIIX2p8lDdMiQzzCo7XuQntIU228pwlvUxhGmPOh1vXM0x5exAey6FOqdDq6z7Xb4yo0H1mm3R8f9iWqIk8XGwYaGcUUD1I9h7Lqfty2E5EtdIrATm7KOfOjoQa3cswa7Ih1R-YTDdTGQ95inTgObMEq8AI9_3koLPffl-9XpD-uatAYNrW-lpCpMQJCY00-nzuTrVQ7xHSijHtQxPdenJNBRPfksBNPUaSujVMQGP3kEFrVZ0XCmBk0ah-EunSPa3fDimPJqdUCLff_2RK_ZJ15VBj5z7VsdnWotR02Tmbd0F6BIe0kZfOlBllkPVYKjTn4hJv9lPOh2aWINYJOcRqmy3E8TwEeABeYKkFnwmRa27rJABDj7nUKYWdCdmnJAhxo2snIUaN6TbvPuA-5ku5UQ7IJYta9YCMAQs2NN070xwBhsq8jdois8a_PdlhNHZGSGg2qfdVDGvCpphqdoqOPxGF7MOXssjY7kWzeaq-T8SwEo3NFg3UasmdZhpj4NQnCIxUwRdOHD8DyBBex2jC4GnTVjXGt9UnICC-3mlUd3Bt5vSEPGWJ_Ez60vW8yhkpST7oA_IvjB6nNzOKvlF7Aad6M3oW3lJc1wL7p1qI7nf2PedM0jnTUjPDigbFq1qdsX_WJ_OTB34382R6kpw6d89yQNgDzfJhjmouC_g4NWDorjourzZhLWw0MhBdS4KganwaJzckGUgnX9zAonbtpYV1Yb6dWlTbxBbn_Qta_q3mVkma8nsHHYZBBS3ekxuWcH3JJO33_NzUt_HsN-GX_2bvqHwEN7pK4qvZi2DcKWyfrrFXDzWrv9qr37plhwzDGBXTuPLe6ORE9Ibro6t6z2Nfl9r-nvhLxBxTsK_08g4all57maGMAkfb4XvEPTizKVFockKTLub0HWJGEcbMjHNYSyuFPvAiUmEXrwo.Rue3ruRy_9eQd-_zBH90v-__feebIi8apYbaEMDOQVs"
}
```

## Validate Authentication
A request can be sent to validate that authentication is working correctly.

### Endpoint
GET to https://api.typsy.com/v2/authenticate

### Request
Send an empty request with an Authorization header
```
Header : Authorization
Value : Bearer eyJhbGciOiJSU0EtT0FFUCIsImVuYyI6IkEyNTZDQkMtSFM1MTIiLCJraWQiOiJCNUE2NzhCNTRFMEIxRUJEMTI4MzMwOEYwRjRCMEY4Q0JCMzFGMjQ4IiwidHlwIjoiYXQrand0IiwiY3R5IjoiSldUIn0.BbU-954CEdwi01dY2IPO1jVkc2WSOlueIYa_VTQkZuXwcvLbZ-KCQxuuciJV2vG3tJj97sRB_n40TUogJY-32KcQrlU_JUcQU6m6UvpQkCad19lLg_0kefakH9NrnGcBi1s7T9Stl4Z3hbu_JYj26h2ELliIR2t4LWXC0D6SY_RgZwbDCnSi4qN1ByaoVGHa-8O6EZMdc1Dpopr3UI2wVFlA4BZOmbsIgQ1xcmjENrKAIHQe-45DeQkz8HdZTNnxdWh_FyYNCi_OAMYqJvoSOhqJSH5_FPL0x2yFyBNnAGwlkAI4yrvnr6oGPJa5QoUGA0UwZCd8uMgotpktvMrPeA.D3Ehq0i6MiNl7TNZtSPoaA.1Xzw7kjkkExw2qro31BMK3o_nSk5V1sz73Qlcs8SksbLucQBKkArBiPTgHky4MHvFv7n81YaXRMb7cPrp5reZYcQLO2CFvj8Qz76m4fn4GxbgFp7cFNtxlnEqcEr6H_ZHL1zWp2mK1b6rPfGIJvAv5UX7PbGYSquQ1za_xmudFb5Eck1oBBBwb9GGyTG8OMc0C5_UnVXdq4TdNBG-obUXckTCSjQCxwkSVjNAVSUnmsjk4eRWNfnCtW1LdzU8m7NHilM3EXLMyo1VLMx3vursZ08oP_tbqDUVjqx3_zu7IKYuA74HBQTP3tg-bC7mYdlaLx2vPA5l-aqunZHxtjBrA30lT3EgoTvsPn9sTzSjlTXAo8CX0EpfjKBKs93RJt9O0iTC-Vy0oRqOkBeH9JWWlGdS37W5NcNHV8mQdsFPekfzOqYNi53sdHb040JsiENCQ_YSz6a5vMg8iSeZvcbuBpn_npwmNFQjpponn4PtShGrdq0fMRxLH_p-MaUICS4Y-DfGJaUTBaNCaucuWV1WejH3zq3zrPoqaqMIPBUUPICThK2lKajLbyUoviq-T-njwYbFtU40c1TFwY3mD2xDdwNMgY400mbV73PkHHiafyE84jxrwWZH_tWXhgzuuVFTn1Md2Hz9OlxN2GCqqNj2LnuR4sk-xa9u3gR0Ce14CFG5LFAr75fEhRw0HaJJI3y-F9nG6n5DUB3JvcFM2X-Jcyi5O30nQ1rmUE-eYV0QamxBM3b-qtBADQpR6G_nHNzvP3DmCS3aD-9xJXceM7b230RZdNf6dCVK6gXgRMEp-V1RCvBeuxBocFCVIZm0q-Y1f1ozBGxGbioM5pUEdKFLgW-PgAWpdeM62odiBv4WvMoIsAKPcmla-dJ3Ckq3NyV1jN7bFyfAtlch2lIcssB8SoBbPlYTXAtdRXf2dM6F23hCV4rrC-OA6D8gIpS6xnG5FmbVXvURjjifCllv__T-B5kqw2VgPTe5fnQzsvbBV3ro3CEhqR05f4irAA25sEgciHcTd6sgH6uw42DSvfIGzsoBNilI9LAnrkhf5NTXg5tVndNY6W-2xSlqRsd9_LEqTY4OgBrGZRsnJRet9MbJHkXHbWu4h3lYu-w0zQj1lhAXvfOyVKUCG5lEEs1i7Sx70pY64sGq9ODe7y6c0paur6HzpKoiLt3V43GD-Tf1l-4AkdiNclJkZB2zj_RjJwPFRdM73qnHxRBDPuCfBjjzqweex19JXqf6gSmgivEWK4PU6WfANdgb0EpBRaE2JYqOt04YcYVkb21HAqFuQD4WAAl73_L2lKmDRcGr2_L8TdpLuSaxDG3MuZ-OVNavvj2.CvM9seoW1LF0-RQ0oMrC01KaIVhQTuehtRGV918UcGA
```

### Response
If authentication has been successful you will be returned a 200 status code.  If you receive a 40x status code then investigate if all the required parameters for authentication have been constructed correctly and provided in the request.

# Users

If you're a master account you will need to add this header to your requests
- Typsy-Account-Code : The internal code your company uses to identify its properties, needed to identify which child account the user belongs to.

If there is an issue with locating the child account matching the code you provided, you will receive a 400 Bad Request response.

## User create

### Endpoint
POST to https://api.typsy.com/v2/users/workspace/create

### Request
Required
- firstName: The first name of the user
- lastName: The last name of the user
- email: The email of the user
- structures: The collection of structures (venues/departments/groups) you wish to add the user to
    - name: the name of the structure
    - role: the role for the member within the structure. Possible values: member, manager

Required for SSO connected accounts
- ssoUserIdentifier: Used for adding the user identifier for SSO login.

Optional
- teams: The collection of teams you wish to add the user to
    - name: the name of the team
- claims: A collection of claims you wish to add the user to
    - key: the name of your external id
    - value: the value of your external id
    - issuer: who issued the claim (often just your overall account name)

- options:
    - sendInvitation: sends an invitation to the user to claim their account. If your account is set up with SSO this must be set to false or the API will return an error. Default = false
    - createStructuresIfNotExist: creates the structure within the account if it does not already exist. Default = true
    - createTeamsIfNotExist: creates the team within the account if it does not already exist. Default = true
    - reactivateIfDeparted: if the user was previously departed from this account it reactivates them within the account if set to true. If set to false, it will give you an error saying that the user was departed from this account. Default = false

Example request to create a user (minimum information).  
```
{
    "firstName": "FirstName",
    "lastName": "LastName",
    "email": "first.last@domain.com",
    "structures": [
        {
            "name": "Venue A",
            "role": "member"
        }
    ],
    "options": {
        "sendInvitation": false,
        "createStructuresIfNotExist": true,
        "reactivateIfDeparted": false
    }
}
```
Example request to create a user (additional information).  
```
{
    "firstName": "FirstName",
    "lastName": "LastName",
    "email": "first.last@domain.com",
    "structures": [
        {
            "name": "Venue A",
            "role": "member"
        },
        {
            "name": "Venue B",
            "role": "manager"
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
            "value": "12345678910",
            "issuer": "IssuerName"
        }
    ],
    "ssoUserIdentifier": "123456",
    "options": {
        "sendInvitation": false,
        "createStructuresIfNotExist": true,
        "createTeamsIfNotExist": true,
        "reactivateIfDeparted": false
    }
}
```  

### Response
Example response where create a user request has been successful. The documentation on what do with the requestId is [here](#request-status)
```
{
    "requestId": "a2e553c0-c963-4bdd-87de-1805122740e6",
    "status": "in progress",
    "errors": [],
    "success": true
    "statusUrl": "https://api.typsy.com/v2/users/request-status/a2e553c0-c963-4bdd-87de-1805122740e6"
}
```


#### Bad Request
Example response where the user create request failed validation.  A 400 Bad Request status code will be returned.

```
{
    "requestId": "",
    "status": "failed",
    "success": false,
    "errors": [
        {
            "code": "NotNullValidator",
            "description": "last name cannot be null."
        },
        {
            "code": "NotEmptyValidator",
            "description": "last name cannot be empty."
        }
    ]
}
```

## User depart

### Endpoint
POST to https://api.typsy.com/v2/users/workspace/depart

### Request
Required
- email: The email of the user

Optional
- options:
    - sendFarewellEmail: sends a farewell email after a period of time to the user after they have been departed, letting them know what has happened to their account and learning history. Default = false
  
Example request to depart a user by email.  
```
{
    "email": first.last@domain.com,
    "options": {
        "sendFarewellEmail": false
    }
}
```

### Response
Example response where depart a user request has been successful. The documentation on what do with the requestId is [here](#request-status)
```
{
    "requestId": "f1c8c78c-78f0-4b50-af09-df0a14dc3759",
    "status": "in progress",
    "errors": [],
    "success": true
    "statusUrl": "https://api.typsy.com/v2/users/request-status/f1c8c78c-78f0-4b50-af09-df0a14dc3759"
}
```

## User update

### Endpoint
PUT to https://api.typsy.com/v2/users/workspace/update

### Request
Required
- identifier: The Typsy identifier for the user

Optional
- firstName: The first name of the user
- lastName: The last name of the user
- email: The email of the user
- ssoUserIdentifier: Used for adding the user identifier for SSO login.


Example request to update a user by identifier.  
```
{
    "identifier": "470fa307710b4c1584fed51e875f050f"
    "firstName": "FirstName",
    "lastName": "LastName",
    "email": "first.last@domain.com",
    "ssoUserIdentifier": "123456"
}
```

### Response
Example response where create a user request has been successful. The documentation on what do with the requestId is [here](#request-status)
```
{
    "requestId": "21752ab0-83ee-4997-9bc9-4870a4fc2884",
    "status": "in progress",
    "errors": [],
    "success": true
    "statusUrl": "https://api.typsy.com/v2/users/request-status/21752ab0-83ee-4997-9bc9-4870a4fc2884"
}
```

## User add teams

### Endpoint
POST to https://api.typsy.com/v2/users/workspace/teams/add

### Request
Required
- email: The email of the user
- teams: The collection of teams you wish to add the user to

Optional
- options:
    - createTeamsIfNotExist: creates the team within the account if it does not already exist. Default = true

Example request to add teams to a user by email. 
```
{
    "email": "first.last@domain.com",
    "teams": [
        {
            "name": "Team A"
        }
    ],
    "options": {
        "createTeamsIfNotExist": true,
    }
}
```

### Response
Example response where add teams to a user request has been successful. The documentation on what do with the requestId is [here](#request-status)
```
{
    "requestId": "1135fd80-ac65-41b9-8db5-f7c2f379e9ab",
    "status": "in progress",
    "errors": [],
    "success": true
    "statusUrl": "https://api.typsy.com/v2/users/request-status/1135fd80-ac65-41b9-8db5-f7c2f379e9ab"
}
```
## User remove teams

### Endpoint
POST to https://api.typsy.com/v2/users/workspace/teams/remove

### Request
Required
- email: The email of the user
- teams: The collection of teams you wish to remove the user from

Optional
- options:
    - continueIfNotInTeam: If the user is not in a team which they were requested to be removed from, the process will continue. If set to false, it will return an error telling you they are not in the team. Default = true

Example request to remove teams from a user by email. 
```
{
    "email": "first.last@domain.com",
    "teams": [
        {
            "name": "Team A"
        }
    ],
    "options": {
        "continueIfNotInTeam": true,
    }
}
```

### Response
Example response where remove teams from a user request has been successful. The documentation on what do with the requestId is [here](#request-status)
```
{
    "requestId": "cf74d64e-bf7b-4b35-bee9-427c16ca051b",
    "status": "in progress",
    "errors": [],
    "success": true
    "statusUrl": "https://api.typsy.com/v2/users/request-status/cf74d64e-bf7b-4b35-bee9-427c16ca051b"
}
```
## User add structures

### Endpoint
POST to https://api.typsy.com/v2/users/workspace/structures/add

### Request
Required
- email: The email of the user
- structures: The collection of structures (venues/departments/groups) you wish to add the user to

Optional
- options:
    - createStructuresIfNotExist: creates the structure within the account if it does not already exist. Default = true

Example request to add structures to a user by email.  
```
{
    "email": "first.last@domain.com",
    "structures": [
        {
            "name": "Venue A",
            "role": "member"
        }
    ],
    "options": {
        "createStructuresIfNotExist": true,
    }
}
```

### Response
Example response where add structures to a user request has been successful. The documentation on what do with the requestId is [here](#request-status)
```
{
    "requestId": "8bd1e102-95d1-4965-a9c3-a73a5fc88101",
    "status": "in progress",
    "errors": [],
    "success": true
    "statusUrl": "https://api.typsy.com/v2/users/request-status/8bd1e102-95d1-4965-a9c3-a73a5fc88101"
}
```
## User remove structures

### Endpoint
POST to https://api.typsy.com/v2/users/workspace/structures/remove

### Request
Required
- email: The email of the user
- structures: The collection of structures (venues/departments/groups) you wish to remove the user from

Optional
- options:
    - continueIfNotInStructure: If the user is not in a structure which they were requested to be removed from, the process will continue. If set to false, it will return an error telling you they are not in the structure. Default = true

Example request to remove structures from a user by email. 
```
{
    "email": "first.last@domain.com",
    "structures": [
        {
            "name": "Venue A",
        }
    ],
    "options": {
        "continueIfNotInStructure": true,
    }
}
```

### Response
Example response where remove structures from a user request has been successful. The documentation on what do with the requestId is [here](#request-status)
```
{
    "requestId": "3b332916-62d8-4a95-a6c7-f83217f3e2ed",
    "status": "in progress",
    "errors": [],
    "success": true
    "statusUrl": "https://api.typsy.com/v2/users/request-status/3b332916-62d8-4a95-a6c7-f83217f3e2ed"
}
```
## User add claims

### Endpoint
POST to https://api.typsy.com/v2/users/workspace/claims/add

### Request
Required
- email: The email of the user
- claims: A collection of claims you wish to add the user to
    - key: the name of your external id
    - value: the value of your external id
    - issuer: who issued the claim (often just your overall account name)

Example request to add claims to a user by email. 
```
{
    "email": "first.last@domain.com",
    "claims": [
        {
            "key": "external_id",
            "value": "12345678910",
            "issuer": "IssuerName"
        }
    ]
}
```

### Response
Example response where add claims to a user request has been successful. The documentation on what do with the requestId is [here](#request-status)
```
{
    "requestId": "e20f2b42-cfdc-434f-a616-710088da4e00",
    "status": "in progress",
    "errors": [],
    "success": true
    "statusUrl": "https://api.typsy.com/v2/users/request-status/e20f2b42-cfdc-434f-a616-710088da4e00"
}
```

## User remove claims

### Endpoint
POST to https://api.typsy.com/v2/users/workspace/claims/remove

### Request
Required
- email: The email of the user
- claims: A collection of claims you wish to remove the user from
    - key: the name of your external id
    - issuer: who issued the claim (often just your overall account name)

Example request to remove claims from a user by email. 
```
{
    "email": "first.last@domain.com",
    "claims": [
        {
            "key": "external_id",
            "issuer": "IssuerName"
        }
    ]
}
```

### Response
Example response where remove claims from a user request has been successful. The documentation on what do with the requestId is [here](#request-status)
```
{
    "requestId": "580db06c-93ea-4c67-9d05-750530180c6c",
    "status": "in progress",
    "errors": [],
    "success": true
    "statusUrl": "https://api.typsy.com/v2/users/request-status/580db06c-93ea-4c67-9d05-750530180c6c"
}
```

## Request Status

### Endpoint
GET to https://api.typsy.com/v2/users/request-status/{requestId}

#### Request not processed yet
If the initial request has not yet been processed you will receive a [204 No Content](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/204) result.  Wait a minute and make another request.

#### Request processed successfully
Example response where the user create request has been successful.
```
{
    "requestId": "a2e553c0-c963-4bdd-87de-1805122740e6",
    "status": "success",
    "errors": [],
    "success": true
}
```

#### Request processed with errors
Example response where the user create request has failed.
```
{
    "requestId": "a2e553c0-c963-4bdd-87de-1805122740e6",
    "status": "failed",
    "errors": [
        {
            "code": "user_already_exists",
            "description": "A user with the email EMAIL already exists within your account."
        }
    ],
    "success": false
}
```

## List Users

### Endpoint
GET to https://api.typsy.com/v2/users?offset=0&limit=25

### Request
Optional
 - offset: How many records to skip. This is used to page through records. Default = 0
 - limit: Amount of records to return for the request. Minimum value is 1 and Maximum is 25. This value is clamped on the server side. Default = 1

### Response
- users: A collection of user summary objects

User Summary
    - identifer: The typsy identifier for the user object
    - name: The full name of the user
    - firstName: The first name of the user
    - lastName: The last name of the user
    - email: The email of the user
    - ssoUserIdentifier: The user identifier used for SSO login
        Workspace
        - identifer: The typsy identifier for the workspace object
        - status: The current status of the user within the account (licensed or departed)
        - structureCount: Count of structures the workspace is active in
        - teamCount: Count of teams the workspace is active in
        - claimsCount: Count of claims the workspace has attached
- metadata:
    - total - total amount of users within your master account
    - count - how many users were returned
    - limit - how many users were requested
    - offset - how many users were skipped
```
{
    "users": [
    {
        "identifier": "f12d3f0fa6b94c5fa9ce2934fefa0cc3"
        "name": "FirstName LastName",
        "firstName": "FirstName",
        "lastName": "LastName",
        "email": "first.last@domain.com",
        "ssoUserIdentifier": "123456",
        "workspace": {
            "identifier": "11844d3c366948f1b14ce3654a7795b2",
            "status": "Licensed",
            "structureCount": 2,
            "teamCount": 2,
            "claimsCount": 1
        }
    }
    ],
    "metadata": {
    "total": 3,
        "count": 1,
        "limit": 1,
        "offset": 0
    }
}
```

## Get User

### Endpoint
POST to https://api.typsy.com/v2/users/workspace

### Request
Required:
 - email: The email provided in the create user step (or)
 - ssoUserIdentifier : The user identifier used for SSO login

 Example request to get userby email. 
```
{
    "email": "first.last@domain.com"
}
```

 Example request to get userby ssoUserIdentifier. 
```
{
    "ssoUserIdentifier": "123456"
}
```

### Response
Returns an UserDetailed object.

```
{
    "identifier": "f12d3f0fa6b94c5fa9ce2934fefa0cc3",
    "name": "FirstName LastName",
    "firstName": "FirstName",
    "lastName": "LastName",
    "email": "first.last@domain.com",
    "ssoUserIdentifier": "123456",
    "workspace": {
    "identifier": "11844d3c366948f1b14ce3654a7795b2",
    "status": "Licensed",
    "structures": [
        {
            "name": "Venue A",
            "role": "member"
        },
        {
            "name": "Venue B",
            "role": "manager"
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
            "issuer": "IssuerName"
        }
        ]
    }
}
```

#### No user found

A 204 No Content response will be returned if no user matching the email can be found within the account.

# Accounts

## Account create
Used to create child accounts with in a parent account

### Endpoint
POST to https://api.typsy.com/v2/accounts/create

### Request
Required
 - name: Name of your property
 - vanityName: The name of the property that the Users will see
 - tzIdentifier: The timezone which the property operates in (https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)
 - country: 2 letter country code the property resides in (https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes)
 - code: The internal code your company uses to identify its properties, needed to identify which child account Users will be created in when using the User API

 Optional
 - region: The region which the property resides in
 - structures: Used for creating structures (venues/departments/groups) within your account to sort your Users into 
 - teams: Used for creating teams within your account to sort your Users into

```
{
  "name": "My Account Pty Ltd",
  "vanityName": "My Account",
  "tzIdentifier": "Australia/Melbourne",
  "country": "AU",
  "code": "MEL_HOTEL1",
  "region": "APAC",
  "structures": [
    {
      "name": "Hotel Restaurant"
    },
    {
      "name": "Hotel Bar"
    }
  ],
  "teams": [
    {
      "name": "Dishwashers"
    },
    {
      "name": "Bartenders"
    }
  ]
}
```


### Response

Example response where the Account create request has been successful. The documentation on what do with the requestId is [here](#request-status-1)

```
{
    "requestId": "23365f4b-7ae8-4d4d-bb74-ad8b4bfee647",
    "status": "in progress",
    "errors": [],
    "success": true
    "statusUrl": "https://api.typsy.com/v2/accounts/request-status/23365f4b-7ae8-4d4d-bb74-ad8b4bfee647"
}
```


#### Bad Request
Example response where the account create request failed validation.

```
{
    "requestId": "",
    "status": "failed",
    "success": false,
    "errors": [
        {
            "code": "NotNullValidator",
            "description": "vanityName cannot be null."
        },
        {
            "code": "NotEmptyValidator",
            "description": "vanityName cannot be empty."
        }
    ]
}
```

## Request Status

### Endpoint
GET to https://api.typsy.com/v2/accounts/request-status/{requestId}

#### Request not processed yet
If the initial request has not yet been processed you will receive a [204 No Content](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/204) result.  Wait a minute and make another request.

#### Request processed successfully
Example response where the account create request has been successful. The documentation on what do with the requestId is [here](#request-status-1)

```
{
    "requestId": "23365f4b-7ae8-4d4d-bb74-ad8b4bfee647",
    "status": "success",
    "errors": [],
    "success": true
}
```


#### Request processed with errors
Example response where the user create request has been accepted but has failed processing.  This is typically because a business rule has failed.

```
{
    "workspaceId": null,
    "requestId": "23365f4b-7ae8-4d4d-bb74-ad8b4bfee647",
    "status": "failed",
    "errors": [
        {
            "code": "account_already_exists",
            "description": "An account with the corporationId CORPORATION_ID and code MY_CODE already exists"
        }
    ],
    "success": false
}
```

## Account role add 
Used to add role to a user with in a child account

If you're a master account you will need to add this header to your requests
- Typsy-Account-Code : The internal code your company uses to identify its properties, needed to identify which child account the user belongs.

### Endpoint
POST to https://api.typsy.com/v2/accounts/roles/add

### Request
Required
 - email: The email of the user
 - role: The role user needs to be added to. Possible values: administrator
```
{
    "email": "first.last@domain.com",
    "role": "administrator"
}
```
### Response

Example response where the Account create request has been successful. The documentation on what do with the requestId is [here](#request-status-1)

```
{
    "requestId": "660c5f82-7bb0-4fa2-a6fa-0cabf7cd62b3",
    "status": "in progress",
    "errors": [],
    "success": true
    "statusUrl": "https://api.typsy.com/v2/accounts/request-status/660c5f82-7bb0-4fa2-a6fa-0cabf7cd62b3"
}
```

## Account role remove 
Used to remove role from a user with in a child account

If you're a master account you will need to add this header to your requests
- Typsy-Account-Code : The internal code your company uses to identify its properties, needed to identify which child account the user belongs.

### Endpoint
POST to https://api.typsy.com/v2/accounts/roles/remove

### Request
Required
 - email: The email of the user
 - role: The role user needs to be removed from. Possible values: administrator
```
{
    "email": "first.last@domain.com",
    "role": "administrator"
}
```
### Response

Example response where the Account create request has been successful. The documentation on what do with the requestId is [here](#request-status-1)

```
{
    "requestId": "b0116927-bebb-4f88-8e4f-f9f729f5027c",
    "status": "in progress",
    "errors": [],
    "success": true
    "statusUrl": "https://api.typsy.com/v2/accounts/request-status/b0116927-bebb-4f88-8e4f-f9f729f5027c"
}
```

## List Accounts

### Endpoint
GET to https://api.typsy.com/v2/accounts?offset=0&limit=25

### Request
Optional
 - offset: How many records to skip. This is used to page through records. Default = 0
 - limit: Amount of records to return for the request. Minimum value is 1 and Maximum is 25. This value is clamped on the server side. Default = 1

### Response
- accounts: A collection of AccountSummary objects
- corporationId: The identifier which is shared between all of your master and child accounts 
- metadata:
    - total - total amount of accounts within your master account
    - count - how many accounts were returned
    - limit - how many accounts were requested
    - offset - how many accounts were skipped
```
{
    "accounts": [
        {
          "identifier": "1f2d3f0aa6b94cb5a9ce2934fefa0cc3",
          "code": "MEL_HOTEL1",
          "name": "My Account Pty Ltd",
          "vanityName": "My Account",
          "tzIdentifier": "Australia/Melbourne",
          "country": "AU",
          "region": "APAC",
          "structureCount": 2,
          "teamCount": 2
        }
    ],
    "corporationId": "test_corporation",
    "metadata": {
        "total": 13,
        "count": 1,
        "limit": 1,
        "offset": 0
    }
}
```

## Get Account

### Endpoint
GET to https://api.typsy.com/v2/accounts/{code}

### Request
Required
 - code: The code provided in the create account step

### Response
Returns an AccountSummaryDetailed object.

```
{
  "identifier": "1f2d3f0aa6b94cb5a9ce2934fefa0cc3",
  "code": "MEL_HOTEL1",
  "name": "My Account Pty Ltd",
  "vanityName": "My Account",
  "tzIdentifier": "Australia/Melbourne",
  "country": "AU",
  "region": "APAC",
  "structures": [
    {
      "identifier": "4f3ee0a5a6d649a1be0e5bb523c21451",
      "name": "Hotel Restaurant"
    },
    {
      "identifier": "42ecb8e2fec7402ea4941db661313950",
      "name": "Hotel Bar"
    }
  ],
  "teams": [
    {
      "identifier": "ea73a0ace3bd479697704cbbd61a9a97",
      "name": "Dishwashers"
    },
    {
      "identifier": "631fec56ce1e425ca80045a60911cf12",
      "name": "Bartenders"
    }
  ]
}
```

#### No account found

A 204 No Content response will be returned if no account matching the code can be found within the requesting master account.
