# **Azure DevOps Terraform CI/CD Pipeline: Automated VM Deployment with Apache**

## **Overview**
This project demonstrates an automated **CI/CD pipeline** using **Azure DevOps** and **Terraform** to create a Linux Virtual Machine (VM) in Azure, install Apache, and implement a structured **three-stage deployment process**:

1. **Terraform Apply** - Creates the VM and installs Apache.
2. **Terraform Before Destroy** - Asks for confirmation before destruction.
3. **Terraform Destroy** - Destroys the infrastructure upon approval.

## **Flow Diagram**
```
+-------------------------------------------+
|        Create Azure DevOps Repo          |
+-------------------------------------------+
                        |
                        v
+-------------------------------------------+
|       Set Up Azure DevOps Pipeline       |
+-------------------------------------------+
                        |
                        v
+-------------------------------------------+
|      Install Terraform Extension         |
+-------------------------------------------+
                        |
                        v
+-------------------------------------------+
|  Configure Azure Service Connection      |
+-------------------------------------------+
                        |
                        v
+-------------------------------------------+
|       Create Terraform main.tf           |
+-------------------------------------------+
                        |
                        v
+-------------------------------------------+
|      Store SSH Keys in Secure Files      |
+-------------------------------------------+
                        |
                        v
+-------------------------------------------+
|        Write apache-install.sh           |
+-------------------------------------------+
                        |
                        v
+-------------------------------------------+
|        Write YAML Pipeline File          |
+-------------------------------------------+
                        |
                        v
+--------------------STAGE 1----------------+
|            Terraform Apply                |
|  - Run Terraform Init & Plan              |
|  - Create VM in Azure                     |
|  - Install Apache                         |
|  - Verify Apache Installation             |
+-------------------------------------------+
                        |
                        v
+--------------------STAGE 2----------------+
|         Terraform Before Destroy          |
|  - Ask for approval before destruction    |
+-------------------------------------------+
                        |
                        v
+--------------------STAGE 3----------------+
|          Terraform Destroy                |
|  - Destroy the infrastructure             |
+-------------------------------------------+
```

## **Step-by-Step Implementation**

### **Step 1: Create Azure Repo**
- Create a new repository in **Azure Repos**.
- Store Terraform and pipeline files.

### **Step 2: Set Up Azure DevOps Pipeline**
- Create a new pipeline in **Azure DevOps**.
- Ensure pipeline runs on **push events**.

### **Step 3: Install Terraform Extension**
- The default image does not have Terraform installed.
- Install Terraform extension from **Azure Marketplace**.
- Add Terraform installation task in the pipeline.

### **Step 4: Configure Azure Service Connection**
- Create a **Service Connection** in Azure DevOps to allow Terraform to authenticate with Azure.

### **Step 5: Create Terraform Configuration (main.tf)**
- Write Terraform code to create a **Linux VM** in Azure.
- Configure **network security rules**.
- Implement **remote-exec** to execute scripts inside the VM.
- Use SSH authentication.

### **Step 6: Store SSH Keys in Secure Files**
- Generate **RSA public and private keys**.
- Store them securely in **Azure DevOps Library** under **Secure Files**.

### **Step 7: Write Apache Installation Script (apache-install.sh)**
- Install Apache inside the VM.
- Validate Apache installation.
- Run `ls -l` command to list files for verification in the pipeline logs.

### **Step 8: Write YAML Pipeline File**

#### **Stage 1: Terraform Apply**
1. **Terraform Install Task** - Ensure Terraform is installed.
2. **Terraform Init Task** - Initialize Terraform backend.
3. **Secure Files Task** - Access SSH private key from secure files.
4. **Terraform Plan Task** - Preview infrastructure changes.
5. **Terraform Apply Task** - Deploy the VM.
6. **Run apache-install.sh** - Install Apache and verify installation.

#### **Stage 2: Terraform Before Destroy**
- Add **manual approval task** before executing the destroy stage.

#### **Stage 3: Terraform Destroy**
- Execute `terraform destroy` after receiving approval.

## **Conclusion**
This project successfully demonstrates a **CI/CD pipeline** in **Azure DevOps** using **Terraform** for Infrastructure as Code (IaC). The pipeline automates **VM provisioning, Apache installation, and controlled destruction** in a structured manner.

