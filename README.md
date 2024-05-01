# gRPC Tutorial (Module 9: High Level Networking)

```credential
Nama  : Muhammad Milian Alkindi
Kelas : AdPro-B (Reguler)
```

## Reflection

> Q: What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods,
> and in what scenarios would each be most suitable?

A:

- **Unary**: Client sends a single request, server sends a single response
  - Suitable scenarios: Fetching a single item from a database, Authenticate a user, PaymentService
- **Server Streaming**: Client sends a single request, server sends a stream of responses to the client
  - Suitable scenarios: Large file transfer in chunks, TransactionService
- **Bi-directional**: Client and server engages in interactive communication to conduct a conversation
  - Suitable scenarios: Real-time analytics where data is continuously sent from server to client and vice versa, ChatService

> Q: What are the potential security considerations involved in implementing a gRPC service in Rust,
> particularly regarding authentication, authorization, and data encryption?

A:

- Authentication: System will need to ensure client and server are authenticated before accessing sensitive data (e.g: passwords). One method would be to pass auth-tokens on each request.
- Authorization: Server will need to make sure to only act on requests based on the authenticated client's authorization level. (e.g: don't process requests of client requesting other client's private info)
- Data Encryption: Sensitive data in requests and responses will have to be encrypted to prevent middleman attacks and ensure its confidentiality.

> Q: What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC,
> especially in scenarios like chat applications?

A:

- Resource management issues such as memory leak for connections over long periods of time
- Eavesdropping of other client's chat with the server

> Q: What are the advantages and disadvantages of using the `tokio_stream::wrappers::ReceiverStream` for streaming responses in Rust gRPC services?

A:

- Advantages:
  - Integrated with other `tokio` library methods
- Disadvantages:
  - Dependent on `tokio` library

> Q: In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity,
> promoting maintainability and extensibility over time?

A: One way would be to separate existing code into different modules to lessen the responsibility of each file (Single Responsibility Principle).
For example, `grpc_server.rs` currently contains code for all three server services (`PaymentService`, `TransactionService`, and `ChatService`).
Separating them into different files (e.g: `server/payment_service.rs`, `server/transaction_service.rs`, `server/chat_service.rs`) will help with
maintainability as each module only has a single responsibility/service to cover.

> Q: In the `MyPaymentService` implementation, what additional steps might be necessary to handle more complex payment processing logic?

A:

- Data validation to make sure payment information are all valid
- Error handling on invalid payment requests / faulty payment process
- Multithreading to process multiple payment requests at a time

> Q: What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems,
> particularly in terms of interoperability with other technologies and platforms?

A:

gRPC as a communication protocol allows the creation of scalable, high-performance framework for efficient distributed system.
Opposed to REST, gRPC does away with manual HTTP configuration methods which eases interaction between modules.

> Q: What are the advantages and disadvantages of using `HTTP/2`, the underlying protocol for gRPC, compared to `HTTP/1.1` or `HTTP/1.1` with WebSocket for REST APIs?

A:

- Advantages:
  - Key features such as Request Multiplexing, Header Compression, and Server push which all collectively contribute to faster and more scalable communication between client and server
- Disadvantages:
  - More complex to set up compared to `HTTP/1.1` or `HTTP/1.1` with WebSocket

> Q: How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?

A: REST API is limited to `HTTP/1.1` which has the limitation of a single request before fetching a response from the server.
gRPC solves this with the use of `HTTP/2`, which has request multiplexing that lets it pack multiple requests and send them all at once to the server.
This allows gRPC to be more scalable and efficient in terms of real-time communication and responsiveness.

> Q: What are the implications of the schema-based approach of gRPC, using Protocol Buffers,
> compared to the more flexible, schema-less nature of JSON in REST API payloads?

A:

A fixed schema-based approach allows the system to validate data and improve processing speeds based on the already created schema.
It may require more effort to create the schema upfront, but a flexible, schema-less approach does not have the same luxury.
