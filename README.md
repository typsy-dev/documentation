# Integrating with Typsy
There are a variety of options to integrate with Typsy and sometimes the choices can be a bit confusing. The good news is that the process is typically simple and quick and we are here to help make it happen.

### Choose integration approach
You connect via either:
1. Learning Tools Interoperability (LTI)
2. SCORM
4. Typsy Web Player
5. Typsy LMS API
6. xAPI (contact us for more information about this beta feature)

Each of these approaches are detailed below under 'Integration options'.

### Integration overview
Any integration with Typsy requires that you support three key functions:
1. Member account management - how you create accounts for your users in the Typsy system (even if they never leave your learning management system they need an account in Typsy)
2. Signing into Typsy - how your members/users/staff will sign into the Typsy Platform (all users have the option of accessing Typsy directly to discover all the Typsy content and view their profile/certificates/badges )
3. Accessing Typsy content/training - how your members/users/staff will access our library of content (e.g. through an LMS or directly in Typsy platform) and the (optional) training assigned to them.

All of the integration approaches enable you to complete the aforementioned three key functions.

The following document provides an overview of how integrations with Typsy work:
https://docs.google.com/document/d/1vv0EgVPCiCUX15xJEFbs0elN80CzUsri1OvxBgrI4oU/edit?usp=sharing

# Integration options
The following sections detail the specific integration options covered in the 'Integration Overview'. 

## LTI
Utilizing the Learning Tools Interoperability (LTI) standard is a common, robust and simple approach supported by many Learning Management Systems (LMS).  

*LTI is typically the best way to integrate with Typsy*.

The following link contains a video which demonstrates adding Typsy content, via LTI, to Moodle:
https://info.typsy.com/integration-demo

### Moodle
Documentation on how to setup LTI in Moodle - https://docs.google.com/document/d/1px34Gz59wV716BVvLpp7BAh7k22K-YgCQAj_eosY4f0/edit?usp=sharing

### Canvas
Documentation on how to setup LTI in Canvas - https://docs.google.com/document/d/1d-bvbrFG1chRzptg63zhF0UN_5DxoBf6HmfIHeY3sjk/edit?usp=sharing

### Blackboard
Documentation on how to setup LTI in Blackboard - https://docs.google.com/document/d/1z2acuyLy6dNxJDz8Z3RkQNtM-KF2s8Rdhc7bohvVNy4/edit?usp=sharing

## SCORM
Utilizing the SCORM standard is a common approach in many older Learning Management Systems.  Typsy always recommends LTI over SCORM as it is more feature rich.  As SCORM does not pass across the User's email address there are some additional steps in place, prior to watching the first lesson, to capture the email.  

Documentation on how to setup SCORM, using Moodle as an example - https://docs.google.com/document/d/165aOsSMsAeGEnrjdWuews6mYQ3aBXGa6qxZa-qhNHKc/edit?usp=sharing 

## Typsy Web Player
If your LMS does not support the LTI standard then this is usually the simplest alternative. Quick to implement and low ongoing maintenance. It allows you to embed Typsy Lessons into a user experience you manage.

The Typsy Player returns an HTML page which is embedded into an external system using an iFrame or through launching a new browser window or tab.

The Typsy Player requires certain information passed to it in the URL for authentication and to identify the user.  The Typsy Player tracks all viewing information to the Typsy System. Should the user or manager wish to, they can login to Typsy and see their statistics.

![Image of Typsy Player embedded as an iFrame](https://typsy.blob.core.windows.net/images/integrations/typsy-web-player-iframe.png)

A sample project, using ASP.NET Core, demonstrates how to embed Typsy Lessons/Videos within an iFrame.
https://github.com/typsy-dev/web-player

### Detailed documentation
https://docs.google.com/document/d/1zunI9KtcbCa5bWecYTpwDHke8pt_8fQv2CCnQ9hwqUM/edit?usp=sharing

## Typsy LMS API
Typsy provides an API that can be used to enable custom integration with LMS based solutions.  The API returns JSON objects.

This approach is typically more complex than using the ‘Typsy Web Player’ (which provides a simple solution for embedding a Typsy lesson via an iFrame). It also has potential for a higher maintenance overhead as, should there be any changes to the structure of the video player, updates will be be required within your LMS.  We always suggest using the Typsy Web Player over the API.  

![Image of Typsy Player embedded using API](https://typsy.blob.core.windows.net/images/integrations/typsy-web-player-api.png)

A sample project, using ASP.NET Core, demonstrates how to enable the playing of Typsy Lessons/Videos returned from the API.
https://github.com/typsy-dev/api-player

### Detailed documentation
https://docs.google.com/document/d/1ZuWk7--Nl_gFKzv2ACaXw76UBGk_-QDIapnLuH6oBZ0/edit?usp=sharing
