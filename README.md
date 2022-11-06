# 💬 TikTalk-documentation 🎃

## R1: Description of Website

### Purpose

The purpose of our application, TikTalk, is to allow users to communicate with one-another in a fast, efficient manner.

**Functionality/Features**

- Chat History
- User Avatars
- File/Image Uploads
- View Chat History
- User Sign up, Sign in, Sign out
- Add User to Group
- Remove User from Group
- Create Group
- Leave Group
- Play a sound effect when receiving new messages

**Target Audience**

The TikTalk development team believes in building applications for everyone. Although we firmly believe that anyone can use our application and we aim to make it as accessible as possible, the typical end-user will probably be between the ages of 20 - 40 years old, and have good taste in chat applications. It will be free to use and likely to suit university students, families, colleagues, and friends alike!

**Tech Stack**

Front-end: HTML5, CSS3, REACT.JS, Javascript, JSX

Back-end: Node, ExpressJS

Database: MongoDB, Mongoose

Deployment: Back-end: AWS EC2, Front-end: Netlify, Database: Atlas

Testing: Jest

Project-management tools: Trello, Discord

Utilities: Draw.io, Balsamic, WebSequenceDiagrams

DevOps: Git, GitHub, VS Code, Postman

---

## R2: Dataflow Diagram

### Dataflow diagram

This diagram shows the dataflow for the chat application. There are three sections in the dataflow diagram, user flows, message flows and group flows.

![R2](docs/diagrams/Dataflow%20diagram.png)

### Sequence Diagram

#### User sign in

This diagram shows a user sending a POST request with their username and password to the Server. The Server sends the details to the Authentication Server to check the username and password are correct. The Authentication Server will return a response containing a JWT and Refresh token or an error which will be returned to the Client from the Server.

![R2](docs/diagrams/client%20logon-%20sequence%20diagrams%20.png)

#### User POST message (authenticated)

When a user is signed in, a user can perform actions such as sending a message. This diagram shows a user sending a message. The client sends a POST request containing a message and JWT to the Server. The Server will authenticate the JWT by sending the JWT to the Authentication Server. If valid, the Server will store the message in the DB and confirm success to the client.

![R2](docs/diagrams/%20client%20create%20a%20message-%20sequence%20diagrams.png)

#### User GET group message history (authenticated)

Every few seconds the client will poll the Server to get the latest message history for a group. The client sends a request containing a group ID with a JWT to the Server. The Server will authenticate the JWT with the Authentication Server. If valid, the Server will get group details from the DB and check if the user is part of the requested group. If the user is part of the group, the Server will get the group's message history from the DB and return it to the Client.

![R2](docs/diagrams/message%20history.png)

### Getting and using JWT

This diagram shows the user signing up. The client sends a POST request with the user information to the Server. The Server sends the user information to the Authentication Server to create an account. Once the account has been created and the Server receives confirmation, the Server signs the user in and receives a JWT and Refresh token for the new user. The Server then returns the sign up confirmation, JWT and refresh token to the Client.

The Client can then continue to send requests to the Server using the JWT.

![R2](docs/diagrams/getting%20and%20using%20an%20Application%20access%20token.png)

### Renew user JWT

JWTs are short-lived, meaning that they expire after a few minutes to increase app security. This diagram shows how the Client can use the Refresh token when the JWT expires. The Client sends a request to exchange the Refresh token for a new JWT to the Server. The Server forwards the Refresh token to the Authentication Server and returns a response and a JWT. The Server then returns the new JWT to the client.

The client can then continue making API requests with the new JWT.

![R2](docs/diagrams/Refresh%20Tokens.png)

### Database ERD

The database for this application is non-relational. There are 3 collections in the database for this application.

#### User collection

This collection contains documents for each user, containing the following properties:

- display_name string: The display name in the app of the user
- created_date date: The date that the document was created
- deleted_date date: The date that the document was delete. Acting as a soft delete flag. If empty, the document has not been deleted.

#### Message collection

This collection contains a document for each message sent by a user, containing the following properties:

- message_id ObjectId: A unique identifier for the message
- message string: containing the message that was sent
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

The client communicates over HTTP requests to an Express backend running on an AWS EC2 instance. Requests are authenticated against Firebase running in Google Cloud. Once authenticated, data is retrieved from the database using the Mongoose library to create a abstraction model of the data.

The database is hosted in MongoDB's Atlas. It consists of a DB cluster containing 3 databases. One primary and two secondary servers for redundancy.

![R3](docs/diagrams/Detailed%20architecture%20diagram.png)

---

## R4: User Stories

### User stories

- As a user, I want to be able to register, sign in and sign out to the app, so that I can see and manage groups and friends.

