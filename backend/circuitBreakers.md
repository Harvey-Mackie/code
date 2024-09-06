# Circuit Breakers

## To Add
Other resilience4j types - rate limiter, retry, thread pools etc

## Resources
https://resilience4j.readme.io/docs/circuitbreaker
https://chatgpt.com/c/a397b183-f88f-49ee-8065-63ad2e309c7e
https://resilience4j.readme.io/docs/getting-started-3
## Notes


### State and Theory

#### Types of state
Circuit Breakers are implemented via a finite state machine with three states:
- Open (no requests allowed until wait duration is reached) 
- Half Open (limited number of reuests allowed)
- Closed (all requests flow normally - no breaker applied)

#### How the state works?
FLOW -  CLOSED -> OPEN -> HALF-OPEN -> CLOSED

- Closed is the default state - transactions will flow normally.
- When the failure threshold is reached, state will move to OPEN
- After custom wait duration is reached, limited number of requests will be allowed as it moves into HALF OPEN
- If failure rate is below threshold, state moves back to CLOSED
- Failures are based on exceptions you create to listen for (failure exceptions), can also be time constraints (slow calls)

#### Sliding Windows
Sliding windows are used to monitor the state of the last X calls, then when a certain threshold is reached for failures/successes the state will change accordingly. There are two types of sliding windows:
- Time based - e.g. aggregate all requests in last 10 seconds
- Count based - e.g. aggregate the last 100 requests


### Implementation
```java
// Create a custom configuration for a CircuitBreaker
CircuitBreakerConfig circuitBreakerConfig = CircuitBreakerConfig.custom()
    // Set failure rate and slow call thresholds
    .failureRateThreshold(50)
    .slowCallRateThreshold(50)

    // Define wait duration in Open state and slow call threshold
    .waitDurationInOpenState(Duration.ofMillis(1000))
    .slowCallDurationThreshold(Duration.ofSeconds(2))

    // Set permitted calls in Half-Open state and sliding window settings
    .permittedNumberOfCallsInHalfOpenState(3)
    .minimumNumberOfCalls(10)
    .slidingWindowType(SlidingWindowType.TIME_BASED)
    .slidingWindowSize(5)

    // Define the exceptions that should trigger the breaker
    .recordException(e -> INTERNAL_SERVER_ERROR.equals(getResponse().getStatus()))
    .recordExceptions(IOException.class, TimeoutException.class)
    .ignoreExceptions(BusinessException.class, OtherBusinessException.class)
  .build();

// Create a CircuitBreakerRegistry with a custom global configuration
CircuitBreakerRegistry circuitBreakerRegistry = 
  CircuitBreakerRegistry.of(circuitBreakerConfig);
```
```
```


### Benefits (Why Use One)
- Avoid repeated failures - if a downstream API is down this will limit the amount of failures as it will register the failure and wait.
- Reduces load on services - prevents adding extra load to API during outage and allows your microservice to prevent performing excessive calls when an error is expected.
- Better monitoring and recovery - prevents unneccessary manual intervention due to the restricted number of API calls being mad.
