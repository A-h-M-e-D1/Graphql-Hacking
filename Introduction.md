### What is GraphQL?

- GraphQL is described as an "open source data query and manipulation language for application programming interfaces (APIs)." Its primary purpose is to facilitate the exchange of information between two applications following a set of rules. Unlike other API formats like REST, GraphQL allows clients (consumers) to request only the specific data they need from a server, avoiding the transmission of unnecessary information.
----
### Key Features and Advantages:

- Specific Data Fetching

    - GraphQL allows clients to request only the data they need.
      -  This solves the over-fetching problem common in REST APIs (getting unnecessary data).

- Reduced Bandwidth Usage

    - Only the requested data is returned, reducing the amount of data transferred.

    - This improves performance, especially for mobile users on slow networks.

- Single Request for Complex Data

    - Clients can fetch complex and related data with a single request.
 
    - This solves the under-fetching problem in REST, where multiple requests are needed.

- Improved Performance

    - Less data and fewer requests lead to faster client-server interactions.

    - Result: a better user experience.

- Schema Stitching and Federation

    - GraphQL supports combining multiple GraphQL services into one unified schema.

    - This makes integration easier in microservices architectures.
----

### Origins and Maintenance:


  - GraphQL was developed by Facebook in 2012 for internal use.
     - Open Source Release

     - Facebook released GraphQL as open-source software in 2015.
 
    - In the same year, they also published the GraphQL specification and a reference implementation called GraphQL.js.

- Current Maintenance

    - GraphQL is now maintained by the GraphQL Foundation,

    - The foundation was created by several major global tech companies.

  
- Use Cases:
  

    - GraphQL can be used by almost any application or device.

    - Best Fit Scenarios

    - It is especially useful when clients need large amounts of information at once,

    - GraphQL avoids the inefficiency of making multiple REST API calls.

   - Adoption by Major Companies

     - Companies like Facebook, Atlassian, GitHub, and GitLab use GraphQL.

    - They serve millions of users across different platforms using it.

---    
### Core Components of a GraphQL Implementation:

- Schema

    - The schema defines what data a client can query.

    - Written using Schema Definition Language (SDL).

    - ncludes object types, fields, and relationships (edges) between objects.

    - Object types are the basic building blocks; they represent individual pieces of data.

    - Schemas look like a graph of interconnected nodes and edges.

    - Two-way links between nodes can sometimes cause Denial of Service (DoS) risks.

- Operations in GraphQL

    - GraphQL queries always start with a root operation type (Query, Mutation, or Subscription):

       -  Query: For read-only operations (fetching data).

       -  Mutation: For data manipulation (add, delete, modify).

      - Subscription: For real-time communication, usually over WebSockets.

- Schema Entry Point

    - The schema defines an entry point (e.g., a Query type with a users field).

    - Naming convention:

        - Object names (like User) start with an uppercase letter.

        - Field names (like users) are written in lowercase.

- Query Parser

    - When the server gets a query:

        - The query parser reads it, extracts the content, and checks it against the schema.

        - It then turns the query into an Abstract Syntax Tree (AST) for easier processing.

- Resolver Functions

    - Resolvers are functions that fetch the real data for each field requested.

   -  Data can come from databases, filesystems, or even other APIs (like REST).

   -  Resolvers are a critical area where vulnerabilities may exist.
---

### GraphQL vs. REST APIs (with a focus on security implications):

- Data Fetching

    - REST APIs:

       - Fixed data structures.

       - Clients often over-fetch and then filter the data.

    - GraphQL APIs:

        - Clients request only specific data they need.

        - Avoids over-fetching and under-fetching.

    - Security Implications:

        - GraphQL reduces information disclosure risks if properly implemented.

        - However, poorly written resolvers can introduce vulnerabilities.

- API Endpoints

    - REST APIs:

       - Multiple endpoints for different resources/actions.

    - GraphQL APIs:

      -  Single endpoint (e.g., /graphql).

    - Security Implications:

        - Single endpoint makes API enumeration easier.

        -  But it can simplify firewall rules if configured properly.

       - REST’s multiple endpoints allow granular access control.

- HTTP Request Methods

    - REST APIs:

      -  Uses various methods: GET, POST, PUT, DELETE.

    - GraphQL APIs:

        - Typically uses POST for all operations (queries, mutations, subscriptions).

       -  May also support GET for queries.

    - Security Implications:

        - POST for reads deviates from HTTP standards.

        - Supporting GET opens up possible CSRF vulnerabilities.

        - Traditional security tools tuned for REST might miss GraphQL-specific issues.

- HTTP Status Codes

    - REST APIs:

      -  Uses standard HTTP status codes (e.g., 200 OK, 404 Not Found, 401 Unauthorized).

    -  GraphQL APIs:

       - Mostly returns 200 OK, even when errors occur.

        - Errors are detailed inside the errors field in the response payload.

   - Security Implications:

        - Makes detecting attacks through status codes harder.

        - Can evade Web Application Firewalls (WAFs) or confuse security operators.

- Complexity

  -  REST APIs:

        - Complexity increases with more endpoints and relationships.

    - GraphQL APIs:

        - Complexity increases with schema stitching, federation, and deep relationships.

    - Security Implications:

       - More complexity = more potential vulnerabilities.

        - Deep GraphQL relationships can be abused for Denial of Service (DoS) attacks.
---
### Security Considerations Highlighted:
- Information Disclosure:

   - GraphQL reduces the risk of leaking sensitive data compared to REST because clients request only the data they need.

- Denial-of-Service (DoS) Attacks:

    - Two-way link relationships in the schema can be abused to cause DoS if not properly restricted (e.g., deep nesting).

- Vulnerabilities in Resolvers:

    - Poorly written resolver functions can introduce serious security vulnerabilities.

- HTTP Method Deviations:

    - Using POST for reads and supporting GET for queries can lead to issues like Cross-Site Request Forgery (CSRF) attacks.

- HTTP Status Code Differences:

    - GraphQL mostly uses 200 OK, even when errors occur.

   - Errors are provided inside the errors field, requiring custom security tools and log analysis.

- Complexity Vulnerabilities:

   - Complex GraphQL implementations (e.g., with schema stitching or federation) can increase the chances of introducing security flaws.

- Introspection Exposure:

    - GraphQL’s introspection feature (often exposed by tools like GraphiQL) can reveal the entire schema to attackers, helping them craft targeted attacks.

- Default Unauthenticated Servers:

    - GraphQL servers often start without authentication, allowing anyone to interact with the API.

   -  Proper authentication and authorization must be enforced at the server/API level.

---

### Interacting with GraphQL APIs

- Open-Source Libraries:

    - Clients can interact with GraphQL APIs using libraries like Apollo Client and Relay.

- Command-Line Tools:

     -   GraphQL queries can be sent using command-line HTTP clients like cURL.

- Graphical User Interfaces (IDEs):

    - Many GraphQL implementations provide GUIs such as GraphiQL Explorer and GraphQL Playground.

    - These tools offer helpful features like:

        - Auto-completion

        - Schema documentation

        - Error highlighting