# Integrating with Typsy
There are a variety of options to integrate with Typsy and sometimes the choices can be a bit confusing. The good news is that the process is typically simple and quick and we are here to help make it happen.

### Choose integration approach
You connect via either:
1. Learning Tools Interoperability (LTI)
2. Typsy Web Player
3. Typsy LMS API

Each of these approaches are detailed below under 'Integration options'.

### Integration overview
Any integration with Typsy requires that you support three key functions:
1. Member account management - how you create accounts for your users in the Typsy system (even if they never leave your learning management system)
2. Signing into Typsy - how your members/users/staff will sign into Typsy (all users have the option of accessing Typsy directly to discover all the Typsy content)
3. Accessing Typsy content/training - how your members/users/staff will access our library of content and the (optional) training assigned to them (how the Typsy Content will be presented).

All of the integration approaches enable you to complete these three key functions.

The following document provides an overview of how integrations with Typsy work:
https://docs.google.com/document/d/1vv0EgVPCiCUX15xJEFbs0elN80CzUsri1OvxBgrI4oU/edit?usp=sharing

# Integration options
The following sections detail the specific integration options covered in the 'Integration Overview'. 

## LTI
Utilizing the Learning Tools Interoperability (LTI) standard is a common, robust and simple approach supported by many Learning Management Systems (LMS).  

*This approach is typically the best way to integrate with Typsy*.

### Moodle
Documentation on how to setup LTI in Moodle - https://docs.google.com/document/d/1px34Gz59wV716BVvLpp7BAh7k22K-YgCQAj_eosY4f0/edit?usp=sharing

### Canvas
Documentation on how to setup LTI in Canvas - https://docs.google.com/document/d/1d-bvbrFG1chRzptg63zhF0UN_5DxoBf6HmfIHeY3sjk/edit?usp=sharing

### Blackboard
Documentation on how to setup LTI in Blackboard - https://docs.google.com/document/d/1z2acuyLy6dNxJDz8Z3RkQNtM-KF2s8Rdhc7bohvVNy4/edit?usp=sharing

## Typsy Web Player
If your LMS does not support the LTI standard then this is usually the simplest alternative. Quick to implement and low ongoing maintenance.

If your LMS does not support the LTI standard then this is usually the best alternative as it allows you to embed Typsy Lessons into a user experience you manage.

The Typsy Player returns an HTML page which is embedded into an external system using an iFrame or through launching a new browser window or tab.

The Typsy Player requires certain information passed to it in the URL for authentication and to identify the user.  The Typsy Player tracks all viewing information to the Typsy System. Should the user or manager wish to, they can login to Typsy and see their statistics.

![Image of Typsy Player embedded as an iFrame](http://images.typsy.com/images/integrations/typsy-web-player-iframe.png?width=850)

A sample project, using ASP.NET Core, demonstrates how to embed Typsy Lessons/Videos within an iFrame.
https://github.com/typsy-dev/web-player

### Detailed documentation
https://docs.google.com/document/d/1zunI9KtcbCa5bWecYTpwDHke8pt_8fQv2CCnQ9hwqUM/edit?usp=sharing

## Typsy LMS API
Typsy provides an API that can be used to enable custom integration with LMS based solutions.  The API returns JSON objects.

This approach is typically more complex than using the ‘Typsy Web Player’ (which provides a simple solution for embedding a Typsy lesson via an iFrame). It also has potential for a higher maintenance overhead as, should there be any changes to the structure of the video player, updates will be be required within your LMS.  We always suggest using the Typsy Web Player over the API.  

![Image of Typsy Player embedded using API](http://images.typsy.com/images/integrations/typsy-web-player-api.png?width=850)

A sample project, using ASP.NET Core, demonstrates how to enable the playing of Typsy Lessons/Videos returned from the API.
https://github.com/typsy-dev/api-player

### Detailed documentation
https://docs.google.com/document/d/1ZuWk7--Nl_gFKzv2ACaXw76UBGk_-QDIapnLuH6oBZ0/edit?usp=sharing
