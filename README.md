# pipeline-assignment

Steps I followed:

1. Create Minikube Cluster
   - To install the latest minikube stable release on x86-64 Linux using binary download:
     
     ```curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64```
     
     ```sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64```
   - Start cluster - from a terminal with administrator access (but not logged in as root), run:

     ```minikube start```
     ![image](https://github.com/user-attachments/assets/058e95af-2989-491b-bba4-d4e750b4be17)
     
   - Download the appropriate version of kubectl and access the cluster:
     ```minikube kubectl -- get po -A```

     ```kubectl get po -A```
     ![image](https://github.com/user-attachments/assets/3c42bfe8-ea4d-4449-96e9-c9ee1f5956f4)

2. Install ArgoCD
   ```kubectl create namespace argocd```
   
   ![image](https://github.com/user-attachments/assets/7f7585fb-1cd3-414c-87b2-32ee1a04d86b)

   - install helm:

   ```
   curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
   sudo apt-get install apt-transport-https --yes
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
   sudo apt-get update
   sudo apt-get install helm
   ```

   - run ```helm repo add argo https://argoproj.github.io/argo-helm```
     
     ![image](https://github.com/user-attachments/assets/d23f1dd2-2a6a-4002-b27f-12f2cd8e78fc)
  
   - run ```helm repo update``` and ```helm install argocd argo/argo-cd --namespace argocd```

     ![image](https://github.com/user-attachments/assets/ed6d03fd-13ed-4184-872b-e650b5e402f8)
     
3. Access ArgoCD UI on Port 8080:
   
   ```kubectl port-forward svc/argocd-server -n argocd 8080:443```

   - Go to ```localhost:8080```
  
     ![image](https://github.com/user-attachments/assets/1ee5c58d-345f-4a3a-8cae-07dbffe7c934)

     The initial username is _Admin_. To get password, run:
     
     ```kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 --decode```

   - Copy + paste password and login.

4. Create Front End, Back End, and connect
   ![Screenshot 2024-10-30 103055](https://github.com/user-attachments/assets/cd36efe6-c463-405c-8145-2b4f0f8e5908)

6. Create Dockerfiles
7. Docker Build
   ![Screenshot 2024-10-26 150817](https://github.com/user-attachments/assets/9d5bf106-0593-4593-b357-87a0f924dd36)
   ![Screenshot 2024-10-26 150921](https://github.com/user-attachments/assets/9075b998-aa1c-493a-9c79-c19b91d8b9b6)

8. Add images to Jfrog
![Screenshot 2024-10-26 154308](https://github.com/user-attachments/assets/dea1a98e-65cc-4ef9-9960-93653b433727)

![Screenshot 2024-10-26 163003](https://github.com/user-attachments/assets/a5c3b18c-3e3b-4e7d-a181-a58878e1f56a)
![Screenshot 2024-10-26 163434](https://github.com/user-attachments/assets/5e95fcef-553c-4257-a95c-3dabc1577f4d)

9. Create Workflows
    ![image](https://github.com/user-attachments/assets/7aa1974b-be3a-4ffc-9a50-d0de10ec87d2)

