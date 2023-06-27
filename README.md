# jenkins-project
## CI/CD Project Documentation

This documentation provides an overview of the CI/CD project that involves the setup of Jenkins and deployment of a simple HTML website to a testing environment and subsequently to a production environment. The project utilizes three EC2 instances: `jenkins`, `staging`, and `production`, where `jenkins` serves as the Jenkins server, and `staging` and `production` act as slaves to the Jenkins server.

### Infrastructure Setup

1. Create EC2 Instances:
   - **Jenkins Instance (`jenkins`):**
     - This instance will host the Jenkins server.
   - **Testing Instance (`testing`):**
     - This instance will be used for testing the website.
   - **Production Instance (`production`):**
     - This instance will be used for deploying the website to the production environment.

2. Install Java and Docker:
   - Install **Java Runtime Environment (JRE)** on all instances (`jenkins`, `testing`, and `production`).
   - Install **Docker** on `testing` and `production` instances to facilitate containerization.

### Setting up the CI/CD Pipeline

1. Create a Git Repository:
   - Create a Git repository to store the source code of the website.

2. Configure Jenkins:
   - Access the Jenkins server (`jenkins`) and set it up by following the installation instructions specific to your operating system.

3. Create Jenkins Jobs:
   - **Git Job:**
     - Purpose: Clone the repository to the staging server.
     - Steps:
       1. Create a new Jenkins job and name it accordingly (e.g., `git-job`).
       2. Configure the job to clone the Git repository to the staging server.
       3. Specify the appropriate branch to clone from.
   - **Build Job:**
     - Purpose: Containerize the website and deploy it on the testing environment.
     - Steps:
       1. Create a new Jenkins job and name it accordingly (e.g., `build`).
       2. Configure the job to containerize the website using Docker.
       3. Specify the necessary Docker commands to build the image and deploy it on port 82 of the testing environment.

4. Define Jenkins Job Dependencies:
   - **Git Job** and **Build Job** should have a sequential dependency. The **Build Job** should only be triggered if the **Git Job** is successful.

5. Test Deployment to Testing Environment:
   - Run the Jenkins job pipeline and verify that the website is successfully containerized and deployed on the testing environment (`testing` instance) on port 82.

6. Configure Production Deployment:
   - **Build Job Modification:**
     - Modify the **Build Job** to include an additional step for containerizing the website and deploying it on the production environment (`production` instance) on port 82.
   - **Production Job:**
     - Purpose: Deploy the website on the production environment.
     - Steps:
       1. Create a new Jenkins job (e.g., `production-job`) to deploy the website on the production environment.
       2. Configure the job to containerize the website using Docker.
       3. Specify the necessary Docker commands to build the image and deploy it on port 82 of the production environment.

7. Define Jenkins Job Dependencies:
   - **Production Job** should depend on the successful completion of the **Build Job**.

### Screenshots

The following sections provide suggested places to add screenshots of your setup and configurations:
<img width="698" alt="Screenshot 2023-06-27 at 3 24 22 PM" src="https://github.com/MohamadSalehIT/jenkins-project/assets/123941794/abc7bbd5-019a-42e4-9b18-0a7d19a4e560">

#### EC2 Instances

- <img width="1434" alt="Screenshot 2023-06-27 at 3 23 42 PM" src="https://github.com/MohamadSalehIT/jenkins-project/assets/123941794/ea9fa06b-da4a-4094-ab05-9f363eb3a5eb">

-we need to open port 8080 on jenkins server in  order to access it
<img width="1314" alt="Screenshot 2023-06-27 at 3 29 31 PM" src="https://github.com/MohamadSalehIT/jenkins-project/assets/123941794/49391a0a-87a9-41d6-a9c2-8ddd8ff517ae">

-To connect the master to slaves we will open all ports(Note: this is for demo purposes, you should not open all inbound ports on an instance)
<img width="1334" alt="Screenshot 2023-06-27 at 3 34 19 PM" src="https://github.com/MohamadSalehIT/jenkins-project/assets/123941794/d440b3e9-1b1d-4d8e-a7a8-45d9ce026c2e">
-In jenkins server we will set the TCP port inbound to random :
<img width="852" alt="Screenshot 2023-06-27 at 3 47 56 PM" src="https://github.com/MohamadSalehIT/jenkins-project/assets/123941794/2e78c2ca-555a-4d5d-9700-fb6789c8613c">

-Now we will create 2 nodes for staging and production: 
<img width="1075" alt="Screenshot 2023-06-27 at 3 50 30 PM" src="https://github.com/MohamadSalehIT/jenkins-project/assets/123941794/74f650ca-1e7b-466e-a8d7-f7972cc9959b">

-After creating the nodes and connecting them to the master, we can start implementing the following pipeline : 
<img width="1402" alt="Screenshot 2023-06-27 at 3 53 34 PM" src="https://github.com/MohamadSalehIT/jenkins-project/assets/123941794/bed7b6f1-e19f-4c47-80d2-cb7310450d35">

-We will create Git-Job first and similarly build-website and production-build, then we will configure them to establish the pipeline :
<img width="956" alt="Screenshot 2023-06-27 at 3 54 50 PM" src="https://github.com/MohamadSalehIT/jenkins-project/assets/123941794/55580fcc-1e9e-4e30-81c2-7468d3782a83">

###Note that I created a basic html website to make the demonstration and testing easy to understand, then i uploaded it to my github repository

-Git-job will hook the repository using a build trigger and then we use a post build action to start the build-website job if successful:
<img width="1402" alt="Screenshot 2023-06-27 at 4 06 38 PM" src="https://github.com/MohamadSalehIT/jenkins-project/assets/123941794/5880e9aa-1968-4d6c-8d09-b1561e69debb">

<img width="1402" alt="Screenshot 2023-06-27 at 4 06 57 PM" src="https://github.com/MohamadSalehIT/jenkins-project/assets/123941794/78a1185e-9aab-40ea-94fc-5b9328b1032d">

-Build-website job will containerize the website  using docker bu executing a shell and then trigger then trigger the production-build job if successful










#### Jenkins Configuration

- Include a screenshot of the Jenkins dashboard after the initial setup.

