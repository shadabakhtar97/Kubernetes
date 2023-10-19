# Kubernetes
Learn Kubernetes Deep Dive

### --------------------------------------------------------------------------
### What is Kubernetes ?
Kubernetes, often abbreviated as K8s, is an open-source container orchestration platform developed by Google and released to the Cloud Native Computing Foundation (CNCF) in 2014. It is designed to automate the deployment, scaling, management, and operation of containerized applications. Containers are a technology that allows applications and their dependencies to be packaged together in a consistent, lightweight, and isolated environment, which makes them easy to deploy and manage.

Key features of Kubernetes include:

1. Container Orchestration: Kubernetes can manage the deployment and scaling of containerized applications across clusters of machines. It ensures that the desired state of an application, specified in a declarative configuration, is maintained.

2. Service Discovery and Load Balancing: Kubernetes provides built-in service discovery and load balancing for containers within the cluster, making it easy to expose services to the network and distribute traffic.

3. Self-Healing: Kubernetes constantly monitors the state of applications and can automatically replace or reschedule containers that fail or become unresponsive, ensuring high availability.

4. Automated Rollouts and Rollbacks: It supports automated deployment updates and rollbacks, enabling you to perform application updates with minimal downtime.

5. Declarative Configuration: Kubernetes allows you to describe your desired application state using configuration files (YAML or JSON), and it will work to make that state a reality, rather than requiring you to script specific actions.

6. Portability: Kubernetes is platform-agnostic and can run on a variety of cloud providers (like AWS, Google Cloud, Microsoft Azure), on-premises data centers, and even on local development machines. This portability makes it easy to move or replicate workloads across different environments.

7. Extensibility: Kubernetes is highly extensible, with a robust ecosystem of plugins, extensions, and custom resources, allowing you to tailor it to your specific needs.

8. Scalability: Kubernetes can scale applications up or down based on resource demands, ensuring efficient utilization of computing resources.

Kubernetes has become a cornerstone of modern container-based application development and deployment. It simplifies the management of complex, distributed systems and has gained widespread adoption in the world of DevOps and cloud-native computing. It provides a powerful platform for building, deploying, and scaling applications in a consistent and efficient manner.

### --------------------------------------------------------------------------
### To install Kubernetes on an Ubuntu laptop, you can set up a single-node Kubernetes cluster using Minikube, which is a tool for easily running Kubernetes locally. Here are the steps to install Minikube and set up a Kubernetes cluster on your Ubuntu laptop:

**Note:** Before you begin, ensure that you have a hypervisor such as VirtualBox or KVM installed on your laptop, as Minikube relies on a hypervisor to create virtual machines.

1. **Install Minikube**:

   Open a terminal and run the following commands to download and install Minikube:

   ```bash
   curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
   sudo install minikube-linux-amd64 /usr/local/bin/minikube
   ```

2. **Install kubectl**:

   `kubectl` is the command-line tool for interacting with Kubernetes clusters. Install it using the following command:

   ```bash
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
   chmod +x kubectl
   sudo mv kubectl /usr/local/bin/
   ```

3. **Start Minikube**:

   Start Minikube and specify the driver you want to use (e.g., VirtualBox). You can choose a different driver based on your preferences and what's installed on your system.

   ```bash
   minikube start --driver=virtualbox
   ```

   This command will create a single-node Kubernetes cluster using Minikube.

4. **Verify Kubernetes Installation**:

   To verify that your Minikube-based Kubernetes cluster is running correctly, you can run the following command:

   ```bash
   kubectl cluster-info
   ```

   You should see information about the cluster, including the cluster master's URL and the Kubernetes dashboard URL.

5. **Access Kubernetes Dashboard (Optional)**:

   If you want to access the Kubernetes dashboard, you can do so using the following command:

   ```bash
   minikube dashboard
   ```

   This will open a web browser with the Kubernetes dashboard interface.


### --------------------------------------------------------------------------------------------------------
### Installing Kubernetes on-premises can be a complex process, as it involves setting up and configuring multiple components. Below is a simplified guide to help you get started with a basic Kubernetes cluster on your on-premises hardware. This guide assumes that you have a few physical or virtual machines available for creating the cluster. Please note that in production environments, you may need to adapt these steps to your specific requirements.

Here are the high-level steps to install Kubernetes on-premises:

**Step 1: Prepare On-Premises Machines**

- Ensure that you have a set of machines with Ubuntu or a compatible Linux distribution installed. You'll typically need at least three machines for a basic Kubernetes cluster, but you can start with one node for testing purposes.

**Step 2: Install Docker**

- On each machine, install Docker, which is a container runtime used by Kubernetes:

  ```bash
  sudo apt update
  sudo apt install docker.io
  ```

**Step 3: Install Kubernetes Components**

- On each machine, you'll need to install Kubernetes components, including `kubeadm`, `kubelet`, and `kubectl`. Run these commands on each node:

  ```bash
  sudo apt update && sudo apt install -y apt-transport-https curl
  sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
  echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
  sudo apt update
  sudo apt install -y kubeadm kubelet kubectl
  ```

**Step 4: Set Up Master Node (Control Plane)**

- Choose one of the machines to be the master (control plane) node. Initialize the cluster and configure the master:

  ```bash
  sudo kubeadm init --pod-network-cidr=10.244.0.0/16
  ```

  Note: You can customize the `--pod-network-cidr` flag based on your network configuration.

- Follow the instructions provided by `kubeadm` to set up `kubectl` for the user:

  ```bash
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
  ```

- Install a pod network add-on to enable communication between pods:

  For example, you can use Calico:

  ```bash
  kubectl apply -f https://docs.projectcalico.org/v3.8/manifests/calico.yaml
  ```

**Step 5: Join Worker Nodes**

- On the worker nodes (all machines except the master), join the cluster by running the command provided by `kubeadm` on the master:

  ```bash
  sudo kubeadm join <master-node-ip>:<master-port> --token <token> --discovery-token-ca-cert-hash <hash>
  ```

  Replace `<master-node-ip>`, `<master-port>`, `<token>`, and `<hash>` with the values provided by `kubeadm init` on the master node.

**Step 6: Verify Cluster**

- On the master node, verify that the worker nodes have joined the cluster:

  ```bash
  kubectl get nodes
  ```

- Ensure that all nodes are in the "Ready" state.

**Step 7: Deploy Applications**

- You can now use `kubectl` to deploy and manage applications on your on-premises Kubernetes cluster.
### --------------------------------------------------------------------------------------------------------

