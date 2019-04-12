---
layout: post
title: On the range with CloudWatch Alarms 🚨
tags: aws, cloudwatch
---

Recently at work I wanted a CloudWatch alarm that only fired when a metric value was between two other values; trying to be clever with CPU alarms.
Looking around on Google I found nobody else had blogged/documented anything; so I'm changing that.

## Ah, that's why I did maths at school

I remembered that a bell curve would fit the job perfectly, and quickly found the equation for a [Gaussian Function](https://en.wikipedia.org/wiki/Gaussian_function) knowing that I could make use of it with [CloudWatch Metric Math](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/using-metric-math.html).

For some reason CloudWatch Math doesn't have a definition of `e` but since we don't need to be _that_ accurate, I hard coded it as `2.71828`—there's 6 significant figures of which CloudWatch metric values could only be 5 so it's good enough.

CloudWatch Math _does_ support exponents though so I'm in with a chance; defining the alarm with 2 metrics:

* `cpu` being my CPU value,
* `range` being the math expression: `2.71828 ^ ( -1 * ( (cpu - 85) ^ 2)/(15^2)) - 0.3`

There's a few magic numbers here which correlate to the Gaussian function which I'll briefly explain here:

* `85` is the midpoint
* `15` is the value we add/subtract from the midpoint to get our upper/lower boundaries respectively
* `0.3` drops the curve so that any value is above 0 when it's within the range. (It just makes it look nice)

It's also incredibly easy to include this in CloudFormation:

```yaml
AWSTemplateFormatVersion: 2010-09-09
Description: Demo Template
Parameters:
  # This is a demo I don't need parameters
  
Resources:
  RDSClusterReaderHighCPUAlarm:
    Type: AWS::CloudWatch::Alarm
    DependsOn: [ RDSDBInstance1, RDSDBInstance2 ]
    Properties:
      AlarmName: !Sub "${RDSIdentifier}-rds-cluster-High_CPU"
      AlarmDescription: !Sub >-
        {
          "a fancy json document": "yes it's nicely hooked up to our internal tools",
          "sounds fun?": "come join us https://www.metoffice.gov.uk/careers"
        }
      Metrics:
        -
          Id: cpu
          ReturnData: false
          MetricStat:
            Metric:
              Namespace: AWS/RDS
              MetricName: CPUUtilization
              Dimensions:
                - Name: DBClusterIdentifier
                  Value: !Sub "${RDSIdentifier}-rds-cluster"
                - Name: Role
                  Value: READER
            Period: 60
            Stat: Minimum
        -
          Id: alarm
          # Misnomer, this determines which metric is returned to be evaluated against the threshold
          ReturnData: true
          Expression: 2.71828 ^ ( -1 * ( (cpu - 85) ^ 2)/(15^2)) - 0.3
      ActionsEnabled: True
      AlarmActions:
        - !Sub arn:aws:sns:${AWS::Region}:${AWS::AccountId}:[a fancy sns topic]
      OKActions:
        - !Sub arn:aws:sns:${AWS::Region}:${AWS::AccountId}:[a fancy sns topic]
      EvaluationPeriods: 30
      # Threshold set to ensure the alarm only triggers when values are between the appropriate values
      Threshold: 0.01
      TreatMissingData: breaching
      ComparisonOperator: GreaterThanThreshold

```

There you have it, how to ensure a CloudWatch Alarm only triggers when it's between a range. 
Is it worth it? Maybe.
I used this to determine when to send a MINOR or a MAJOR alert to our internal monitoring tool; MAJOR or MINOR depending on how high the CPU value is at.
Even though we've got AutoScaling enabled on RDS so the alarm shouldn't ever fire this is production so anything can happen 👍.

My two ranges overlapped slightly, as it's entirely possible for you to flip-flop in and out of the range thus trigger neither Alarm, defeating the whole point.
It requires tweaking; and in most cases I'd suggest having a MINOR and MAJOR alarm on a simple GreaterThan comparison and when *Ops receive the alarm, fixing the MAJOR should fix the minor

Still, it's nice to know it's possible and I got a blog post out of it...
