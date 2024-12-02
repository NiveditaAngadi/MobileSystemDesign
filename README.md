# Mobile System Design
Provides the information about the Mobile System Design Interview

What are the expectations from this kind of Interview?
1. Ability to understand and solve complex problems
2. Communicate clearly and effectively
3. Having relevant experience and knowledge


To demonstrate "Ability to understand and solve complex problems", 
1. Think about the business part/impact.
2. Understand the vague requirements, ask the right questions to get clarify about requirements and technical decisions.
3. Ability to break the problem into smaller piece. Follow the top to bottom approach. Provide the context and the main conception first, and then using divide and conquer technics, gradually split the system to smaller and smaller pieces.

To exhibit clear communication,
1. Do not take a big pause, can communicate the design decisions clearly and precisely.
2. You can use white board to demonstarte/note down the design decisions and discuss.

For relevant expierence and knowledge, 
1. Have experience in the development of the huge mobile applications or better the whole client-server systems.
   - Server Communication Design (one-way, two-way, API design)
   - Pagination
   - Cache
   - State Management
   - Modularisation Technique
   - Design patterns, Pros and Cons
   - Problems and solutions for - State Mutation, Storing of the big images in the app, Overuse of Singleton and god objects.
2. Ability to foresee the problems or difficulties in the solution: Clear communication of the problems in the solution and possible options to solve it.
3. Have experience working with the different quality assurance and risk mitigation technique: How you test your design, blue-green deployments, fail fast etc.
4. Ability to design the modules on the class level - awarness of main principles and design patterns.  “How would you implement updating of the unread messages count label?” — you will need to decide will it be observer pattern or delegate or polling or whatever else it could be and draw the simple diagram.

Before start design
1. Gather as many requirements by asking relevant questions.
2. You should demonstarte your knowledge.
3. You shouldn't be silent, speak all the time, communicate clearly, don't wait for hints from an interviewer.
4. Always provide information about the alternatives and defend your choice.

## High Level Plan
1. Business Idea - What are you selling to end user (Data/service) 3-4 mins
   Service List and Data entities 
2. Requirement clarification - 1-2 mins
   Limitations and priorities list 
3. Designing of a mathematical model - 0-5 mins
   Formula(s), input and output 
4. High Level System Design - Define how to split that state and functionality between the server and the client side - 3-5 mins
   Scheme splitting backened and front end
5. API design - 7-10 mins
   API calls list, detailed data entities 
6. High level client side design (layered structure) - 4-5 mins
   Layered structure scheme
7. Module Design - Detailed design of the chosen module - 4-8 mins
   Functional scheme of the module
8. One complex/tricky case and detailed discussion - 5-10 mins
   Anything to visualise your ideas.

Possible System design questions:
1. Maintainability: are we designing MVP or PoC or full scale system? How big is the team which will implement my design?
2. Testability
3. Scalability/Performance: Cross platform? Limitations of the technology and compatible versions of the OS for platforms. Discuss the impact of third party libaries on performance, battery life etc. 
4. Security: Personal information storage in app, Pros and Cons, various method to store sensitive information.
5. Availability - Ability to work offline, limitation of OS version, phone/tablet choice, limitation of storage size, screen sizes etc.
6. High-Level System Design - What part of the services and the data should be implemented/stored on the server and what part should be implemented/stored on the mobile device.
7. Layers -
   - Business Layer,
   - Service Layer (Implementation of API's - interval Services Layer helps to isolate concrete implementations of the low level communication and persistent modules (Data Layer) from the Business Layer.), Business Layer shouldn’t bother about the place where we get the data from — persistent storage or communication channels, and what kind of SDK we use to implement audio/video calls. Another purpose of the Service Layer is to convert data from multiple formats to the one Business Layer is using.
   - Data layer - contains SDKs, frameworks, libraries that provide your application with such features like network communication, local DB access, logging, or, complete fully functional features like Audio/Video calls.
   - Presentation Layer - The main purpose of this layer is to prepare the data from Business Layer to be displayed to user in UI Layer.
   - UI layer -  It’s very platform specific layer where the business data, converted by the Presentation Layer, is being displayed on the device screen using OS SDKs.
     The second purpose of this layer is to interact with the user and pass all those interactions throughout the Presentation Layer to the Business Layer and further if needed.
     This layered design can be mapped to any concrete architecture patterns like MVC, MVI, Redux, VIPER, RIBs, etc, but it’s very important to remain on the higher level of abstraction at this step and not to go deeper to those concrete patterns.

8. Detail Design - Choose one module/feature, and define architecture pattern that suits it best in your opinion.
   Looks like Redux is a good option for the Business Layer + middleware as the Service Layer + MVP or MVVM or MVI patterns for the Presentation and UI layers with the Redux store playing the Model role. VIPER seems a bit excessive for just a few screens with minimum number of routes between them and RIBs is better suits very complex screens with many teams working on the same screen.
   you would have to to explain where store/state should be placed, how it should work, how we would implement subscription for state changes, how services should be used and how they will update the state.
   Advantage of Redux design:
   1. Maintainability: We fully decouple data receiving part (Data and Service Layer) and data consumer part (Presentation and UI Layer) using store with updates subscriptions, so it doesn’t matter from which source the data comes — from a persistent store or a network communication channel. It helps to change some parts of the app without impacting the others + reuse as much code as possible.
   2. Scalability: The store could have multiple subscribers out of the box, so Presenter of our chat feature will be triggered and will pass the latest changes to View in order to display them + Presenter of the top panel, for instance, will be triggered as well and will update the counter of the unread messages. Adding one more subscriber is easy.
   3. Testability
  

Mobile Architecture patterns: MVC, MVP, MVVM, MVI, VIPER, REDUX, etc. It would be good to know about them and about the conceptions behind each of them.
  

Reference:
https://artem-goncharov.medium.com/grokking-the-mobile-system-design-interview-6a06fa94491b
