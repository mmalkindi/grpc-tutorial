# GRPC Tutorial (Module 9: High Level Networking)

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

A: ...

> Q: What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems,
> particularly in terms of interoperability with other technologies and platforms?

A: ...

> Q: What are the advantages and disadvantages of using `HTTP/2`, the underlying protocol for gRPC, compared to `HTTP/1.1` or `HTTP/1.1` with WebSocket for REST APIs?

A: ...

> Q: How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?

A: ...

> Q: What are the implications of the schema-based approach of gRPC, using Protocol Buffers,
> compared to the more flexible, schema-less nature of JSON in REST API payloads?

A: ...
