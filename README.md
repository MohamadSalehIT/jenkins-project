# jenkins-project
## CI/CD Project Documentation

This documentation provides an overview of the CI/CD project that involves the setup of Jenkins and deployment of a simple HTML website to a testing environment and subsequently to a production environment. The project utilizes three EC2 instances: `jenkins`, `testing`, and `production`, where `jenkins` serves as the Jenkins server, and `testing` and `production` act as slaves to the Jenkins server.

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


#### Jenkins Configuration

- Include a screenshot of the Jenkins dashboard after the initial setup.

