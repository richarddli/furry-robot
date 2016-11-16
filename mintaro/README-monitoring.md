Mintaro
-------

Your application and services depend on APIs. Externally, you might use Stripe or Twilio. Internally, you might use ElasticSearch or a microservice. How do you know, immediately, if one of these APIs isn't performing?

Mintaro is a monitoring system that does real-time client-side monitoring of APIs. Mintaro is different from traditional tools in a few different ways:

* The expected behavior of an API is defined as part of the API specification stored in source control, instead of a threshold stored in a cloud system somewhere
* You define what you want to monitor at an API level, not an application level
* Mintaro monitors actual RPC interactions, instead of just passively collecting metrics
* Alerts occur when actual metrics deviate from expected behavior, instead of relying on anomaly detection algorithms

Example 1: External service
---------------------------

Imagine you're using Stripe's Payment API to make a charge in your code. In your Mintaro file, you could write this:

```
method stripe.Charge.create() {
  max_latency = 100ms
  max_error_rate = 1%
}
```

Mintaro would then alert you if either of these limits were encountered during a Charge.create().

Alternative
-----------

Let's say you don't want to use Mintaro. What are your choices?

* You could use an API monitoring solution such as Runscope. However, Runscope will only execute a synthetic transaction against the Stripe API -- it's not your actual code that's running.
* You could write your own custom wrapper around your RPC that tracks latency. But don't you have better things to do?

[WIP below]

Quick start
-----------

1. pip install mm

2. Define what healthy looks like for a given service in a service.mm file:

   method makePayment(String foo) {
     latency = 50ms
     max_error_rate = 1%
   }
   
3. Get an authentication token, and add the token to the file:

   $ mm get_token
   token=YOUR_SECRET_HERE

4. Wrap each of your methods with a magical wrapper?


Smart alerts
------------

We do the analytics to figure out when to actually alert.

How would I do this normally?
-----------------------------

In the try/catch block, do a:
  send_alert('STRIPE IS BROKEN')


Use case: New version rollout
----------------------------

--> why is this an urgent problem?
 - monitoring is a requirement
 - it took you 3 hours before someone noticed that some functionality
   wasn't working
   - because you rely on a third party service for SMS
     or payments
   - because you built some service that degraded gracefully


Use case: Canary Test
---------------------

Because you're smart, you canary test. You roll out a new service and
route 5% of your traffic to the service. 
