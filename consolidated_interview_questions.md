# Interview Preparation Guide

## Table of Contents
- [JavaScript Fundamentals](#javascript-fundamentals)
- [Node.js](#nodejs)
- [Database & SQL](#database--sql)
- [Web Technologies & Protocols](#web-technologies--protocols)
- [Development Tools & Practices](#development-tools--practices)
- [System Design & Architecture](#system-design--architecture)
- [Coding Challenges](#coding-challenges)
- [Behavioral Questions](#behavioral-questions)

---

## JavaScript Fundamentals

### Core Concepts

**What is a closure?**
A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function's scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

**What is a callback?**
A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action. Callbacks can be passed into promise functions.

**What is a promise?**
A promise is an object that may produce a single value sometime in the future. A promise has three possible states: resolved (fulfilled), rejected, or pending.

**What is async/await?**
- `async` ensures the function returns a promise
- `await` suspends the function execution until the promise settles and then resumes with the promise result
- `await` does not work in top-level code (outside of modules)

**Variable Declarations: var, let, const**
- `var`: has function scope or global scope, can be redeclared and updated
- `let`: has block scope, can be updated but not redeclared in the same scope
- `const`: has block scope, cannot be updated or redeclared

**What is the Event Loop?**
The event loop is JavaScript's mechanism for handling asynchronous operations. It continuously checks the call stack and task queues (microtask and macrotask queues), executing callbacks when the call stack is empty.

**What is the microtask queue?**
The microtask queue holds tasks from promises and mutation observers. Microtasks are executed before macrotasks (setTimeout, setInterval) after the current script finishes.

**What is `this`?**
`this` refers to the context in which a function is executed. Its value depends on how the function is called (global context, object method, constructor, arrow function, etc.).

**What is destructuring?**
Destructuring is a syntax that allows you to extract values from arrays or properties from objects into distinct variables in a concise way.

**What is Object.freeze()?**
`Object.freeze()` makes an object immutable - you cannot add, delete, or modify its properties. However, it only performs a shallow freeze.

### React-Specific

**What is the difference between state and props?**
- **State**: Internal data managed within a component, mutable, triggers re-renders when changed
- **Props**: External data passed from parent to child components, immutable from the child's perspective

**Class Components vs Hooks/Context API**
Hooks provide a more functional approach to state management and lifecycle methods. Context API is useful for sharing state across components without prop drilling. Redux is better for complex state management with strict patterns, while Context API + Hooks work well for simpler applications.

**What is the importance of immutability in React?**
Immutability helps React efficiently detect changes and determine when to re-render components. It prevents unexpected side effects and makes debugging easier.

**Describe how a SPA in React works**
A Single Page Application loads a single HTML page and dynamically updates content without full page reloads. React manages the view layer, updating only the parts of the DOM that change using its virtual DOM diffing algorithm.

**Describe how React Router works and its benefits**
React Router enables client-side routing by mapping URLs to React components. Benefits include better user experience (no page reloads), browser history management, and the ability to create nested routes.

### Advanced Topics

**What is your favorite feature in JavaScript?**
ES6 features like arrow functions, destructuring, spread/rest operators, and array methods (map, filter, reduce) that enable functional programming patterns.

**Error Handling: try/catch**
The `try` statement allows you to define a block of code to be tested for errors while it is being executed. The `catch` statement allows you to define a block of code to be executed if an error occurs in the try block.

### Language Characteristics

**Is JavaScript a loosely or strictly typed language?**
JavaScript is a loosely typed language because you don't have to specify what type of information will be stored in a variable in advance. TypeScript adds static typing on top of JavaScript.

**Is JavaScript single-threaded or multi-threaded?**
JavaScript is single-threaded with one call stack and one memory heap. It executes code line by line before moving to the next line. However, it can handle asynchronous operations using the event loop and browser Web APIs (or Node.js runtime), which makes it appear concurrent.

**Is JavaScript an object-oriented programming language?**
JavaScript supports OOP principles but is prototype-based rather than class-based. With ES6, class syntax was added as syntactic sugar over the prototype chain, making it easier to work with OOP patterns.

**Object-Oriented Programming (OOP)**
OOP is a programming paradigm that relies on the concept of classes and objects. It emphasizes encapsulation, inheritance, and polymorphism.

---

## Node.js

### Core Concepts

**How does Node work?**
Node.js uses event-driven programming in conjunction with an asynchronous non-blocking I/O model. The event listener monitors functions and handles triggers via callback functions (event handlers) whenever a preset condition is met. The event loop manages the sequence of events.

**What is asynchronous non-blocking?**
Node is single-threaded, so only one callback can run at a time. Although it's single-threaded, it can delegate I/O operations to the OS kernel through the libuv library, allowing the system to handle multiple operations concurrently without blocking the main thread.

**What is libuv?**
Libuv is a C library that provides Node.js with the event loop, asynchronous I/O operations, and cross-platform compatibility. It handles the thread pool for file system operations and other async tasks.

**What is a Node Event Emitter?**
EventEmitter is a class that helps create a publisher-subscriber pattern in Node.js. With an event emitter, you can raise events from different parts of an application, and listeners will listen to the raised events and perform actions.

### When to Use Node

**How do you decide if Node is suitable for an app?**
Node is particularly suitable for:
- Real-time data exchange applications (chat apps, instant messaging)
- E-commerce apps that handle simultaneous requests in real-time and at scale
- Streaming applications (like Netflix) - Node efficiently handles streams
- API development - lightweight and fast
- Microservices architecture - highly scalable

**Examples of real-time data exchange:**
- Instant messaging and chat applications
- Collaborative editing tools
- Live dashboards and analytics
- Gaming servers

### Drawbacks and Solutions

**What are some drawbacks of using Node?**

1. **Callback Hell**: Callbacks can become so nested they're impossible to manage
   - **Solution**: Use Promises or async/await for cleaner asynchronous code

2. **CPU-Intensive Operations**: Node can struggle with heavy CPU resource usage
   - **Solution**: Use worker threads to run CPU-intensive operations in parallel
   - Worker threads enable multithreading in Node.js
   - Access via: `const worker = require('worker_threads')`
   - Note: Workers help with CPU-intensive JavaScript operations but don't improve I/O operations (Node's built-in async I/O is already efficient)

3. **API Instability**: Frequent changes and lack of backward compatibility
   - Developers may need to rewrite parts of code with each update

### Node vs Other Technologies

**Ruby on Rails vs Node**
- Ruby on Rails is easier to set up initially but less scalable
- RoR includes everything for a website project (logic, routing, applications) out of the box
- Node offers more flexibility and better performance for real-time applications

---

## Database & SQL

### PostgreSQL Concepts

**What is a primary key?**
A unique value that can identify each row in a table. No two rows can have the same primary key value, and it cannot be NULL.

**Why use an integer for a primary key instead of a string?**
- Keep indexes as small as possible for better performance
- Integers are faster to compare and sort
- Less storage space required
- Optimize indexes for your queries

**What is a foreign key?**
A foreign key is a field (or collection of fields) in one table that uniquely identifies a row in another table. It establishes a relationship between two tables.

**What are triggers?**
A trigger is a procedure that runs automatically in response to certain events in a SQL database (INSERT, UPDATE, DELETE). Triggers help ensure certain actions are completed regardless of which program or user makes changes to the data, such as maintaining audit logs.

### SQL Queries

**Sample JOIN Query:**
```sql
SELECT * 
FROM species AS s 
INNER JOIN (
    SELECT f.title, f.release_date, sf._id, sf.film_id, sf.species_id 
    FROM films AS f 
    INNER JOIN species_in_films AS sf ON f._id = sf.film_id 
    WHERE f.title = 'A New Hope'
) AS sfj ON s._id = sfj.species_id;
```

### Database Scaling

**How would you scale a database (both NoSQL and SQL)?**
- **Vertical scaling**: Increase server resources (CPU, RAM, storage)
- **Horizontal scaling (sharding)**: Distribute data across multiple servers
- **Read replicas**: Create copies of the database for read operations
- **Caching**: Use Redis or Memcached to reduce database load
- **Indexing**: Optimize queries with appropriate indexes
- **NoSQL specific**: Take advantage of built-in horizontal scaling features
- **SQL specific**: Partitioning tables, connection pooling

### Security

**SQL Injection Protection**
Never directly insert client-side inputs into SQL queries. Use:
- Parameterized queries/prepared statements
- ORM frameworks with built-in protections
- Input validation and sanitization
- Principle of least privilege for database users

---

## Web Technologies & Protocols

### HTTP & Network

**What is the difference between HTTP vs HTTPS?**
- **HTTP**: Hypertext Transfer Protocol - unencrypted communication
- **HTTPS**: HTTP Secure - encrypted using SSL/TLS certificates, protecting data in transit

**What are some other transfer protocols?**
- FTP (File Transfer Protocol)
- SMTP (Simple Mail Transfer Protocol)
- WebSocket (bidirectional communication)
- SSH (Secure Shell)
- TCP/IP (Transmission Control Protocol/Internet Protocol)

**What is TCP?**
A connection-oriented protocol that creates a reliable connection between client and server through a three-way handshake using IP packets. Once connected, computers can freely send data. Connections can timeout after a specific period of inactivity.

**HTTP Status Codes:**
- **200**: OK - successful request
- **400**: Bad Request - malformed request syntax
- **401**: Unauthorized - authentication required
- **404**: Not Found - resource doesn't exist
- **500**: Internal Server Error - server-side error

**REST API Request Types:**
- **GET**: Retrieve data from server
- **POST**: Send data to server (creates new resource, causes state change)
- **PUT**: Replace all current representations of the target resource
- **PATCH**: Partial modification of a resource
- **DELETE**: Remove resource from server
- **HEAD**: Same as GET but returns only headers, no response body

### GraphQL vs REST API

**Why would you use GraphQL over REST API?**
- Single endpoint vs multiple endpoints
- Request exactly the data you need (no over-fetching or under-fetching)
- Strongly typed schema
- Better for complex, nested data structures
- Built-in introspection and documentation
- Reduces number of network requests

### System Architecture

**What is a reverse proxy?**
A reverse proxy represents the server to the client. Client requests go to the reverse proxy first. Benefits include:
- Filter out unwanted requests
- Cache HTML content
- Load balancing - distribute load between multiple servers
- SSL termination
- Security layer

**What is a rate limiter?**
A mechanism that controls the rate of requests a user/client can make to an API within a specific time window. Important for:
- Preventing API abuse and DDoS attacks
- Ensuring fair resource usage
- Protecting server resources
- Maintaining service quality

**Design a rate limiter that resets every four seconds:**
```javascript
class RateLimiter {
  constructor() {
    this.counter = 0;
    this.windowStart = Date.now();
    this.windowSize = 4000; // 4 seconds
  }
  
  allowRequest() {
    const now = Date.now();
    if (now - this.windowStart >= this.windowSize) {
      this.counter = 0;
      this.windowStart = now;
    }
    this.counter++;
    return true; // or implement max limit check
  }
}
```

### IP Addresses

**How many characters are in an IP address?**
IPv4: 7-15 characters (e.g., 192.168.1.1)
IPv6: Up to 39 characters (e.g., 2001:0db8:85a3:0000:0000:8a2e:0370:7334)

**Where do you get the IP address?**
- Assigned by DHCP server on local network
- ISP assigns public IP addresses
- DNS resolution for domain names
- Can be obtained programmatically via network APIs

---

## Development Tools & Practices

### Build Tools

**What is webpack?**
Webpack is a module bundler that takes all JavaScript files and dependencies and bundles them into a single, minified file that's optimized for quick serving to browsers.

**What does Babel do?**
Babel is a JavaScript transpiler that converts modern JavaScript (ES6+) into backwards-compatible ES5 syntax for older browsers.

**What is ESLint?**
ESLint is a linting tool that analyzes code for potential errors, enforces coding standards, and helps maintain code quality and consistency.

### CSS

**What is a CSS preprocessor? Pros & Cons**
SASS (Syntactically Awesome Style Sheets) is a preprocessor that compiles into CSS. SassScript is the scripting language while SCSS is the main syntax building on top of CSS.

**Pros:**
- Variables, nesting, mixins
- Better code organization
- Reusable code components

**Cons:**
- Requires compilation step
- Additional tooling complexity
- Learning curve

**What are mixins in CSS?**
Mixins are reusable blocks of CSS declarations that can be included in multiple selectors, allowing for DRY (Don't Repeat Yourself) code.

**What is Flexbox?**
A one-dimensional layout model that offers space distribution between items in an interface and powerful alignment capabilities along a single axis (row or column).

**Why use Grid over Flexbox and vice versa?**
- **Grid**: Two-dimensional layouts (rows AND columns), better for overall page structure
- **Flexbox**: One-dimensional layouts, better for component-level layouts and alignment
- Use Grid for macro layouts, Flexbox for micro layouts

**Why use semantic HTML?**
- Improves accessibility for screen readers
- Better SEO (search engines understand content structure)
- More maintainable and readable code
- Establishes clear document structure
- Helps with responsive design

### Testing

**What is TDD and your experience with testing suites?**
Test-Driven Development involves writing tests before writing code. Common testing frameworks:
- **Jest**: JavaScript testing framework with built-in mocking
- **Mocha**: Flexible test framework
- **Chai**: Assertion library
- **Enzyme/React Testing Library**: React component testing

**What's the difference between isolated testing and network testing?**
- **Isolated (Unit) Testing**: Tests individual functions/components in isolation, mocking dependencies
- **Network (Integration) Testing**: Tests actual network requests and API interactions
- In Jest: Use `jest.mock()` for isolated tests, use actual endpoints for network tests

### Version Control

**Git Commands:**
```bash
git init                              # Initialize repository
git add <file> or git add .          # Stage files
git commit -m "message"               # Commit changes
git clone <url>                       # Clone repository
git status                            # Check status
git remote add origin <server>        # Add remote
git remote -v                         # List remotes
git checkout -b <branch>              # Create and switch to branch
git branch                            # List branches
git merge <branch>                    # Merge branch
git pull                              # Fetch and merge
git push                              # Push to remote
```

### Docker

**Docker Commands:**
- `docker exec`: Run command in running container
- `docker cp`: Copy files between container and local filesystem
- `docker create`: Create new container
- `docker container`: Manage containers
- `docker config`: Manage Docker configs
- `docker image`: Manage images
- `docker ps`: List running containers
- `docker build`: Build image from Dockerfile
- `docker run`: Create and start container

**Why use Docker?**
- Consistent development environments
- Isolation and containerization
- Easy deployment and scaling
- Dependency management

### TypeScript

**Why would you use TypeScript?**
- Static typing catches errors at compile time
- Better IDE support (autocomplete, refactoring)
- Improved code documentation
- Easier maintenance and refactoring
- Better for large-scale applications
- Optional - can gradually adopt

**Reasons against TypeScript:**
- Additional complexity and learning curve
- Longer setup time
- Compilation step required
- May be overkill for small projects

### CI/CD & DevOps

**Technologies to Review:**
- Travis CI/CD: Continuous integration and deployment
- Redis: In-memory data structure store (caching, sessions)
- Redux: State management library
- Passport.js: Authentication middleware
- Bcrypt: Password hashing library
- Chart.js: Data visualization
- AWS Services: EC2 (compute), IAM (identity), RDS (database), S3 (storage), EBS (block storage)

### Development Patterns

**Design Patterns:**

**Singleton Pattern**
Used when you need exactly one instance of a class (e.g., database connection, configuration manager). Ensures a class has only one instance and provides global access point.

**Factory Pattern**
Creates objects without specifying exact class to create. Useful when creation logic is complex or needs to be centralized.

**Prototype Pattern**
Creates new objects by cloning existing ones. Useful when creating objects is expensive.

### Anti-Patterns to Avoid

- Global variables (namespace pollution)
- Using strings in setTimeout/setInterval instead of callback functions
- Deeply nested callbacks (callback hell)
- Not handling errors properly
- Direct DOM manipulation in React
- Mutating state directly

---

## System Design & Architecture

### Event-Driven Architecture

**What is event-driven programming?**
A programming paradigm where program flow is determined by events (user actions, messages, sensor outputs). Event listeners wait for events and trigger corresponding event handlers.

**Drawbacks of event-based architectures (Kafka):**
- Complexity in debugging and tracing
- Eventual consistency challenges
- Potential message ordering issues
- Overhead of message broker infrastructure
- Harder to understand system flow

### MVC Pattern

**What is MVC (Model-View-Controller)?**
An architectural pattern that separates an application into three interconnected components:
- **Model**: Data and business logic
- **View**: User interface and presentation
- **Controller**: Handles user input and updates model/view

### Microservices

**Benefits:**
- Independent deployment and scaling
- Technology flexibility
- Fault isolation
- Easier to understand and maintain small services
- Team autonomy

### Architecture Questions

**Name a time when you designed an integrated system**
Discuss system components, how they communicate, data flow, scaling considerations, and trade-offs made.

**Vue vs React**
- Vue: Gentler learning curve, template-based, all-in-one framework
- React: JSX syntax, larger ecosystem, more flexible, component-based

### Optimization

**If your website is slow, how do you optimize it?**
- Reduce HTTP requests
- Use vanilla JS when possible (avoid unnecessary libraries)
- Optimize images (compression, lazy loading, appropriate formats)
- Minify CSS/JS
- Use CDN for static assets
- Implement caching strategies
- Code splitting and lazy loading
- Database query optimization
- Use production builds

---

## Coding Challenges

### Algorithms

**Binary Search**
Search algorithm that finds the position of a target value in a sorted array by repeatedly dividing the search interval in half. O(log n) time complexity.

**Problems to Practice:**

1. **Merge K sorted arrays**
2. **Merge ranges/intervals**
3. **Calculate mode/mean of dataset**
4. **Shifted binary search traversal** (each layer is right side of tree)
5. **Factorial with memoization** (save previously computed values)
6. **Reverse vowels in a string**
7. **Maximum perimeter triangle from array of integers**

### Data Structures

**Implement a Stack with min() method**
Create a stack that returns minimum value in O(1) time. Use auxiliary stack to track minimums.

**Array/String Problems:**

- Parse stock tickers "APL|400" and return top N by sales
- Traverse matrix and print elements in reverse
- Given departure/arrival times, find minimum gates needed

### Advanced Problems

**Calendar Availability**
Given unordered list of busy times, find intervals when ALL people are available.

**Log Analysis**
Given unsorted web access logs (access time, user ID, resource ID), find resource with highest accesses in any 5-minute window.

**Safe Function Wrapper**
Wrap an error-prone function to return error message without crashing program.

**Line Overlap Problems**
1. Determine if two lines overlap (1D: x, width)
2. Return new line representing overlap
3. Extend to 2D boxes (x, y, width, height)
4. Find overlap of any number of 2D boxes

**Keyword Balancing**
Given pairs of keywords (like HTML tags) and a string, verify keywords are properly balanced.

**DOM Manipulation**
Implement Tag class with:
- getName() method
- addClass() method
- getClassName() method
- appendChild() method
- getChildren() method

### Event Handling

**onClick Event Propagation**
If an HTML page has onClick on body tag and button inside body also has onClick, clicking the button triggers:
1. Button's onClick (target phase)
2. Bubbles up to body's onClick (bubbling phase)
Use `event.stopPropagation()` to prevent bubbling.

---

## Behavioral Questions

### Technical Challenges

- What's the hardest technical challenge you've encountered?
- Describe a technical challenge in your most recent project
- Tell me about a time something didn't work and you had to start over
- Walk me through a piece of code you've written recently
- Describe a difficult piece of tech you've learned in layman's terms

### Team & Collaboration

- Tell me about your development team structure
- Tell me about your experience working in cross-functional teams (data, frontend, backend, product, business, customers)
- Tell me about a conflict with your team and how you resolved it
- How do you help team members develop their careers/invest in their skills?
- What's your approach to mentoring junior developers?
- What do you look for when doing code reviews?
- You mentioned user stories, how did you divide tasks regarding features?

### Agile & Process

- Talk about your experiences with Agile/Scrum
- What's your experience with agile development? How long were your sprints?
- How do you decide if a feature/epic should go into the next sprint?
- How do you determine which tools to use?

### Decision Making & Problem Solving

- Tell me about a time you had to turn a business requirement into a product feature
- If you worked for me and I called you in the middle of the night to say the app was down, what would be your first step to debug?
- How do you decide if Node is suitable for an app?
- Tell me about a time you faced tight deadlines and didn't have time to consider all options
- Tell me about a time you disagreed with your manager on something important to the business
- Tell me about a time you got pushback from a manager and how you worked through it

### Product & User Focus

- Tell me about a time you've put the customer first
- What kind of usability did you take into account for users?
- Why is accessibility important?
- Why are your projects all open-source?
- How many active users does your developer tool have?

### Self-Reflection & Growth

- Give me a sense of your background
- Tell me about a time you failed to meet a commitment
- What is a weakness you are working on?
- What is a weakness you are not working on?
- Tell me about a goal you set that would take significant time and you're still working towards
- Tell me about a time you took a big risk and failed
- Tell me about a time you took on something significant outside your area of responsibility
- Tell me about a time you've given back to others or your community

### Company Fit

- What are the top three things you look for in a company?
- Why did you leave your current role/company?
- What can you contribute to the company you're applying to?
- Why you? Your experience is so short and limited. Why you?
- What is it about your personality that makes you think you'd be a good fit at this company?

### Technical Decisions

- If you were to create a startup, would you use Redux or React Hooks?
- What state management library do you prefer and why?
- Why use Node over another technology like Rails, Java/Spring, or Django?
- What is your favorite dev tool and why?
- Why use a Node VM2 instead of simply using a Docker container?
- When would it be a good time to implement Context API as opposed to Redux?
- Do you prefer React class components or hooks/Context API for state management, and why?

### Project & Architecture

- Tell me about something you have built and walk me through the components/system design
- What are some ways your tool could be further optimized?
- Do you have any experience with user authentication/security?
- Walk me through every step in a to-do list after clicking the checkbox that a task is completed

### Performance & Quality

- What measures have you put in place to ensure performance improvement targets and standards are achieved?
- How do you determine potential in team members?
- Why does it look like you have fewer commits on this project compared to others?

---

## Additional Topics to Review

- Regex (Regular Expressions)
- GraphQL caching mechanisms
- Advanced Redux patterns
- WebSockets for real-time communication
- Service Workers and PWAs
- OAuth and JWT authentication
- Kubernetes basics
- Message queues (RabbitMQ, Kafka)
- Monitoring and logging (DataDog, Sentry)
- Performance profiling tools
