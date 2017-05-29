# AWSLambda_RIPEAtlas_CloudWatch [![Build Status](https://travis-ci.org/chriselsen/AWSLambda_RIPEAtlas.svg?branch=master)](https://travis-ci.org/chriselsen/AWSLambda_RIPEAtlas)
AWS Lambda script to push Status and Latency information from a RIPE Atlas (https://atlas.ripe.net/) health check into AWS CloudWatch

RIPE Atlas employs a global network of probes that measure Internet connectivity and reachability. Status checks let you turn a measurement into a basis for an alert, allowing you to use measurements to gauge the health of your network in a variety of ways. This AWS Lambda script collects information from a RIPE Atlas status check and feeds it into AWS CloudWatch metrics.

**Pre-Requisites:**
* Role for Lambda that allows put-metric access to Amazon CloudWatch
* RIPE Atals account with a "status check" measurement (https://atlas.ripe.net/docs/api/v2/manual/measurements/status-checks.html)

**How-To:**
* Create AWS Lambda function
 * Name: RIPEAtlas_CloudWatch
 * Description: Check availability of websites
 * Runtime: Node.js 4.3
 * Handler: index.handler
 * Timeout : 10 sec
 * Source: In file RIPEAtlas_CloudWatch.nodejs
* Configure AWS CloudWatch event rule as trigger
 * Schedule: Fixed rate of 5 minute
 * Function: RIPEAtlas_CloudWatch
 * Input: Constant (JSON text)
 * JSON: { "atlasid": "1234567", "target": "www.test.com_IPv6" }

**Explanation of JSON:**
 * atlasid: Measurement of the RIPE Atlas status check
 * target: Name of the corresponding metrics in CloudWatch
