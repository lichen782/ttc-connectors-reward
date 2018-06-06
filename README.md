# BluePrint - Trending Topic Campaigns: Rewards Service Connector
This project is an implementation of an Activiti Cloud Connector, 
which is a simple bi-directional 3rd party system-to-system integration using Spring Cloud Streams.
 
This project provides the integration mechanisms against a Mock Reward Service. This Activiti Cloud Connector listen to events
generated by Runtime Bundles (Campaigns for this example) and interacts with the Reward Service. 
  


# Run

In order to run this project locally, you need to clone the source code and then run inside the root directory

> mvn -Dserver.port=808x spring-boot:run

**Note**: replace "x" for your desired port number

You can use the following docker-compose file in order to start Rabbit MQ so the service can connect and send messages.



# Endpoints
- GET http://localhost:808x/ -> welcome message
- GET http://localhost:808x/rewards/{campaign} -> Get the rewards that had been sent related to the specified campaign
- POST http://localhost:808x/rewards/{campaign} -> Trigger a manual reward for the top engaged users of the campaign
- DELETE http://localhost:808x/rewards/{campaign} -> Clean up rewards for Campaign

# Campaign Rewards Format
```json
[
    {
        "campaignName": "activiti",
        "rankedAuthor": {
            "nroOfTweets": 1,
            "userName": "WilliamShakespeare"
        },
        "rewardsText": "You Won WilliamShakespeare for your participation in activiti",
        "rewardDate": "2018-06-06T08:51:05.199+0000"
    },
    {
        "campaignName": "activiti",
        "rankedAuthor": {
            "nroOfTweets": 1,
            "userName": "Unknown58"
        },
        "rewardsText": "You Won Unknown58 for your participation in activiti",
        "rewardDate": "2018-06-06T08:51:05.200+0000"
    },
    {
        "campaignName": "activiti",
        "rankedAuthor": {
            "nroOfTweets": 1,
            "userName": "NapoleonHill"
        },
        "rewardsText": "You Won NapoleonHill for your participation in activiti",
        "rewardDate": "2018-06-06T08:51:05.200+0000"
    }
]
```

# Configuration
Rewards Cycles can be configured by setting up the following properties:

>campaignCycle1.campaigns=activiti-en
>campaignCycle1.milliseconds=60000

