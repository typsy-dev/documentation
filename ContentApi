<base target="_blank">

# API V2
Typsy provides an API for basic operations on Users and Accounts.

## Actions
The supported actions are:

Authenticate
1. [Test Authentication with the API](#authentication)

Course API
1. [Get Courses list (get list of courses)](#list-courses)
2. [Get a Course (get a course)](#get-course)

Lesson API
1. [Get Lessons list (get list of lessons)](#list-lessons)
2. [Get a lesson (get a lesson)](#get-lesson)

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


## List Courses

### Endpoint
GET to https://api.typsy.com/v2/courses?offset=0&limit=25

### Request
Optional
 - offset: How many records to skip. This is used to page through records. Default = 0
 - limit: Amount of records to return for the request. Minimum value is 1 and Maximum is 25. This value is clamped on the server side. Default = 1

### Response
- courses: A collection of course summary objects

Course Summary
    - identifier: The Typsy identifier for the course object
    - name: The full name of the course
	- issuer: The issuer for the course
    - category: The category of the course
    - instructor: The instructor of the course
    - description: The description of the course
    - lessonCount: The count of lessons in the course
    - image: The image of the course
    - created: The created date of the course
    - updated: The updated date of the course
    - lengthSeconds: The total length in seconds of the course

- metadata:
    - total - total count of courses
    - count - how many courses were returned
    - limit - how many courses were requested
    - offset - how many courses were skipped
```
{
    "courses": [
        {
            "identifier": "c6286b1987df4472bc07d4d3ee9c1a8b",
            "name": "Mise en place",
            "issuer": "Typsy",
            "category": "Culinary",
            "instructor": "Alastair McLeod",
            "description": "It may look and sound strange but mise en place is anything but. This old French culinary term translates as 'everything in its place', meaning no messy workstations and no stress over missing ingredients. We couldn't think of anything worse than being halfway through service and realizing that o...",
            "lessonCount": 6,
            "image": "https://images-staging.typsy.com/get/issuers/694081e89df44c39bccb4dabea9568a4/courses/c6286b1987df4472bc07d4d3ee9c1a8b.png?lastMod=638635393196490434",
            "created": "2020-09-04T04:57:54.443",
            "updated": "2024-10-03T08:01:59.6490434",
            "lengthSeconds": 1203
        }
    ],
    "success": true,
    "errors": [],
    "metadata": {
        "total": 175,
        "count": 1,
        "limit": 1,
        "offset": 0
    }
}
```

## Get Course

### Endpoint
POST to https://api.typsy.com/v2/courses/{identifier}


### Response
Returns an Course object.

```
{
    "course": {
        "identifier": "c6286b1987df4472bc07d4d3ee9c1a8b",
        "name": "Mise en place",
        "issuer": {
            "identifier": "694081e89df44c39bccb4dabea9568a4",
            "name": "Typsy"
        },
        "category": {
            "identifier": "1e7d14d80a334718af5251161e3920b2",
            "name": "Culinary"
        },
        "instructor": {
            "identifier": "d52887513b544d0197e0c8ddb7be3384",
            "name": "Alastair McLeod"
        },
        "description": "It may look and sound strange but mise en place is anything but. This old French culinary term translates as 'everything in its place', meaning no messy workstations and no stress over missing ingredients. We couldn't think of anything worse than being halfway through service and realizing that o...",
        "lessons": [
            {
                "identifier": "0b559ea7beae4ab49531070bdfad6488",
                "name": "What is Mise en Place and why is it important?",
                "issuer": "Typsy",
                "category": "Culinary",
                "instructor": "Alastair McLeod",
                "description": "Pronounced 'meez-ahn-plahs', this French culinary term means having your workstation organized and ready to go before service starts. Anything from ingredients, to utensils and plates, will be arranged so you can find what you need when you need it without suffering from a kitchen meltdown. Exper...",
                "image": "https://images-staging.typsy.com/get/issuers/694081e89df44c39bccb4dabea9568a4/lessons/0b559ea7beae4ab49531070bdfad6488.png?lastMod=637791944657188687",
                "created": "2018-05-17T19:00:00",
                "updated": "2022-01-31T02:54:25.7188687",
                "lengthSeconds": 201
            },
            {
                "identifier": "a84aeeb074b24e71aac38a89b155e0f1",
                "name": "How to write a mise en place plan",
                "issuer": "Typsy",
                "category": "Culinary",
                "instructor": "Alastair McLeod",
                "description": "When service starts things tend to move quickly, so you don't want to jump straight in and see things fall apart before they even start. That's why having a mise en place plan is important. The whole point of mise en place is having everything prepared before service starts. Having a plan in plac...",
                "image": "https://images-staging.typsy.com/get/issuers/694081e89df44c39bccb4dabea9568a4/lessons/a84aeeb074b24e71aac38a89b155e0f1.png?lastMod=637932980579661297",
                "created": "2018-05-17T19:00:00",
                "updated": "2022-07-13T08:34:17.9661297",
                "lengthSeconds": 190
            },
            {
                "identifier": "ffc11a9915d9440884532e0fd3495d3b",
                "name": "How to keep your workplace tidy during mise en place",
                "issuer": "Typsy",
                "category": "Culinary",
                "instructor": "Alastair McLeod",
                "description": "A cluttered workstation will mean a messy service that could end in disaster. That's something we are sure you want to avoid! Even though cleaning your workplace will seem like a chore the benefits of keeping your area tidy are endless. An organized work area means you can avoid things such as cr...",
                "image": "https://images-staging.typsy.com/get/issuers/694081e89df44c39bccb4dabea9568a4/lessons/ffc11a9915d9440884532e0fd3495d3b.png?lastMod=637791944133519539",
                "created": "2018-05-17T19:00:00",
                "updated": "2022-01-31T02:53:33.3519539",
                "lengthSeconds": 168
            },
            {
                "identifier": "451536e67e91412dbf72503cb01068b7",
                "name": "How to work effectively during mise en place",
                "issuer": "Typsy",
                "category": "Culinary",
                "instructor": "Alastair McLeod",
                "description": "So, you've got your task list ready to go but what comes next? First things first, get out everything you need so that you don't need to rush and get it later. Whether it's a spatula or a pinch of cumin, get it ready on your workstation so it's there for when service starts. Have a recipe which i...",
                "image": "https://images-staging.typsy.com/get/issuers/694081e89df44c39bccb4dabea9568a4/lessons/451536e67e91412dbf72503cb01068b7.png?lastMod=637791943928892981",
                "created": "2018-05-17T19:00:00",
                "updated": "2022-01-31T02:53:12.8892981",
                "lengthSeconds": 254
            },
            {
                "identifier": "cd0cbfc8baa14073ae847f92f0aef62b",
                "name": "How to communicate with your team during mise en place",
                "issuer": "Typsy",
                "category": "Culinary",
                "instructor": "Alastair McLeod",
                "description": "You've got your workstation ready, but have you checked on your team? Service won't run smoothly if everyone else isn't ready. Communicating with your team to see if they need any help can make the difference between having one element on the plate and having every element on the plate. If you've...",
                "image": "https://images-staging.typsy.com/get/issuers/694081e89df44c39bccb4dabea9568a4/lessons/cd0cbfc8baa14073ae847f92f0aef62b.png?lastMod=638439127073502372",
                "created": "2018-05-17T19:00:00",
                "updated": "2024-02-19T04:11:47.3502372",
                "lengthSeconds": 185
            },
            {
                "identifier": "9ab0521624fb489888b58e179ec06a3f",
                "name": "How to organize your station ready for service",
                "issuer": "Typsy",
                "category": "Culinary",
                "instructor": "Alastair McLeod",
                "description": "Everyone is prepped and you're almost ready for the first docket to come into the kitchen. Now you just need to have everything in order. Start by making sure the tools and ingredients you need are ready and set out clearly to avoid confusion when things get busy. Like your knives to be in a spec...",
                "image": "https://images-staging.typsy.com/get/issuers/694081e89df44c39bccb4dabea9568a4/lessons/9ab0521624fb489888b58e179ec06a3f.png?lastMod=637791943581492767",
                "created": "2018-05-17T19:41:10",
                "updated": "2022-01-31T02:52:38.1492767",
                "lengthSeconds": 205
            }
        ],
        "enabled": true,
        "image": "https://images-staging.typsy.com/get/issuers/694081e89df44c39bccb4dabea9568a4/courses/c6286b1987df4472bc07d4d3ee9c1a8b.png?lastMod=638635393196490434",
        "created": "2020-09-04T04:57:54.443",
        "updated": "2024-10-03T08:01:59.6490434",
        "lengthSeconds": 1203
    },
    "success": true,
    "errors": []
}
```

#### No course found

A 404 Not Found response will be returned if no lesson is found.


## List Lessons

### Endpoint
GET to https://api.typsy.com/v2/lessons?offset=0&limit=25

### Request
Optional
 - offset: How many records to skip. This is used to page through records. Default = 0
 - limit: Amount of records to return for the request. Minimum value is 1 and Maximum is 25. This value is clamped on the server side. Default = 1

### Response
- lessons: A collection of lesson summary objects

Lesson Summary
    - identifier: The Typsy identifier for the lesson object
    - name: The full name of the lesson
	- issuer: The issuer for the lesson
    - category: The category of the lesson
    - instructor: The instructor of the lesson
    - description: The description of the lesson
    - image: The image of the lesson
    - created: The created date of the lesson
    - updated: The updated date of the lesson
    - lengthSeconds: The total length in seconds of the lesson

- metadata:
    - total - total count of lessons
    - count - how many lessons were returned
    - limit - how many lessons were requested
    - offset - how many lessons were skipped
```
{
	"identifier": "32a49a1e4a0842de87afa0a10014a163",
	"name": "Conclusion - Sustainable food practices",
	"issuer": "Typsy",
	"category": "Culinary",
	"instructor": "Carlos Henriques",
	"description": "Well done! You've finished the Sustainable food practices course. Ready to test your skills? Complete the quiz and earn your certificate today. This course is ideal for any kitchen employees and staff members wanting to learn more about sustainable food practices....",
	"image": "https://images-staging.typsy.com/get/issuers/694081e89df44c39bccb4dabea9568a4/lessons/32a49a1e4a0842de87afa0a10014a163.png?lastMod=637418169125934973",
	"created": "0001-01-01T00:00:00",
	"updated": "2020-11-24T12:15:12.5934973",
	"lengthSeconds": 74
}
```

## Get Lesson

### Endpoint
POST to https://api.typsy.com/v2/lessons/{identifier}


### Response
Returns an Lesson object.

```
{
    "lesson": {
        "identifier": "32a49a1e4a0842de87afa0a10014a163",
        "name": "Conclusion - Sustainable food practices",
        "issuer": {
            "identifier": "694081e89df44c39bccb4dabea9568a4",
            "name": "Typsy"
        },
        "category": {
            "identifier": "1e7d14d80a334718af5251161e3920b2",
            "name": "Culinary"
        },
        "instructor": {
            "identifier": "06b1952e57914a8dab98a6c2d2f53c51",
            "name": "Carlos Henriques"
        },
        "description": "Well done! You've finished the Sustainable food practices course. Ready to test your skills? Complete the quiz and earn your certificate today. This course is ideal for any kitchen employees and staff members wanting to learn more about sustainable food practices....",
        "enabled": true,
        "image": "https://images-staging.typsy.com/get/issuers/694081e89df44c39bccb4dabea9568a4/lessons/32a49a1e4a0842de87afa0a10014a163.png?lastMod=637418169125934973",
        "created": "0001-01-01T00:00:00",
        "updated": "2020-11-24T12:15:12.5934973",
        "lengthSeconds": 74
    },
    "success": true,
    "errors": []
}
```

#### No lesson found

A 404 Not Found response will be returned if no lesson is found.
