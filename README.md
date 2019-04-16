# Integrating with Typsy
There are many ways to integrate with Typsy and sometimes the choice of options can be a bit confusing. The good news is that the process is typically simple and quick and we are here to help make it happen.

The following document explains the three items you need to cover:
1. Member account management - how you create accounts for your users in the Typsy system
2. Signing into Typsy - how your members/users/staff will sign into Typsy
3. Accessing Typsy content/training - how your members/users/staff will access our library of content and the (optional) training assigned to them.

### Integration overview
https://docs.google.com/document/d/1vv0EgVPCiCUX15xJEFbs0elN80CzUsri1OvxBgrI4oU/edit?usp=sharing

# Integration options
The following sections detail some of the specific integration options covered in the 'Integration Overview'. 

## LTI
Utilizing the Learning Tools Interoperability (LTI) standard is a common, robust and simple approach supported by many Learning Management Systems (LMS).

### Moodle
Documentation on how to setup LTI in Moodle - https://docs.google.com/document/d/1px34Gz59wV716BVvLpp7BAh7k22K-YgCQAj_eosY4f0/edit?usp=sharing

### Canvas
Documentation on how to setup LTI in Canvas - https://docs.google.com/document/d/1d-bvbrFG1chRzptg63zhF0UN_5DxoBf6HmfIHeY3sjk/edit?usp=sharing

### Blackboard
Documentation on how to setup LTI in Blackboard - https://docs.google.com/document/d/1z2acuyLy6dNxJDz8Z3RkQNtM-KF2s8Rdhc7bohvVNy4/edit?usp=sharing

## Typsy Web Player
It’s possible to embed Typsy Lessons into an external website through the use of the ‘Typsy Web Player’.

The Typsy Player returns an HTML page which is typically embedded into an external system using an iFrame or through launching a new browser window or tab.

The Typsy Player requires certain information passed to it in the URL for authentication and to identify the user.  The Typsy Player tracks all viewing information to the Typsy System. Should the user or manager wish to, they can login and see their statistics.

A sample project, using ASP.NET Core, demonstrates how to embed Typsy Lessons/Videos within an iFrame.
https://github.com/typsy-dev/web-player

### Detailed documentation
https://docs.google.com/document/d/1zunI9KtcbCa5bWecYTpwDHke8pt_8fQv2CCnQ9hwqUM/edit?usp=sharing

## Typsy LMS API
Typsy provides an API that can be used to enable custom integration with LMS based solutions.  The API returns JSON objects.

This approach is typically more complex than using the ‘Typsy Web Player’ (which provides a simple solution for embedding a Typsy lesson via an iFrame). 

A sample project, using ASP.NET Core, demonstrates how to enable the playing of Typsy Lessons/Videos returned from the API.
https://github.com/typsy-dev/api-player

### Detailed documentation
https://docs.google.com/document/d/1ZuWk7--Nl_gFKzv2ACaXw76UBGk_-QDIapnLuH6oBZ0/edit?usp=sharing
