# Product Architecture Documentation

## Product Choice
Product name: Telegram  
Website: https://telegram.org  

Telegram is a cloud-based messaging platform that allows users to exchange messages, media, and files with a strong focus on speed, scalability, and security.

## Main components

![Telegram Component Diagram](./diagrams/out/telegram/component-diagram/Component Diagram.svg)

[Component Diagram source](./diagrams/src/telegram/component-diagram.puml)

**Client Applications (Mobile / Desktop / Web)**  
Provide the user interface and handle user interactions such as sending messages, uploading media, and displaying chats.

**API Gateway**  
Acts as a single entry point for all client requests, handling authentication, request validation, and routing to backend services.

**Messaging Service**  
Processes, stores, and delivers messages between users, including message synchronization across devices.

**Media Storage Service**  
Stores and serves media files such as photos, videos, and documents uploaded by users.

**User & Authentication Service**  
Manages user accounts, login sessions, authentication tokens, and access control.

## Data flow

![Telegram Sequence Diagram](./diagrams/out/telegram/sequence-diagram/Sequence Diagram.svg)

[Sequence Diagram source](./diagrams/src/telegram/sequence-diagram.puml)

**Selected flow: Sending a message**

1. The user sends a message from the Client Application.  
2. The request is sent to the API Gateway with an authentication token.  
3. The API Gateway validates the request and forwards it to the Messaging Service.  
4. The Messaging Service stores the message and processes delivery.  
5. If the message contains media, the Media Storage Service is used.  
6. The message is delivered to the recipient’s client application.

**Data exchanged:**
- Client → API Gateway: message content, auth token  
- API Gateway → Messaging Service: validated message  
- Messaging Service → Media Storage Service: media upload/download  
- Messaging Service → Client: delivery status  

## Deployment

![Telegram Deployment Diagram](./diagrams/out/telegram/deployment-diagram/Deployment Diagram.svg)

[Deployment Diagram source](./diagrams/src/telegram/deployment-diagram.puml)

Telegram client applications run on user devices (mobile, desktop, web).  
Backend services such as the API Gateway, Messaging Service, Authentication Service, and Media Storage Service are deployed on distributed cloud servers behind load balancers to ensure scalability and high availability.

## Assumptions
- The Messaging Service is horizontally scalable and uses sharding to support millions of concurrent users.  
- Media files are stored in a distributed object storage system with replication for fault tolerance.  

## Open questions
- How is end-to-end encryption implemented and managed for secret chats?  
- What caching strategies are used to reduce latency for frequently accessed messages and media?
