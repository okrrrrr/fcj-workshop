---
title: "Week 6 Worklog"
date: 2026-05-25
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Learn Serverless with Lambda and API Gateway.
* Learn how to build event-driven architecture with EventBridge.
* Practice Step Functions to orchestrate workflows.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 2 | Reviewed Docker, ECS knowledge from Week 5. Learned Lambda basics: functions, runtimes, triggers. Understood Lambda execution roles and environment variables. Learned Lambda layers to share code and versioning | 25/05/2026 | 25/05/2026 | <https://serverlessland.com/lambda> |
| 3 | Created Lambda Function with Python runtime. Wrote handler code to process event. Configured API Gateway REST API. Created GET method with Lambda integration to fetch data. Created POST method to receive data from client. Deployed API to Stage (dev) for testing. Tested API using Postman or curl. Enabled CORS for API Gateway to allow cross-origin requests | 26/05/2026 | 26/05/2026 | <https://000066.awsstudygroup.com/> |
| 4 | Created DynamoDB Table (Users) with partition key user_id. Created Lambda function for CREATE operation (POST /users) to add new user. Created Lambda function for READ operation (GET /users/{id}) to get user info. Created Lambda function for UPDATE operation (PUT /users/{id}) to update data. Created Lambda function for DELETE operation (DELETE /users/{id}) to delete user. Configured Lambda layers to share common code between functions. Configured environment variables for table name instead of hardcoding. Tested all CRUD operations via API Gateway | 27/05/2026 | 27/05/2026 | <https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-dynamo-db.html> |
| 5 | Accessed Step Functions Console. Created State Machine to define workflow. Wrote ASL (Amazon States Language) definition describing flow steps. Added Pass state to transform data between steps. Added Task state calling Lambda function to perform business logic. Added Choice state for conditional logic (e.g., if approved then do what). Added Map state to process array items in parallel. Added Parallel state to run multiple tasks concurrently. Executed state machine and checked execution logs for debugging | 28/05/2026 | 28/05/2026 | <https://catalog.workshops.aws/stepfunctions/en-US> |
| 6 | Created custom EventBridge Event Bus to receive events. Created Rule to capture EC2 state change events (e.g., when instance start/stop). Configured Target as Lambda function to process matching events. Created API Destination to forward events to external services. Created Scheduler to schedule Lambda invocations by time. Created SQS Queue to receive and store messages. Created Lambda consumer to process SQS messages asynchronously. Configured EventBridge Rule to trigger Lambda when events occur. Created SNS Topic to send notifications. Connected all components into complete flow to process data pipeline | 29/05/2026 | 29/05/2026 | <https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-get-started.html> |


### Week 6 Achievements:

* Created and deployed Lambda functions with API Gateway integration.
* Built Serverless CRUD API with DynamoDB backend.
* Used Step Functions to orchestrate multi-step workflows.
* Deployed Event-Driven Architecture with EventBridge and SQS.
