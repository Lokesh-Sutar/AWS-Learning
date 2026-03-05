# Cloudwatch
- It is Resource Monitoring Tool
- Used to store Logs
- Alerts: Sends notification if anything goes wrong
- You can integrate this with SNS (Simple Notification Service) which runs on following model (pub-sub model, just like YouTube):
    - Publisher
    - Subsciber
    - Topic
- SNS is a managed service that provides message delivery from publishers to subscribers (also known as producers and consumers).
- An SNS topic is a communication channel that allows you to group multiple recipients (subscribers) under a single entity.

## Cloudwatch Dashboard
- You can add multiple widgets (graphs) to monitor system performance

## CloudWatch alarms
- you can create alarms that automatically perform actions if the value of your metric has gone above or below a predefined threshold.
- There are 3 states of the CloudWatch metric alarm:
    - OK : The metric or expression is within the defined threshold.
    - ALARM : The metric or expression is outside of the defined threshold.
    - INSUFFICIENT_DATA : The alarm has just started, the metric is not available, or not enough data is available for the metric to determine the alarm state.
- To set alarms you have to create `SNS topic` and `SNS subcribers`

## Cloudwatch Logs -
- CloudWatch Logs enables you to centralize the logs from all of your systems, applications, and AWS services that you use, in a single, highly scalable service.
- It allows you to monitor, store, and access log files from various AWS services.

## Cloudwatch Events-
- CloudWatch Events delivers a near real-time stream of system events that describe changes in AWS resources.
- CloudWatch Events becomes aware of operational changes as they occur.
- CloudWatch Events responds to these operational changes and takes corrective action.