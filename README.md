# Angular-app-Deployment

### Step-1 Create RDS Database in Aws  
![image](https://github.com/mayur4279/Angular-app-Deployment/assets/73772313/66f2cd9c-8627-49ac-8107-3b68b7787e05)
Username: admin 
Password:- admin@123  

- launch  Any instance and mariadb-server (We are installing mariadb-server beacuse we required mysql client) 
  ```
  sudo apt update
  sudo apt install mariadb-server -y
  ```
- Create Database for our application  
   ```
   mysql  -u admin  -padmin@123  -h  <Rds-Database-endpoint>
   CREATE DATABASE springbackend;
   ```
- Append the Schema which is given by the database engineer
  ```
  git clone  https://github.com/mayur4279/Angular-app-Deployment
  cd Angular-app-Deployment
  sudo mysql -h  -u Angular-db -pPasswd123$ springbackend < springbackend.sql
  ```
  ```
  show databases;
  show tables;
  select * from tbl_workers;
  ```  
  
### Step-2 Create backend  

1. launch ubuntu Instance:
2. Update the packages:
   ```
   sudo apt update -y
   sudo apt install git -y
   ````

4. Install Openjdk-8:
   ```
   sudo apt install openjdk-8-jdk  
   ```
5. Install Maven:
   ```
   sudo apt install maven
   ```
6. Create Database Connection with RDS Database:
   ```
   vim   Angular-app-Deployment/angular-frontend/src/main/resources/application.properties
   ```
   **1. add db-endpoint 2. username 3. password**

7. Build the project using Maven:
   ```
   cd  Angular-app-Deployment/angular-frontend/
   mvn clean package -Dmaven.test.skip=true
   ```
8. Run The Application  
   ```
   java -jar target/spring-backend-v1.jar
   ```
**make sure to allow port 8080 in security group**




    

   

  
  