- As a user, I want to be able to send messages and receive messages, so that I can chat with my friends.

- As a user, I want to be able to create a group, so that I can chat with multiple friends at the same time.

- As a user, I want to be able to add friends to my groups so that I can chat with multiple friends at the same time.

- As a user, I want to be able to delete a group, so that I can manage groups and control access to conversations.

- As a user, I want to be able to leave a group, so that I no longer receive messages from that group.

- As a user, I want to be able to view message history, so that I can find previous relevant messages.

### User stories revision

- As a user, I want to be able to access the chat app on a mobile device and desktop device, so that I can access the device wherever it is convenient, whatever device I have.

- As a user, I want to be able to access the chat app on any operating system, so that I am not restricted in accessing the app.

- As a user, I want to have the choice of light and dark mode on the app, so that I can choose my user experience

- As a user, I want the app the be Halloween themed so that it appeals to young people.

- As a user, I want the app the play a sound when I receive new messages, so that I am alerted and don't need to keep checking the app.

---

## R5: Wireframes

This chat application will feature light and dark mode. The dark mode is a halloween-based theme, and the light mode is a combination of light colours. The application will originally be loaded in the dark mode format for spooky halloween goodness 🎃.


### Sign Up, Login, Chats, and Show Chat Mobile (Dark Mode)

- On the **Sign Up** page, users will create an account with a username, email and encrypted password. They can upload an avatar as well. At the bottom, they have the option to sign in if they already have an account.

- The **Login** page is similar, but users will only need to enter their username and password in order to log in.

- Once the user is signed up or logged in, they'll be taken to their **Chats (Show Chat)** page. This will show all their individual and group chats. This is exclusively for the *mobile* and *tablet* views of the application. The *desktop* version will have Chats in a Sidebar, as will be seen below.

- From there the user will be able to click through to the **Chat** page, which will show an individual chat or group chat.

- Users can toggle light and dark mode from the bottom of the page, except on the invididual chat screen, where it would be a little impractical as it could accidentally be touched.

![R5](./docs/wireframes/Login%2C%20Sign-Up%2C%20Chats%2C%20Show%20Chat%20MOBILE%20DARKMODE.png)

### Sign Up, Login, Chats, and Show Chat Mobile (Light Mode)

- All of the functionality is the same on the *mobile* view. Users will log in or sign up, then progress to their Chats and Group Chats page, then to the individual chats page. The only difference is the light mode colour scheme.

- Users can toggle light and dark mode from the bottom of the page, except on the invididual chat screen, where it would be a little impractical as it could accidentally be touched.

![R5](./docs/wireframes/Login%2C%20Sign-Up%2C%20Chats%2C%20Show%20Chat%20MOBILE%20LIGHTMODE.png)

### Sign Up, Login, Chats, and Show Chat Tablet (Dark Mode)

- The pages in *tablet* view are very similar to the *mobile* pages in terms of their layouts. As is fitting for tablets, the pages have slightly more space. The users log in or sign up, then progress to their Chats page to show individual/group chats, then progress on to those chats to interact.

- Users can toggle light and dark mode from the bottom of the page, except on the invididual chat screen, where it would be a little impractical as it could accidentally be touched.

![R5](./docs/wireframes/Login%2C%20Sign-Up%2CChats%2C%20Show%20Chat%20Tablet%20DARKMODE.png)

### Sign Up, Login, Chats, and Show Chat Tablet (Light Mode)

- Light mode for tablet view is the same as dark mode view, except the colour scheme has changed.

- Users can toggle light and dark mode from the bottom of the page, except on the invididual chat screen, where it would be a little impractical as it could accidentally be touched.

![R5](./docs/wireframes/Login%2C%20Sign-Up%2CChats%2C%20Show%20Chat%20Tablet%20LIGHTMODE.png)

### Sign Up Page Desktop (Dark Mode)

- The **Sign Up** page on *desktop* is very similar to the *mobile* and *tablet* views, just with more space. This is the darkmode theme.

- Users can toggle light/dark mode from the bottom of the page.

![R5](./docs/wireframes/Sign%20Up%20Desktop%20DARKMODE%20copy.png)

### Sign Up Page Desktop (Light Mode)

- The **Sign Up** page in light mode has all the same features as darkmode in *desktop*, *mobile* and *tablet* views, just a different colour scheme.

- Users can toggle light/dark mode from the bottom of the page.

![R5](./docs/wireframes/Sign%20Up%20Desktop%20LIGHTMODE.png)

### Log In Page Desktop (Dark Mode)

- **Log In** on *desktop* is the same as *mobile* and *tablet* views, just with more space. This is darkmode.

