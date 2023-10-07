# Kubernetes
Learn Kubernetes Deep Dive

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

That's it! You have successfully installed Minikube and set up a single-node Kubernetes cluster on your Ubuntu laptop. You can now use `kubectl` to manage and interact with your local Kubernetes cluster, and you have the option to deploy and test applications on this cluster for development and testing purposes.

### --------------------------------------------------------------------------------------------------------
