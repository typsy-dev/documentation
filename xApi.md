# xApi statements
Typsy supports publishing xApi statements when certain learning events are completed.

Typsy customers can subscribe to these messages and save the information in their own Learning Management System (LMS) and/or Reporting System (e.g a data warehouse).

It's important to understand that xApi (even though it has the term 'Api' within it) is **not** an Api hosted by Typsy that you make requests to.  xApi is a standard (or schema) for describing a JSON message that Typsy will 'push' to you, much like how a [Webhook](https://en.wikipedia.org/wiki/Webhook) functions.

For more information about xApi visit https://xapi.com/statements-101

## Supported statements
Typsy currently supports **progressed** and **completed** [verbs](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI-Data.md#verb) for Courses & Lessons.

By default, these verbs use a Typsy namespace (e.g. http://xapi.typsy.com/verbs/completed). The messages can also be provided with the [ADLNET namespace](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI-Data.md#verb) (e.g. https://adlnet.gov/expapi/verbs/completed)

## Integration
### Integration overview
1. A learner completes a course within Typsy.
2. Typsy publishes (pushes) an xApi statement (JSON) to an asynchronous HTTPS endpoint that the customer exposes.
3. Customer processes message - saving the data they require to an internal system.  Any mapping of the fields within the xApi message to internal systems is the customer's responsibility. Typsy is able to transform the xApi message it produces should specific fields be required in a particular format (e.g. if the value for a claim, that represents a unique user, must be attached to the Actor object).

### Customer endpoint
The endpoint provided to Typsy must have the following characteristics:
1. Accessible over the internet via HTTPS POST (it is typically REST based)
2. High availability
3. Must be **asynchronous** (in other words, accept the xApi message from Typsy and immediately provide a valid [HTTP status code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)).  The message is typically stored internally on a message queue for subsequent processing.
4. It's preferable that the endpoint supports authentication.
5. It is highly recommended that the endpoint supports idempotency - that is it must handle the same message being sent multiple times.  Should the same message be received multiple times a 2xx status code must be returned and the process to handle the duplicate message is internal to the customer system. Should you wish to reject the duplicate, provide a 409 status code.  This is important as there are scenarios where the same message can be sent twice - for example requests for batch migration (where all messages from a previous time frame can be requested again) or if there was an error in the message (e.g. a calculation is incorrect) and the message (with the same id) must be sent again.

### Sample xApi message
This is a sample message sent at course completion

    {
        "id": "f4178dfb-d61c-4a16-8ab3-5b9fccae7d8c",
        "stored": "2018-11-01T19:03:01.2719736Z",
        "authority": {
            "objectType": "Agent",
            "name": "Typsy",
            "mbox": "mailto:badges@typsy.com"
        },
        "actor": {
            "objectType": "Agent",
            "name": "John Shaker",
            "account": {
                "homePage": "https://www.typsy.com/profile/john-shaker",
                "name": "4db4abe545c74c16bff2c82d45d1a9b8"
            }
        },
        "verb": {
            "id": "http://xapi.typsy.com/verbs/completed",
            "display": {
                "en": "completed"
            }
        },
        "object": {
            "objectType": "Activity",
            "id": "http://xapi.typsy.com/activity/788f7f25ba4e4801a438f2108fe2fa0a",
            "definition": {
                "type": "http://xapi.typsy.com/types/course",
                "moreInfo": "https://www.typsy.com/courses/wine-101-for-servers",
                "name": {
                    "en": "Wine 101 for servers"
                },
                "description": {
                    "en": "Mastering wine service is one of the most important and valuable skills a server can possess. The ability to perform tableside wine service with confidence is a guaranteed way to display your professionalism and your knowledge of the different aspects of the hospitality industry. It's also an una..."
                },
                "extensions": {
                    "http://xapi.typsy.com/course/id": 299,
                    "http://xapi.typsy.com/course/issuer": "Typsy",
                    "http://xapi.typsy.com/course/self-discovery": false,
                    "http://xapi.typsy.com/course/iteration": 1,
                    "http://xapi.typsy.com/user/workspace-structures": "Hotel A,Hotel B",
                    "http://xapi.typsy.com/user/workspace-teams": "Bar Staff",
                    "http://xapi.typsy.com/user/workspace-job-roles": "Barista",
                    "http://xapi.typsy.com/badge/expires": "2024-02-16T02:05:12.48Z"
                },
                "interactionType": "choice"
            }
        },
        "result": {
            "completion": true,
            "duration": "PT28M48S",
            "score": {
                "scaled": 1,
                "raw": 14,
                "min": 0,
                "max": 14
            },
            "extensions": {
                "http://xapi.typsy.com/course/quiz/attempts": 1,
                "http://xapi.typsy.com/course/quiz/scaled": 0.85,
                "http://xapi.typsy.com/course/quiz/raw": 11,
                "http://xapi.typsy.com/course/quiz/min": 10,
                "http://xapi.typsy.com/course/quiz/max": 13
            }
        },
        "context": {
            "platform": "Typsy",
            "language": "en",
            "extensions": {
                "http://xapi.typsy.com/user/workspace-id": 987654321,
                "http://xapi.typsy.com/user/workspace-email": "john.shaker@sample.com",
                "http://xapi.typsy.com/user/workspace-claims": "customer-employee-id:0123456789",
                "http://xapi.typsy.com/account/id": 82,
                "http://xapi.typsy.com/account/name": "Demo Inc",
                "http://xapi.typsy.com/account/vanity-name": "Demo"
            }
        },
        "timestamp": "2018-11-01T19:03:01.2719736Z"
    }

This is a sample message sent at course progressed

    {
        "id": "f4178dfb-d61c-4a16-8ab3-5b9fccae7d8c",
        "stored": "2018-11-01T19:03:01.2719736Z",
        "authority": {
            "objectType": "Agent",
            "name": "Typsy",
            "mbox": "mailto:badges@typsy.com"
        },
        "actor": {
            "objectType": "Agent",
            "name": "John Shaker",
            "account": {
                "homePage": "https://www.typsy.com/profile/john-shaker",
                "name": "4db4abe545c74c16bff2c82d45d1a9b8"
            }
        },
        "verb": {
            "id": "http://xapi.typsy.com/verbs/progressed",
            "display": {
                "en": "progressed"
            }
        },
        "object": {
            "objectType": "Activity",
            "id": "http://xapi.typsy.com/activity/788f7f25ba4e4801a438f2108fe2fa0a",
            "definition": {
                "type": "http://xapi.typsy.com/types/course",
                "moreInfo": "https://www.typsy.com/courses/wine-101-for-servers",
                "name": {
                    "en": "Wine 101 for servers"
                },
                "description": {
                    "en": "Mastering wine service is one of the most important and valuable skills a server can possess. The ability to perform tableside wine service with confidence is a guaranteed way to display your professionalism and your knowledge of the different aspects of the hospitality industry. It's also an una..."
                },
                "extensions": {
                    "http://xapi.typsy.com/course/id": 299,
                    "http://xapi.typsy.com/course/issuer": "Typsy",
                    "http://xapi.typsy.com/course/self-discovery": false,
                    "http://xapi.typsy.com/course/iteration": 1,
                    "http://xapi.typsy.com/user/workspace-structures": "Hotel A,Hotel B",
                    "http://xapi.typsy.com/user/workspace-teams": "Bar Staff",
                    "http://xapi.typsy.com/user/workspace-job-roles": "Barista"
                },
                "interactionType": "choice"
            }
        },
        "result": {
            "completion": false,
            "duration": "PT28M48S",
            "score": {
                "scaled": 0.07,
                "raw": 1,
                "min": 0,
                "max": 14
            }
        },
        "context": {
            "platform": "Typsy",
            "language": "en",
            "extensions": {
                "http://xapi.typsy.com/user/workspace-id": 987654321,
                "http://xapi.typsy.com/user/workspace-email": "john.shaker@sample.com",
                "http://xapi.typsy.com/user/workspace-claims": "customer-employee-id:0123456789",
                "http://xapi.typsy.com/account/id": 82,
                "http://xapi.typsy.com/account/name": "Demo Inc",
                "http://xapi.typsy.com/account/vanity-name": "Demo"
            }
        },
        "timestamp": "2018-11-01T19:03:01.2719736Z"
    }

