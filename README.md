# Angular-app-Deployment

### Step-1) Create RDS Database in Aws  
![image](https://github.com/mayur4279/Angular-app-Deployment/assets/73772313/66f2cd9c-8627-49ac-8107-3b68b7787e05)
Username: admin  </br>
Password: admin@123  

- launch  Any instance and mariadb-server (We are installing mariadb-server beacuse we required mysql client) 
  ```
  sudo apt update -y 
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
  
### Step-2) Create backend  

1. launch **ubuntu** Instance: (make sure to allow port 8080 in security group)
   
   ![image](https://github.com/mayur4279/Angular-app-Deployment/assets/73772313/c30b8ce5-7199-49fd-a742-cd8722c87ad3)

3. Update the packages:
   ```
   sudo apt update -y
   sudo apt install git -y
   git clone https://github.com/mayur4279/Angular-app-Deployment
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
   cd Angular-app-Deployment
   vim spring-backend/src/main/resources/application.properties
   ```
   - add db-endpoint, username, password

   ![image](https://github.com/mayur4279/Angular-app-Deployment/assets/73772313/577126f1-6119-4825-b2f9-b5d8017478e5)

7. Build the project using Maven:
   ```
   cd  Angular-app-Deployment/spring-backend/
   mvn clean package -Dmaven.test.skip=true
   ```
   ![image](https://github.com/mayur4279/Angular-app-Deployment/assets/73772313/74269948-8fbf-41d3-9279-435efbb16ee6)

8. Compiled java application successfully created

   ![image](https://github.com/mayur4279/Angular-app-Deployment/assets/73772313/44c4b161-bfec-435d-819f-8dfd10d6cb92)

8. Run The Application  
   ```
   java -jar target/spring-backend-v1.jar
   ```
   ![image](https://github.com/mayur4279/Angular-app-Deployment/assets/73772313/e26e491e-75df-4312-9e43-0074bd790ff7)

### Step-3) Create Frontend  

1. Launch New Ubuntu Instance (make sure allow port http/80 in security group)

   ![image](https://github.com/mayur4279/Angular-app-Deployment/assets/73772313/1f2a6963-ba25-499a-bde6-78386cdf1ca0)

2. Install Node.js and npm
   ```bash
   sudo apt update -y  
   sudo apt install -y nodejs npm  
   ```

3. Check Node.js and npm versions

   ```bash
   node -v
   npm -v
   ```
   
4. Install Angular CLI globally
   ```bash
   sudo npm install -g @angular/cli@14.2.1
   ```
   
5. Verify Angular CLI installation
   ```bash
   ng version
   ```
6. Install Angular js code
   ```
   git clone https://github.com/mayur4279/Angular-app-Deployment
   cd Angular-app-Deployment/angular-frontend
   ```
7. Step 5: Connect to backend server
   ```
   vim src/app/services/worker.service.ts
   ```
   Note: add public-ip of backend server

   ![image](https://github.com/mayur4279/Angular-app-Deployment/assets/73772313/b016e38a-e654-479d-a09a-37b49270d8dc)

8. Install project dependencies (if needed)

   ```bash
   cd Angular-app-Deployment/angular-frontend
   ```
9. Build The frontend with ng command  
   ```
   ng build
   ```
   ![image](https://github.com/mayur4279/Angular-app-Deployment/assets/73772313/c3e6bddb-e825-47c8-a18c-68de658e1ac5)

   New Directory Automatically created After building process is complete.

   ![image](https://github.com/mayur4279/Angular-app-Deployment/assets/73772313/f4d6520f-2d6a-42f1-899c-1e33b0b5b15f)

10. Start the server 
    ```
    sudo ng serve --host 0.0.0.0 --port=80
    ```
    ![image](https://github.com/mayur4279/Angular-app-Deployment/assets/73772313/e6ce765f-d277-40a1-a3cc-d4489af1fa66)
    
11. Go to browser and hit public-ip of frontend instance

    ![image](https://github.com/mayur4279/Angular-app-Deployment/assets/73772313/b5735e32-deae-448b-80d2-8a1be86d50a5)



9. Deploy the artifact to s3 bucket
   ````
   cd dist/angular-frontend
   aws s3 mb s3://angular-frontend-app-buck
   aws s3 cp .  s3://angular-frontend-buck --recursive
   ````

10. Create Cloudfront Distribution
    ![cloudfront-dis](https://github.com/abhipraydhoble/Project-Angular-App/assets/122669982/b7734aee-4c8d-4cb7-a4a2-b2334399ddd8)


    ![Angular-cdn](https://github.com/abhipraydhoble/Project-Angular-App/assets/122669982/aba82b3f-ca43-4a34-9a4e-89a4db42f7c2)

11. Step 10: Create Hosted zone in route:53
    ![hosted zone](https://github.com/abhipraydhoble/Project-Angular-App/assets/122669982/cc0abb81-4184-4dcd-b159-3b0e35f7a2d3)


12. Step 11: ADD NS records in hostinger

13. Generate SSL certificate and create records in s3

    ![ssl](https://github.com/abhipraydhoble/Project-Angular-App/assets/122669982/d31be2ab-1dfa-4d1a-949b-7aa2ca82c0e0)

14. Step 13: Attach SSL to cloudfront distribution

15. Create A record in RT-53 and add cloufront distribution

    ![a-record](https://github.com/abhipraydhoble/Project-Angular-App/assets/122669982/fc902838-ad31-487c-a92d-51316ccd4648)

16. Final Result

    ![domain-frontend](https://github.com/abhipraydhoble/Project-Angular-App/assets/122669982/083c3e34-543b-4a9e-a40a-bb06b1beea2a)

  







1. Install AWS CLI
   ```
   sudo apt install unzip -y
   curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
   unzip awscliv2.zip
   sudo ./aws/install
   ```
   
   ```
   aws configure
   ```
