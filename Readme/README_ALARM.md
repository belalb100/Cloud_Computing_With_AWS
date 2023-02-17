## How to set up an alarm for our EC2 app instance:

1. Open the AWS Management Console and navigate to the CloudWatch service.

2. In the left-hand menu, click on "Alarms".

3. Click on the "Create alarm" button.

4. Choose "EC2 metrics" as the source for your alarm, you may have to type this in the search column.

5. Select the "Per-Instance Metrics" (you may have to type this in the search column) option and then choose the instance you want to monitor."

6. Under "Select metric", choose "CPUUtilization".

7. Under "Conditions", you can specify the threshold at which you want the alarm to trigger. For example, you can set the threshold to trigger when CPU utilization is greater than 60%.

8. Under "Actions", you can choose what action you want to take when the alarm is triggered. For example, you can send an email notification, stop or terminate the instance.

9. We select create new topic, that way we are able to enter out email address and we need to choose a topic

10. Then we click create topic and we can test our alarm and see if we get an email, and we can confirm using our email.

11. Give your alarm a name and description, and then click "Create Alarm".

Once your alarm is created, you can view it in the CloudWatch Alarms console and manage it as needed.