- Users can toggle light/dark mode from the bottom of the page.

![R5](./docs/wireframes/Login%20Desktop%20DARKMODE.png)

### Log In Page Desktop (Light Mode)

- And lightmode:

![R5](./docs/wireframes/Login%20Desktop%20LIGHTMODE.png)

### Chat Page Desktop (Dark Mode)

- The *desktop* variety of the application will have a cruicial difference to the *mobile* and *tablet* views. Because it has the most space, it will **not** have an individual **Chats** page. Because it has the most space, it will have the **Chats** page embedded as a sidebar on the **Chat** page. Here is darkmode.

- Users can toggle light/dark mode from the top right corner of the page.

![R5](./docs/wireframes/Chat%20Desktop%20DARKMODE.png)

### Chat Page Desktop (Light Mode)

- And lightmode:

![R5](./docs/wireframes/Chat%20Desktop%20LIGHTMODE.png)

---

## R6: Trello Screenshots

This is a link to our trello workspace:

https://trello.com/b/rhCwvSGR/tiktalk 

And a link to all trello screenshots. All are labelled with dates and descriptions.

[Trello](./docs/trello-screenshots/)

### Added some back-end and front-end cards 26:10:22

![R6](./docs/trello-screenshots/added%20back-end%20and%20front-end%20cards%2026%3A10%3A22.png)

### Added difficulty level and task numbers 21:10:22

![R6](./docs/trello-screenshots/added%20difficulty%20level%20and%20task%20numbers%2021%3A10%3A22.png)

### Added git workflow check list 12:12:23

![R6](./docs/trello-screenshots/Added%20git%20workflow%20check%20list%2012%3A12%3A23.png)

### Added front-end components in trello 26:10:22

![R6](./docs/trello-screenshots/added%20front-end%20components%20in%20trello%2026%3A10%3A22.png)

### Added more feature ideas and moved criteria to check column 21:10:22

![R6](./docs/trello-screenshots/added%20more%20feature%20ideas%20and%20moved%20criteria%20to%20check%20column%2021%3A10%3A22.png)

### Decided app name 13:00:01

![R6](./docs/trello-screenshots/Decided%20app%20name%2013%3A00%3A01.png)

### Added numbering system to project items, more items complete 6:11:22

![R6](./docs/trello-screenshots/added%20numbering%20system%20to%20project%20items%2C%20more%20items%20complete%206%3A11%3A22.png)

### Added some cards to doing column, final updates to README 4:11:22

![R6](./docs/trello-screenshots/added%20some%20cards%20to%20doing%20column%2C%20final%20updates%20to%20README%204%3A11%3A22.png)

### Allocated front-end and back-end, made cards for marking criteria 21:10:22

![R6](./docs/trello-screenshots/allocated%20front-end%20and%20back-end%2C%20made%20cards%20for%20marking%20criteria%2021%3A10%3A22.png)

### Completing wireframes and aspects of readme 1:11:22

![R6](./docs/trello-screenshots/completing%20wireframes%20and%20aspects%20of%20readme%201%3A11%3A22.png)

### Decided on scss to keep front end tidy; colour variables card added 1:11:22

![R6](./docs/trello-screenshots/decided%20on%20scss%20to%20keep%20front%20end%20tidy%3B%20colour%20variables%20card%20added%201%3A11%3A22.png)

### Front-end practice for part b 1:11:22

![R6](./docs/trello-screenshots/front-end%20practice%20for%20part%20b%201%3A11%3A22.png)

### More assigning of person, difficulty and task numbers 21:10:22

![R6](./docs/trello-screenshots/more%20assigning%20of%20person%2C%20difficulty%20and%20task%20numbers%2021%3A10%3A22.png)

### Project setup 21:10:22

![R6](./docs/trello-screenshots/project%20setup%2021%3A10%3A22.png)

### Wireframes and delegating front-and-back end done 1:11:22

![R6](./docs/trello-screenshots/wireframes%20and%20delegating%20front-and-back%20end%20done%201%3A11%3A22.png)

### Working on first half of readme1 21:10:22

![R6](./docs/trello-screenshots/working%20on%20first%20half%20of%20readme1%2021%3A10%3A22.png)

### Assign tasks to person based on front-end and back-end 1:00:13

![R6](./docs/trello-screenshots/Assign%20tasks%20to%20person%20based%20on%20front-end%20and%20back-end%201%3A00%3A13.png)

### Added more must to have features and nice to have features 1:15:04

![R6](./docs/trello-screenshots/Added%20more%20must%20to%20have%20features%20and%20nice%20to%20have%20features%201%3A15%3A04.png)