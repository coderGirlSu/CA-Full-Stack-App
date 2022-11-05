# 💬TikTalk-documentation

## R1: Description of Website

### Purpose

The purpose of our application, TikTalk, is to allow users to communicate with one-another in a fast, efficient manner.

**Functionality/Features**

- Chat history
- User avatars
- File/Image uploads
- Download chat history

**Target Audience**

The TikTalk development team believes in building applications for everyone. Although we firmly believe that anyone can use our application and we aim to make it as accessible as possible, the typical end-user will probably be between the ages of 20 - 40 years old, and have good taste in chat applications. It will be free to use and likely to suit university students, families, colleagues, and friends alike!

**Tech Stack**

- MongoDB
- ExpressJS
- ReactJS
- Node.js
- JSON Web Tokens (Auth)

---

## R2: Dataflow Diagram

### Dataflow diagram

This diagram shows the dataflow for the chat application. There are three sections of dataflow, user flows, message flows and group flows.

![R2](docs/diagrams/Dataflow%20diagram.png)

### Sequence Diagram

#### User sign in

This diagram shows a user sending a POST request with their username and password to the Server. The Server sends the details to the Authentication Server to check the username and password. The Authentication Server will return a response containing a JWT and Refresh token or an error which will be returned to the Client from the Server.

![R2](docs/diagrams/client%20logon-%20sequence%20diagrams%20.png)

#### User POST message (authenticated)

When a user is signed in, a user can perform actions such as sending a message. This diagram shows a user sending a message. The client sends a POST request containing a message and JWT to the Server. The Server will authenticate the JWT by sending the JWT to the Authentication Server. If authenticated, the Server will store the message in the DB and confirm to the client.

![R2](docs/diagrams/%20client%20create%20a%20message-%20sequence%20diagrams.png)

#### User GET group message history (authenticated)

Every few seconds the client will poll the Server to get the latest message history for a group. The client sends a request containing a group ID with a JWT to the Server. The Server will authenticate the JWT with the Authentication Server. If authenticated, the Server will get group details from the DB and check if the user is part of the requested group. If the user is part of the group, the Server will get the group's message history from the DB and return it to the Client.

![R2](docs/diagrams/message%20history.png)

### Getting and using JWT

This diagram shows the user signing up. The client sends a POST request with the user information to the Server. The Server sends the user information to the Authentication server to create an account. Once the account has been created and the Server receives confirmation, the Server signs the user in and receives a JWT and refresh token for the new user. The Server then returns to sign up confirmation, JWT and refresh token to the Client.

The Client can then continue to send requests to the Server using the JWT.

![R2](docs/diagrams/getting%20and%20using%20an%20Application%20access%20token.png)

### Renew user JWT

This diagram shows how the Client can use the refresh token when the JWT expires. The Client sends a request to exchange the Refresh token for a new JWT to the Server. The Server forwards the refresh token to the Authentication Server and returns a response and a JWT. The Server then returns the new JWT to the client.

The client can the continue making API requests with the new JWT.

![R2](docs/diagrams/Refresh%20Tokens.png)

### Database ERD

There are 3 collections in the database for this application.

#### User collection

This collection contains document for each user, containing the following properties:

- display_name string: The display name in the app of the user
- created_date date: The date that the document was created
- deleted_date date: The date that the document was delete. Acting as a soft delete flag. If empty, the document has not been deleted.

#### Message collection

This collection contains a document for each message sent by a user, containing the following properties:

- message_id ObjectId: A unique identifier for the message
- message string: containing the message
- group_id ObjectId: containing the group ID that this message belongs to
- user_id ObjectId: containing the user ID for the user that sent the message
- created_date date: The date that the document was created
- deleted_date date: The date that the document was delete. Acting as a soft delete flag. If empty, the document has not been deleted.

#### Group collection

This collection contains a document for each group created by a user, containing the following properties:

- group_id ObjectId: A unique identifier for the group
- user_ids []ObjectId: An array of user IDs that belong to this group
- created_date date: The date that the document was created
- deleted_date date: The date that the document was delete. Acting as a soft delete flag. If empty, the document has not been deleted.

![R2](docs/diagrams/ERD.png)

---

## R3: Architecture Diagram

### Top level architecture diagram

This is a top level architecture diagram. The application runs on a MERN stack. The client will use React to make HTTP requests to an API server running Express on an AWS EC2 instance. Each request is authenticated against a Firebase authentication server. MongoDB is used as a backend database which runs as an Atlas DB cluster.

![R3](docs/diagrams/Top%20level%20architecture%20diagram.png)

### Detailed architecture diagram

This is a details architectural diagram of the application stack.

The client side part of the application is hosted on Netlify. This consists of CSS, HTML, Frontend libraries together with the web app developed using React.

The client communicates over HTTP requests to an Express backend running on an AWS EC2 instance. Requests are authenticated against Firebase running in Google Cloud. Once authenticated, data is retrieved from the database using Mongoose to create a abstraction model of the data.

The database is hosted in MongoDB's Atlas. It consists of a DB cluster containing 3 databases. One primary and two secondary servers to redundancy.

![R3](docs/diagrams/Detailed%20architecture%20diagram.png)

---

## R4: User Stories

### The first version of user stories

- As a user, I want to be able to register, log in and log out to the app, so that I can see and manage my own group or friends.

- As a user, I want to be able to send messages and receive messages, so that I can chat with my friends.

- As a user, I want to be able to create a group, so that I can chat with multiple friends at the same time.

- As a user, I want to be able to add friends to my groups so that I can chat with multiple friends at the same time.

- As a user, I want to be able to delete a group, so that I can manage group and keep the chat app tidy.

- As a user, I want to be able to leave a group, so that I no longer receive messages from that group.

- As a user, I want to be able to view message history, so that I can find some important information without lose it.

