Resources - https://aakashgupta.medium.com/system-design-for-product-managers-8557aa4b7646
https://www.news.aakashg.com/p/system-design-interview?utm_source=medium
https://www.youtube.com/watch?v=iiR6DY1w3jI

System design interviews for engineers are about how to build. For PMs, they’re about why and what to build.
Understand how the underlying systems tie together, why they are used and tradeoffs; everything should support user needs and business goals

DNS(Domain Naming Service) - It is like phonebook of the internet
When you type in a website name(like google.com), the browser checks with DNS to find IP address for that website. The DNS returns the IP address and the browser then sends a GET request to that IP address, requesting the landing page. (POST request when you are sending data). A web service(such as Apache) catches this request and forwards the request to the backend. The backend server reads the URL path/talk to database if needed, and then frames the response in json/html. The backend sends the response to the browser through web server. The browser then renders the page. 
GET - Viewing/searching something	Asks the server to give you data
POST - Submitting forms/saving data	Sends data to the server

Example:
GET: “Can I see the product list?”
POST: “Here’s my order details, please save them.”

An API endpoint is just a specific URL path that lets your system talk to another system.
For example:
https://myshop.com/api/products is an endpoint where:
GET shows the product list
POST adds a new product

Scaling a system means being able to handle more users(traffic), more data(storage), more requests per second(performance).

Scaling server - 
Vertical scaling can be done only to a certain point after that we move to horizontal scaling - adding more commodity servers. Load Balancers are used to spread incoming traffic(load) evenly across servers. Trade-offs -  Adds complexity, but increases reliability; Must ensure stateless servers or use sticky sessions. When using load balancer, the DNS gives the IP address of the load balancer which then sends the request to the appropriate server. 

Scaling database - If all the requests go to a single database, the database can face issues and so we replicate it to safeguard against such issues and ensure data availability at all times. 
We make primary and secondary database. Primary is for writing data and secondary for read requests. 

Another way to improve performance of database is to put a cache in between. A cache is a high-speed storage layer—usually in memory (like RAM)—that temporarily holds frequently accessed data so future requests can be served faster. In most systems, the cache layer sits between the application and the database. When a user requests data, the app checks the cache (usually Redis or Memcached) first. If found, it avoids a slower database call. This setup improves speed, reduces DB load, and helps scale the system efficiently. Example - Redis

Two Main Types of Scaling
1. Vertical Scaling (Scaling Up)
What it is: Add more CPU, memory, or storage to a single database server.

Analogy: Upgrading your laptop to have more RAM and a faster processor.

Pros: Easy to implement.

Cons: Expensive and has hardware limits (can’t scale infinitely).

🟡 Useful for early-stage products with low to moderate traffic.

2. Horizontal Scaling (Scaling Out)
What it is: Add more servers to share the load across multiple machines.

Analogy: Hiring more chefs in a kitchen instead of making one chef faster.

Pros: Better for handling high traffic and large datasets.

Cons: More complex setup and maintenance.

🚦 Techniques for Horizontal Scaling
✅ 1. Read Replicas (Replication)
What it is: Create copies of your database that can only be read from, not written to.

Why it's useful: Offloads read traffic (e.g., product browsing, profile views).

Example: Writes go to master DB, reads go to replicas.

🧠 Trade-off: Replicas may be eventually consistent (a slight delay in data updates).

✅ 2. Sharding (Partitioning)
What it is: Split the database into smaller chunks called shards, each holding part of the data.

Example: Users with IDs 1–1000 on one shard, 1001–2000 on another.

Why it's useful: Allows parallel storage and querying.

🧠 Trade-off:

Complex to design and maintain

Cross-shard queries are harder and slower

✅ 3. Caching (Offload the DB)
What it is: Use in-memory cache (e.g., Redis) to serve frequently accessed data.

Why it's useful: Prevents repetitive DB hits for things like user profiles, product pages.

🧠 Trade-off: Must manage cache invalidation to avoid showing outdated data.


We shard the database to split the data across multiple servers—for example, by region or user group. Then, we add read replicas to each shard to offload read traffic. This allows us to scale both in terms of data size and query volume. It’s common in systems with millions of users or global operations, like social media platforms or e-commerce.

CDN - A Content Delivery Network (CDN) is a system of servers distributed across different locations (called edge locations) that store cached copies of static content like Images, CSS & JavaScript files, Videos, Fonts, PDFs
💡 Think of it like having mini warehouses of your most popular products spread across the globe so customers get them faster.

A CDN sits between users and your main server. It stores and delivers cached static content from edge servers closer to the user. This reduces latency, improves performance, and lowers the load on your application. Browser requests an image/script/page.
CDN checks if it has it cached at a nearby edge location:
✅ Hit → Return content instantly.
❌ Miss → Fetch from origin server → Cache it for next time.

Flow --
The browser contacts DNS to resolve the domain name.
DNS returns the IP address of the CDN edge server, not your origin/load balancer yet.
The CDN edge server (e.g., Cloudflare, Akamai) checks if it has a cached copy of the requested file (e.g., images, HTML, JS, CSS).
  Two Possibilities:
  Cache Hit 🟢: It returns the content instantly.
  Cache Miss 🔴: It needs to fetch it from your origin infrastructure.
If the CDN doesn’t have the content cached it sends the request to your Load Balancer (e.g., AWS ELB, NGINX).
The Load Balancer distributes traffic across multiple application servers to avoid overloading any single one.
Your backend processes the request. It might fetch data from the cache(redis) or database, then returns a response.
Response travels back: App Server → Load Balancer → CDN → User
The CDN may cache it for future users.

Messaging queue - 

A message queue allows one part of a system to hand off work to another part asynchronously. For example, after a user signs up, the server queues an email job. A worker picks it up and sends the email in the background. This keeps the system fast, scalable, and loosely coupled—especially useful when handling spikes in traffic or slow tasks like notifications, logging, or processing files. Example - Apache Kafka


Framework to answer interview questions--
For these types of system design questions, use this 5-step approach:

1. Clarify scope and goals
“Who is this for? What questions will it answer?”
“What are success criteria?”

2. Identify inputs and sources
“What data do we need? Where does it come from?”

3. Define processing and transformation
“What transformations, models, or aggregations are required?”
“How do we clean/validate data?”

4. Choose outputs and delivery
“How will users consume this? Looker dashboards? Reports?”
“How often does it update?”

5. Consider non-functional aspects
Data quality / monitoring
Documentation
Ownership / access control
Scalability

