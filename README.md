# Integrating with Typsy
There are a variety of options to integrate with Typsy and sometimes the choices can be a bit confusing. The good news is that the process is typically simple and quick and we are here to help make it happen.

### Choose integration approach
You connect via either:
1. Learning Tools Interoperability (LTI)
2. SCORM
3. Typsy LMS API
4. [xApi](https://github.com/typsy-dev/documentation/blob/master/xApi.md) - contact us for more information about this feature.

Each of these approaches are detailed below under 'Integration options'.

### Integration overview
Any integration with Typsy requires that you support three key functions:
1. Member account management - how you create accounts for your users in the Typsy system (even if they never leave your learning management system they need an account in Typsy)
2. Signing into Typsy - how your members/users/staff will sign into the Typsy Platform (all users have the option of accessing Typsy directly to discover all the Typsy content and view their profile/certificates/badges )
3. Accessing Typsy content/training - how your members/users/staff will access our library of content (e.g. through an LMS or directly in Typsy platform) and the (optional) training assigned to them.

All of the integration approaches enable you to complete the aforementioned three key functions.

# Integration options
The following sections detail the specific integration options covered in the 'Integration Overview'. 

## LTI
Utilizing the Learning Tools Interoperability (LTI) standard is a common, robust and simple approach supported by many Learning Management Systems (LMS).  

*LTI is typically the best way to integrate with Typsy*.

The following link contains a video which demonstrates adding Typsy content, via LTI, to Moodle:
https://info.typsy.com/typsy-integration-demo

### Moodle
Documentation on how to setup LTI in Moodle - https://typsy.sharepoint.com/:w:/s/Development/EdfXkOsLxb9Ehsm8s8YLwkwB8urIj0qiCYCYINZ5B6ZFcQ?e=8w14N6

### Canvas
Documentation on how to setup LTI in Canvas - https://typsy.sharepoint.com/:w:/s/Development/EbQLMBRKqrdNn3gUZ-OWVyIBOR3BnYTTIfzJzWyKSC4IeA?e=alHaOJ

### Blackboard
Documentation on how to setup LTI in Blackboard - https://typsy.sharepoint.com/:w:/s/Development/EdWEcFfaAglFtw8ltyY1t0EBBCSQFZqH-rCXEa7D7fNBtA?e=iNZB7T

## SCORM
Utilizing the SCORM standard is a common approach in many older Learning Management Systems.  Typsy always **recommends LTI over SCORM** as it is more feature rich.  As SCORM does not pass across the User's email address there are some additional steps in place, prior to watching the first lesson, to capture the email.  

Documentation on how to setup SCORM, using Moodle as an example - https://typsy.sharepoint.com/:w:/s/Development/EbHia077-NdNvDQqio16mSkBPgFFYCbHKCQueR9QOoSCWQ?e=JxtJOi
