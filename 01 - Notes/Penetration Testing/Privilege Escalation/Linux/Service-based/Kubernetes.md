
2026-05-15 15:53

Tags: #escalation  

## Kubernetes

- **Definition:** An open-source *container orchestration platform* originally developed by Google, now the industry standard for managing microservices.


- **Functionality:** Automates deployment, scaling, and management of containerized applications.


- **Versus Docker:** While Docker is a platform for containerizing apps with manual scaling, K8s orchestrates those containers with automatic scaling, complex network policies, and varied storage options.


- **Pods:** The core operational unit in K8s. A pod acts as a *separate virtual machine* containing one or more closely connected containers sharing an IP, hostname, and storage.


## Architecture

- **Control Plane (Master Node):** The management layer that controls the cluster and maintains its desired state. Key components include:
    - **API Server (Port 6443):** The main entry point for RESTful administrative commands (via `kubectl`).
        
    - **etcd (Ports 2379, 2380):** A key-value store containing cluster state data.
        
    - **Scheduler (Port 10251):** Assigns new pods to worker nodes.
        
    - **Controller Manager (Port 10252):** Regulates the state of the cluster.
        
    - **Kubelet API (Ports 10250, 10255):** Agent running on each node communicating with the Master.


- **Worker Nodes (Minions):** The designated machines where containerized applications (pods) actually run, managed entirely by the Control Plane.

## Security Mechanisms & Risks

- **RBAC (Role-Based Access Control):** K8s uses RBAC to assign specific permissions to authenticated users or processes.

- **Vulnerability - Anonymous Kubelet Access:** By default, the Kubelet API permits anonymous, unauthenticated requests. If exposed, attackers can query the API to extract sensitive data or execute commands.

## Exploitation & Privilege Escalation Methodology

- **Step 1: Reconnaissance (Extracting Pods)**
    - Access the exposed Kubelet API (port 10250) using `curl` or `kubeletctl`.
        
    - Extract pod configurations to uncover namespaces, container images, uids, and potentially hardcoded secrets from the "last applied configuration."
    - ![[Screenshot_20260515_155748.png]]


- **Step 2: Command Execution (RCE)**
    - Use `kubeletctl` to scan for pods vulnerable to Remote Code Execution (`kubeletctl scan rce`).
        
    - Execute commands inside the container (e.g., `kubeletctl exec "id"`). Often, containers run as root (`uid=0`), granting full administrative access _within_ that container.
    - ![[Screenshot_20260515_155832.png]]
    - ![[Screenshot_20260515_155913.png]]
    - ![[Screenshot_20260515_155944.png]]


- **Step 3: Extracting Tokens & Certificates**
    - Extract the Kubernetes service account token: `cat /var/run/secrets/kubernetes.io/serviceaccount/token`
    - ![[Screenshot_20260515_160023 1.png]]
        
    - Extract the CA certificate: `cat /var/run/secrets/kubernetes.io/serviceaccount/ca.crt`


- **Step 4: Enumerating Privileges**
    - Use the stolen token and certificate to check permissions on the cluster: `kubectl auth can-i --list`.
    - ![[Screenshot_20260515_160053.png]]
        
    - Identify if the compromised account has permissions to `create`, `get`, or `list` pods.


- **Step 5: Host System Compromise**
    - If pod creation is permitted, write a malicious YAML deployment file.
        
    - Configure the YAML to mount the host system's root directory (`/`) into the new container (e.g., at `/root`).
        
    - Deploy the malicious pod using `kubectl apply -f`.
        
    - Execute commands on the new pod to read host files, such as extracting the host root user's private SSH key (`/root/root/.ssh/id_rsa`).
## References:
https://academy.hackthebox.com/app/module/51/section/2444
