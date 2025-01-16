# TASK 0
![Capture d'écran 2025-01-14 151619_task0](https://github.com/user-attachments/assets/28d2397b-a517-410c-8fed-3e8792ef1f18)

---

## Diagram Legend

1. **User**:
   - The end user accessing the website via HTTP or HTTPS.

2. **DNS Record A**:
   - Resolves the domain name `www.foobar.com` to the server's IP address (8.8.8.8).

3. **Nginx (Web Server)**:
   - Receives HTTP/HTTPS requests from users and forwards them to the application server.
   - Sends the application server's responses back to the user.

4. **Application Server**:
   - Hosts the application logic and handles requests coming from the web server.
   - Interacts with the database to retrieve or store data.

5. **Code Base (Application Files)**:
   - Contains the application source code, used by the application server to generate responses.

6. **MySQL (Database)**:
   - A relational database used to store the data required by the application.

7. **Data Flows**:
   - **HTTP/HTTPS Request**: Flow between the user and Nginx.
   - **DNS Record A**: Arrow representing the domain resolution to an IP address.
   - **Forward Request**: Flow of requests forwarded from Nginx to the application server.
   - **Query**: Requests from the application server to the database.
   - **Response**: Responses sent by the database or application server to Nginx and then to the user.
  
# TASK 1
![Capture d'écran 2025-01-14 151807_task1](https://github.com/user-attachments/assets/0dcd43b6-90f9-43c2-a817-9b0cd9e560bf)

---

### Legend

1. **User**: The end-user sending a request via a browser or application.  
2. **Load Balancer (HAProxy)**: Distributes incoming requests to available servers to prevent overload.  
3. **Web Server (Nginx)**: Receives HTTP requests, serves static files, or forwards requests to application servers.  
4. **Application Servers**: Servers (1 and 2) that process business logic, handle data, and generate dynamic responses.  
5. **Database Cluster**:  
   - **Primary Database (MySQL)**: Handles write and main read operations.  
   - **Replica Database (MySQL)**: A replica of the primary database used to offload read operations.  

---

### Data Flows

1. The user sends an HTTP/HTTPS request.  
2. HAProxy forwards the request to an available Nginx server.  
3. Nginx passes the request to one of the application servers (Application Server 1 or 2).  
4. The application server queries the primary database for write or read operations.  
5. Data is replicated from the primary database to the replica database for additional read operations.  
6. The application server retrieves the necessary data from either the primary or replica database.  
7. The application server sends the processed response back to Nginx.  
8. Nginx forwards the response to the load balancer.  
9. HAProxy sends the response back to the user.  
