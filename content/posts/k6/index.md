---
title: "K6: A Powerful Tool for Load Testing"
date: 2025-01-27
draft: false
image: "k6.png"
categories:
    - qa
tags:
    - load-testing
    - automate-testing
    - k6
    - Kamkarha
author:
    name: "Neda Sarvestani"
    image: "neda.jpg"
    linkedin: "https://www.linkedin.com/in/nedasarv"
    mail: "mailto:neda.svt@gmail.com"
    medium: "https://medium.com/@neda.svt"
---

1. **Introduction**

K6 is a powerful and efficient tool in the field of automated testing, which is especially useful for load testing. In this article, we introduce load testing and explain how we used K6 to test one of our team's critical projects.

## What is Automated Testing and Load Testing?

Automated software testing is a process where tools are used to test software and find bugs. These tests simulate user interactions with the application or system, increasing the speed, efficiency, and accuracy of testing compared to manual testing. Automated tests allow for the execution of thousands of diverse and lengthy tests, something that would be impossible with manual testing.

The main goal of automated testing is to enhance testing efficiency and software development processes.

## Advantages of Automated Testing:

- **Increased productivity** 
- **Cost savings** 
- **Improved software quality** 
- **Reduced testing time** 
- **Support for load testing** 

## What is Load Testing?

Load testing is the process of subjecting a website or application to multiple requests to evaluate its performance. It involves sending simulated HTTP traffic to the server to answer questions like:

- Is the server's response time appropriate and close to our expected target?
- Is the application, website, or software running efficiently?
- Have sufficient resources been allocated to handle the expected load?

Various tools, such as K6, Gatling, LoadRunner, and JMeter, can be used for load testing.In this article, we focus on K6, which we used for load testing our website and API endpoints.

2. **Why K6?**

K6 is an open-source tool for load and performance testing. It helps developers and QA teams evaluate the performance of applications and services under heavy load. Although K6 is written in Go language, we use JavaScript to write test scripts.

K6 is modern, flexible, and user-friendly, making it a preferred tool for load testing. We used K6 for load testing the “**Kamkarha Music Group**” project at Fidibo. The project involved developing a ticket reservation system for an orchestral concert, and once the system was built, we needed to ensure it could handle high traffic from concertgoers. This testing helped us identify and debug potential issues.

In the following sections, we will explain the step-by-step process for performing load testing with K6.

3. **Load Testing Step by Step**

**Step 1 (Install K6):**

To install K6 on Ubuntu, follow these steps:

```
$ sudo apt update
$ sudo apt install snapd
$ sudo snap install k6
```

**Step 2 (Writing Test Scripts):**

The next step is to write the test scenarios in a script file. Here’s a simple example of the script:

```js
import http from 'k6/http';
import { check, sleep } from 'k6';

export default function () {
  const res = http.get('https://your/api/address');
  
  check(res, { 'status is 200': (r) => r.status === 200 });
  check(res, { 'response time < 120000ms': (r) => r.timings.duration < 120000 });
  
  console.log(`Request duration: ${res.timings.duration}ms`);
  console.log(`Response status: ${res.status}`);
  
  sleep(4);
}
```

In this script, we have three important components:

- **HTTP Requests:** We make a request to an API or website.
- **Check:** We use the check function to verify that the response status is 200 (OK) and that the response time is within an acceptable range.
- **Sleep:** We simulate user behavior by adding a 4-second pause between requests.
For load testing, you can define stages to simulate different user behaviors.
For example:
- **Stage 1:** Ramp up to 10,000 virtual users over 10 seconds.
- **Stage 2:** Keep 10,000 users active on the website.
- **Stage 3:** Reduce users to zero over 10 seconds.
You can customize these stages based on your specific requirements.

**Step 3 (Test Execution):**

At this stage, we use the command bellow to execute the test and view the results directly in the terminal:

```
k6 run file_name
```

Once the test is completed, you will receive data about the performance of the system, including:

- **Response times**
- **Request statuses**
- **Performance trends**

For example, in our case, the load test on the “**Kamkarha Music Group**” ticket reservation system successfully handled ticket reservations for four sessions without any downtime.

4. **Conclusion**

Load testing ensures that your software can handle both expected and unexpected traffic effectively. K6 is a powerful and efficient load testing tool that is easy to learn and use. It was instrumental in our successful testing of the ticket sales system for “**Kamkarha Music Group.**” With K6, we were able to test and ensure the website could handle the stress of concert ticket reservations without any issues.

I highly recommend K6 for load testing, whether you are working on an application, website, or API. By following the steps outlined in this article, you can easily set up and execute your own load tests for your projects.