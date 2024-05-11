**Title**: ADR-0002-Circuit Breakers for Provider Calls

**Status**: [[Accepted Status]], (By [[Hadi]] - at 2024-10-12)

**Tags**: [[Resilience]], [[Integration]], [[Circuit Breaker]], [[Providers]]

**Context**: In addition to implementing retry mechanisms for provider calls in the flight ticket selling system, there is a need to further enhance resilience by incorporating circuit breakers. Circuit breakers act as a safety mechanism to prevent continuous calls to a provider that is experiencing prolonged failures, thereby protecting the system from cascading failures and preserving resources.

**Decision**: We decide to integrate circuit breakers into the provider call mechanism of the flight ticket selling system. The circuit breakers will monitor the success and failure rates of provider calls and automatically open if the failure rate exceeds a predefined threshold. When the circuit breaker is open, subsequent calls to the failing provider will be bypassed, reducing the load on the provider and allowing it time to recover. After a specified cooldown period, the circuit breaker will attempt to close and resume normal operation, gradually allowing traffic to flow back to the provider.

**Justification**: The decision to add circuit breakers is essential for proactively managing failures and preventing the system from being overwhelmed by continuous requests to a failing provider. By monitoring the health of provider calls and dynamically adjusting the flow of traffic, circuit breakers help mitigate the risk of cascading failures and improve the overall resilience of the system. Additionally, circuit breakers complement retry mechanisms by providing an additional layer of protection against prolonged provider outages, thereby enhancing the system's ability to withstand transient failures.

**Consequences**:

✅**Improved Fault Tolerance:** Circuit breakers enhance the fault tolerance of the system by isolating failing providers and preventing cascading failures.
✅**Reduced Resource Consumption:** By bypassing failing providers, circuit breakers help conserve resources and prevent unnecessary load on the system, improving overall performance and scalability.
❌**Delayed Recovery:** While circuit breakers prevent continuous calls to failing providers, they may also delay the recovery of the affected provider by temporarily blocking traffic. Therefore, it is crucial to carefully tune the circuit breaker parameters to balance between protecting the system and allowing providers sufficient time to recover.
❌**Increased Complexity:** Integrating circuit breakers adds complexity to the system, requiring careful configuration and monitoring to ensure optimal performance and resilience. Additionally, developers need to be aware of the circuit breaker state and handle circuit open scenarios gracefully to provide meaningful feedback to users.
