# Load Balancing in web server 
### 1. **Round Robin Load Balancing**
   - **How it works**: Traffic is distributed evenly across all available servers, one after another.
   - **Use case**: Suitable for evenly distributed traffic and when all servers have similar capacity.
   - **NGINX Configuration**:
     ```nginx
     upstream backend {
       server backend1.example.com;
       server backend2.example.com;
     }
     ```

### 2. **Least Connections Load Balancing**
   - **How it works**: The server with the least number of active connections is selected to handle the next request.
   - **Use case**: Useful when servers have varying performance or traffic is unpredictable.
   - **NGINX Configuration**:
     ```nginx
     upstream backend {
       least_conn;
       server backend1.example.com;
       server backend2.example.com;
     }
     ```

### 3. **IP Hash Load Balancing**
   - **How it works**: The client’s IP address is used to determine which server will handle the request. This ensures that a client is always directed to the same server.
   - **Use case**: Helps with session persistence (sticky sessions), where users should consistently connect to the same server.
   - **NGINX Configuration**:
     ```nginx
     upstream backend {
       ip_hash;
       server backend1.example.com;
       server backend2.example.com;
     }
     ```

### 4. **Weighted Round Robin Load Balancing**
   - **How it works**: Similar to round robin but allows assigning weights to servers, so more powerful servers receive more traffic.
   - **Use case**: When servers have varying capacities and you want to distribute traffic based on their capabilities.
   - **NGINX Configuration**:
     ```nginx
     upstream backend {
       server backend1.example.com weight=3;
       server backend2.example.com weight=1;
     }
     ```

### 5. **Least Time Load Balancing**
   - **How it works**: NGINX directs requests to the server with the lowest response time, based on active connections and processing time.
   - **Use case**: Ideal for reducing latency in environments where server response time varies.
   - **NGINX Plus Feature** (not available in the open-source version):
     ```nginx
     upstream backend {
       least_time header;
       server backend1.example.com;
       server backend2.example.com;
     }
     ```

### 6. **Random with Two Choices**
   - **How it works**: NGINX selects two servers at random and compares their active connections, then chooses the one with fewer connections.
   - **Use case**: Provides a balance between least connections and random selection.
   - **NGINX Plus Feature**:
     ```nginx
     upstream backend {
       random two;
       server backend1.example.com;
       server backend2.example.com;
     }
     ```

### 7. **Sticky Sessions (Session Persistence)**
   - **How it works**: Ensures that requests from a particular client are always directed to the same backend server by using cookies or a session identifier.
   - **Use case**: Critical for applications where maintaining a user’s session on the same server is important, like shopping carts.
   - **NGINX Plus Feature**:
     ```nginx
     upstream backend {
       sticky cookie srv_id expires=1h domain=.example.com path=/;
       server backend1.example.com;
       server backend2.example.com;
     }
     ```

### Summary of Load Balancing Methods in NGINX:
- **Round Robin**: Simple, even distribution. (startring natural start from 1.2.3)
- **Least Connections**: Balances based on active connections.
- **IP Hash**: Sticky sessions based on client IP.
- **Weighted Round Robin**: Distributes based on server capability.
- **Least Time**: Prioritizes servers with the lowest response time.
- **Random with Two Choices**: Combines random and least connections.
