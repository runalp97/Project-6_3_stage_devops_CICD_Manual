**DevOps Project Documentation: 3-Stage Kubernetes Deployment:**

A DevOps learning project to deploy a **Flask application** on a local **Kubernetes KinD cluster** with three environments: **Dev, Test, and Prod** — using **manual deployments** (no CI/CD tools).

> 🔄 This project has a **automated CI/CD version** with Jenkins, Ansible, Prometheus & Grafana.

> You are currently viewing the **Manual Deployment** version.


**🎯 Project Goal**

The purpose of this project is to:

- Learn how to **containerize** a Flask application.

- Create a **local Kubernetes cluster** using **KinD**.

- Deploy the same app into **three environments**:
  - `dev`
  - `test`
  - `prod`
- Understand **namespaces**, **services**, and **basic K8s objects**.

- Perform **manual deployments** using `kubectl` to build a strong Kubernetes foundation.

This project **does not** use Jenkins, Ansible, or observability tools.  
Those are implemented in the **automated version** of this project.


 **🧱 Architecture**

+-----------------------------+
|       Local Ubuntu          |
|  (Docker + KinD + kubectl)  |
+-----------------------------+
             |
      +--------------+
      |  KinD Cluster|
      +--------------+
   /        |        \
 Dev NS   Test NS   Prod NS
  |         |         |
Flask App Flask App Flask App


**Infrastructure:**

- Local **Ubuntu** machine (host)

- **Docker** to run containers

- **KinD** (Kubernetes in Docker) for creating a local K8s cluster

- **Three namespaces** for three stages of deployment:
  - `dev-namespace`
 
  - `test-namespace`

  - `prod-namespace`
 
**  Application:**

A simple **Flask web application** (Python) that:

- Listens on HTTP

- Returns a basic web page

- Used as a sample workload for Kubernetes deployments


<img width="898" height="385" alt="image" src="https://github.com/user-attachments/assets/74dcda2c-07d3-47f8-be3c-9d4efbaefe74" />

**🌐 Environments**

Each environment is isolated using namespaces:

⏹︎ Dev

-Used for initial testing.

-Frequent deployments allowed.

⏹︎ Test

-Receives manually promoted builds after dev validation.

⏹︎ Prod

- Considered stable.

- Only updated after Test verification.

- The same Docker image (Flask app) is deployed to all three, but:

- They may use different replicas, resource limits, or configs.


**⚙️ How It Works:**

⏹︎ Build Docker Image

Containerize the Flask app into a Docker image.

⏹︎ Create KinD Cluster

Use KinD to spin up a local Kubernetes cluster on the Ubuntu machine.

⏹︎ Create Namespaces

dev-namespace, test-namespace, prod-namespace.

⏹︎ Deploy to Dev

Apply Kubernetes manifests under k8s/dev/.

Validate pod & service status.

⏹︎ Deploy to Test

Once Dev is working, apply manifests from k8s/test/.

⏹︎ Deploy to Prod

Finally, deploy to k8s/prod/ using the Prod manifests.

⏹︎ Access the App

Use NodePort / port-forward to access app in each environment.

All of this is done manually using kubectl commands and configuration files.


**▶️ How to Run:**

⏹︎ Set up local environment

- Install Docker.

- Install KinD.

- Install kubectl.

⏹︎ Create a KinD cluster

- Use a KinD config file (if required) to define the cluster.

- Verify nodes and cluster info.

⏹︎ Build and tag Docker image

- Build the Flask app image.

- Load it into the KinD cluster.

⏹︎ Create namespaces

Create dev, test, and prod namespaces.

⏹︎ Deploy to Dev

- Apply definitions from k8s/dev/.

- Confirm the app is running.

⏹︎ Deploy to Test & Prod

- Repeat using k8s/test/ and k8s/prod/.

⏹︎ Test in browser

- Access services in each environment and verify responses.


**📸 Screenshots:**

kind-cluster⬇︎

<img width="940" height="652" alt="image" src="https://github.com/user-attachments/assets/a7655c4c-f481-462b-ad7a-fdc614813e70" />


dev-pod, test-pod, prod-pod,  ⬇︎

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/fd2663f9-8ac6-4321-ad9b-d1b827a7700d" />



flask-dev, flask-test, flask-prod⬇︎

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/8831242d-ad88-4aa6-8ae2-b0c80d83d822" />


<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/99ce228a-6cab-45ba-b539-d45de7aa27b4" />


<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/a6685254-2f80-42f9-bdc3-b6b75bf61b2f" />



📌 What I Learned

⏹︎ How to create and manage a KinD-based Kubernetes cluster.

⏹︎ How to structure Dev/Test/Prod environments using namespaces.

⏹︎ Hands-on experience with:

-Deployments

-Services

-Basic K8s resource management

-Importance of having separate environments even for a simple app.

📌 Conclusion

This manual deployment version helped me build a strong foundation in Kubernetes fundamentals.  
I learned how to:

● Deploy applications into multiple Kubernetes environments (Dev/Test/Prod)  

● Work with deployments, pods, services & namespaces  

● Use Docker and KinD to simulate a production-like cluster locally  

● Validate deployments manually through testing in each environment  

This project represents the first stage of developing a real DevOps pipeline —  
focusing on **understanding the basics before automation**.
