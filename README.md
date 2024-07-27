# BootStrap K8s with ArgoCD
Prerequisites
To follow along, you’ll need the following installed/configured on the environment or machine you’ll work on.

Git Installed

Terraform Installed

AWS CLI installed and configured

AWS Account and Access Keys Configured

![Screenshot 2024-07-27 130719](https://github.com/user-attachments/assets/fc399c9a-6f5e-44d7-b61d-cca6b1bd2a76)
![Screenshot 2024-07-27 130840](https://github.com/user-attachments/assets/6fda1916-d206-4cc7-a9cc-d7785cb3c6db)
![Screenshot 2024-07-27 130914](https://github.com/user-attachments/assets/63ed9ee9-bc8b-4b2b-acd3-19ce70217d21)
![Screenshot 2024-07-27 130925](https://github.com/user-attachments/assets/5ddf688c-a3fb-4df8-9fed-fca2476189ba)

 STEP 1. 
 Clone the repository containing Terraform files
 CD into the terrafrom folder 
 
 Initialize, plan, and apply the Terraform files to provision your cluster on AWS
 
terraform init

terraform plan

terraform apply

 ![Screenshot 2024-07-27 131102](https://github.com/user-attachments/assets/5cc43694-b066-458a-97e0-5e4258e0202a)
![Screenshot 2024-07-27 131207](https://github.com/user-attachments/assets/ad7c7d71-86f4-4325-9c81-8a1532501d5d)

STEP 2
The terraform configuration provisions the following listed below:

EKS cluster on AWS
![Screenshot 2024-07-27 131321](https://github.com/user-attachments/assets/01fc4765-81d9-435c-8402-6286b943d5c3)
![Screenshot 2024-07-27 133420](https://github.com/user-attachments/assets/c6f724b3-e000-43bb-b9ce-1809db2492d7)

Update Kube config on the machine you’re running terraform from.
![Screenshot 2024-07-27 133603](https://github.com/user-attachments/assets/a89a79c8-01c9-47eb-b1db-1ae05ff6d88c)


INSTALL ARGOCD
![Screenshot 2024-07-27 133433](https://github.com/user-attachments/assets/1b36de78-08d3-4c93-9958-f030ccc5d262)


STEP 3

INSTALL KUBECTL 

![Screenshot 2024-07-27 133844](https://github.com/user-attachments/assets/e4583f61-f608-4c7e-b36a-da0521e19031)


STEP 4
After updating your cluster to receive manifests configuration, apply the files in the manifest folder with the command below. The command applies a manifest of a golang application.
![Screenshot 2024-07-27 133934](https://github.com/user-attachments/assets/70177766-3c75-4d46-9be6-7f0dab1b5b19)

STEP 5

Bootstrapping the Manifest with ArgoCD

Once your manifest files have been applied, the next step is to bootstrap them to ArgoCD to enhance continuous delivery. Follow these steps:

Check that argocd is installed and the pods are running.

![Screenshot 2024-07-27 134132](https://github.com/user-attachments/assets/95d9d29e-13e9-418b-929a-18b024e24d76)
![Screenshot 2024-07-27 145457](https://github.com/user-attachments/assets/4352a22e-bcf3-4fab-8e83-d714e7fe6652)

When the pods are ready, map your port to access ArgoCD in the browser

![Screenshot 2024-07-27 143917](https://github.com/user-attachments/assets/6a5c0e6b-44b3-40cb-a4bd-9580b248671f)

CONFIRM ON THE BROWSER USING http://localhost:8080

![Screenshot 2024-07-27 173933](https://github.com/user-attachments/assets/c9295781-9088-4480-8a88-1ff15a1bb243)


Upon access, you will be required to log in with a username and a password. The username is admin, and the password can be retrieved using the following command:
![Screenshot 2024-07-27 181322](https://github.com/user-attachments/assets/4d7f6215-82a0-400d-801e-c244948deadf)

![Screenshot 2024-07-27 181456](https://github.com/user-attachments/assets/9b8178da-eb3d-4b5f-86f6-c332b3c2a80d)

STEP 6
Adding Your Repository and Cluster to ArgoCD
Once logged in successfully, connect the GitHub repo that contains the manifest with the following command:
argocd repo add https://github.com/username/repourl --username <your-github-username> --password <your-personal-access-token>

![Screenshot 2024-07-27 172244](https://github.com/user-attachments/assets/42bc6cb6-7573-4ae3-b9a0-40a38b3eb152)

Once your repo has been connected successfully, add your cluster to the ArgoCD server using the following command as shown below:
![Screenshot 2024-07-27 172458](https://github.com/user-attachments/assets/58907bed-a19b-4deb-94a0-d8ed3f4e0610)

STEP 7
Creating and Syncing Your Application
Once the cluster has been added successfully, proceed to create your app and configure your ArgoCD using:
argocd app create appname \
   --repo https://github.com/username/repourl \
   --path manifests/ \
   --dest-server https://kubernetes.default.svc \
   --dest-namespace argocd
   
If the app was successfully created, you should get a message like this:
![Screenshot 2024-07-27 173402](https://github.com/user-attachments/assets/410bd2b9-15c0-4c28-ada6-a4d1c8dc53ea)

STEP 8
Finally, sync your app using the following command:

argocd app sync <app-NAME>

![Screenshot 2024-07-27 173539](https://github.com/user-attachments/assets/7a2008ef-af28-4b9a-b694-6cea77103369)

STEP 9
When you see this response, you can go on to Login into your ArgoCD via browser to check it out.
![Screenshot 2024-07-27 173807](https://github.com/user-attachments/assets/490e67ac-53d0-4261-9ece-e2e5f94cc037)



   







 
