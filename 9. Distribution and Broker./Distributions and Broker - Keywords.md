# Distributed System
A distributed system is one in which components located at networked computers communicate and coordinate their actions only by passing messages.

# Marshalling
**Is the process of taking a collection of structured data items and assembling them into a byte array suitable for transmission in a networks message**

# Unmarshalling
**Is the process of disassembling a byte array received in a network message to produce the equivalent collection of structed data items.**


# A Future
A concept in Software-engineering which represents the answer to a request which may  take a long time to compute. The Future can then be polled to see if the answer has become available, once it is the answer can be received. The purpose of a Future is to avoid the client block for a long time while the answer is being computed.

# Multi Type Dispatching
When using Multi Type Dispatching, we are using a "super" invoker that delegates to subInvokers. In hotstone for example we had the card, game and hero Invokers. Prevents the blob