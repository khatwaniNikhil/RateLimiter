# Resources
1. https://www.alibabacloud.com/blog/throttling-solutions-in-standalone-and-distributed-scenarios_596984
2. https://www.quinbay.com/blog/understanding-rate-limiting-algorithms
3. https://medium.com/@avocadi/rate-limiter-sliding-window-counter-7ec08dbe21d6
4. https://www.figma.com/blog/an-alternative-approach-to-rate-limiting/

# Approaches
# Fixed size Window
fixed size windows, incoming request mapped to a window and check for threshold cutoff in that window

### PRO
straightforward and simple to implement
### cons
in case of bursts at window boundaries, total requests in a overlapping section across two consecutive windows could be higher than threshold

# Sliding Window: 
other than checking incoming request in the mapped current window for threshold cut off, imagine a virtual window ending at current timestamp - check for cutoff in this virtual window also.

### PRO
request processing rate better managed than fixed window.

### Cons: 
in case of bursts, cuts off the traffic suddenly so no smoothness in throttling.

# Leaky Bucket:
input request rate can vary and discarded in case of bucket overflow, but the output request processing rate remains constant.
Bucket acts as an queue.
![image](https://github.com/khatwaniNikhil/RateLimiter/assets/3686308/06caa5f3-3e9b-4801-8f99-78c666f87e6d)

## Conceptual analogies are listed below:
1. Maximum Number of Requests Allowed (N): The bucket size
2. Time Window Size (T): The time required for the entire bucket to be drained
3. Maximum Traffic Rate (V): The rate at which the entire bucket of water leaks, which is equal to N/T
4. Request Throttling: Indicates that the water injection rate is greater than the water leakage rate, eventually causing an overflow of water in the bucket

## use case
usually used for traffic shaping in network communication.

# Token Bucket:
![image](https://github.com/khatwaniNikhil/RateLimiter/assets/3686308/0490a8b0-3546-4d25-8e08-c1b1d018325c)

## use case
allows the output rate to vary depending on the traffic burst size.
