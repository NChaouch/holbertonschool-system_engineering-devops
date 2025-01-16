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

# TASK 2
![Capture d'écran 2025-01-14_200750_task2](https://github.com/user-attachments/assets/4747f47c-ce37-4761-a595-ab9acc554e21)

Here is a detailed explanation of the provided diagram. It represents a distributed network architecture with data flows between different layers and components. I'll explain each part of the legend and the data flows:

---

### **Legend and Components:**

1. **User:**  
   The end-user accessing the system via HTTPS.

2. **Firewall Cluster:**  
   A group of firewalls (Firewall 1, Firewall 2, Firewall 3) that filter incoming traffic to ensure security before passing it to other components.

3. **Load Balancer (SSL Termination):**  
   A load balancer that distributes user traffic to web servers while handling SSL termination to secure connections.

4. **Monitoring System:**  
   A monitoring system consisting of multiple clients (Monitoring Client 1, 2, 3) that collect and analyze performance and health data from the components.

5. **Web Servers:**  
   Three web servers (Web Server 1, 2, 3) that process user requests and interact with the database.

6. **Primary MySQL Server:**  
   The main database server that handles SQL queries.

7. **Replica MySQL Server:**  
   A replica database server that contains a copy of the primary server's data, often used for failover or read-only operations.

---

### **Data Flows:**

1. **HTTPS:**  
   The user sends requests via HTTPS to the firewall cluster.

2. **Firewall to Load Balancer:**  
   The firewalls verify the security of requests before forwarding them to the load balancer.

3. **Load Balancer to Web Servers:**  
   The load balancer distributes incoming requests among the web servers (Web Server 1, 2, 3) to balance the load evenly.

4. **Web Servers to Primary MySQL Server:**  
   The web servers send database queries to the primary MySQL server to retrieve or update data.

5. **Replication (Primary to Replica MySQL Server):**  
   The primary MySQL server replicates its data to the replica server to ensure redundancy and enable failover or read-only access.

6. **Monitoring Clients:**  
   The monitoring clients collect performance and health data from the following:
   - Load Balancer.
   - Web Servers.
   - Database servers.

---
# TASK 3
![Capture d'écran 2025-01-14 201734_task3](https://github.com/user-attachments/assets/a1225f02-e0ce-454c-a95b-a8236b1210fa)

L'image montre une architecture logicielle organisée en plusieurs couches avec un flux de données clair entre les composants. Voici une explication des légendes et des interactions entre les différentes couches :

### 1. **Load Balancer - HAProxy (équilibreur de charge)**
   - **Rôle** : Répartit le trafic entre plusieurs serveurs pour assurer une distribution équilibrée des requêtes et éviter la surcharge.
   - **Interaction** : 
     - Le **Cluster** HAProxy en haut gère la redondance et la haute disponibilité, envoyant les requêtes à un deuxième niveau de HAProxy.
     - Ce deuxième niveau de HAProxy distribue les requêtes aux serveurs Web de la **Web Layer**.

---

### 2. **Web Layer (Couche Web)**
   - **Composants** : 
     - **Web Server 1**
     - **Web Server 2**
   - **Rôle** : 
     - Ces serveurs reçoivent les requêtes HTTP/S des utilisateurs via HAProxy.
     - Ils servent le contenu statique (HTML, CSS, JavaScript) ou transmettent les requêtes dynamiques vers les serveurs d'applications de la couche suivante.
   - **Interaction** :
     - Les requêtes envoyées par les utilisateurs, via HAProxy, sont distribuées à l’un des serveurs Web.
     - Ces serveurs transmettent les requêtes dynamiques (comme les traitements de données) vers l'**Application Layer**.

---

### 3. **Application Layer (Couche Application)**
   - **Composants** : 
     - **Application Server 1**
     - **Application Server 2**
   - **Rôle** :
     - Gèrent les traitements applicatifs comme l'exécution de la logique métier, les transactions, ou les requêtes aux bases de données.
   - **Interaction** :
     - Les serveurs Web leur transmettent les requêtes nécessitant un traitement dynamique.
     - Ils communiquent ensuite avec la couche base de données pour récupérer ou stocker des informations.

---

### 4. **Database Layer (Couche Base de Données)**
   - **Composants** : 
     - **Database Server - Primary**
     - **Database Server - Secondary**
   - **Rôle** : 
     - Le **Primary** est le serveur principal qui gère les écritures et lectures des données.
     - Le **Secondary** agit comme une réplique pour la redondance et peut être utilisé pour les lectures afin de réduire la charge sur le serveur principal.
   - **Interaction** :
     - Les serveurs d’applications envoient des requêtes SQL au serveur **Primary**.
     - Le **Secondary** synchronise les données avec le **Primary** pour maintenir une copie fidèle.

---

### **Résumé des flux :**
1. Les utilisateurs envoient des requêtes aux load balancers (HAProxy).
2. Les load balancers dirigent les requêtes vers les serveurs Web disponibles dans la **Web Layer**.
3. Les serveurs Web traitent les requêtes statiques ou transmettent les requêtes dynamiques aux serveurs d’applications dans la **Application Layer**.
4. Les serveurs d’applications envoient des requêtes aux bases de données pour récupérer ou écrire des données.
5. Les réponses suivent le chemin inverse pour arriver aux utilisateurs.

Si vous avez besoin de plus de détails ou d'une mise en page différente, n'hésitez pas !
