# 🌐 Multi-Region Web Application Deployment using Azure Traffic Manager & Application Gateway

## 📌 Project Overview

This project demonstrates the deployment of a **multi-region web application architecture on Microsoft Azure** using **Traffic Manager**, **Application Gateway**, **Virtual Machines**, **VNets**, and **Azure Blob Storage**.

The solution ensures **optimal traffic distribution between Central US and West US regions**, supports **path-based routing**, and uses **custom error pages hosted on Azure Blob Storage**.

---

## 🏗️ Architecture Summary

```
Client
  |
  v
Traffic Manager (example.com)
  |
  +----------------------+
  |                      |
Central US           West US
  |                      |
Application Gateway   Application Gateway
  |                      |
Path-based routing   Path-based routing
  |                      |
VM2 (Home Page)      VM2 (Home Page)
VM1 (/upload)        VM1 (/upload)
```

* **/ → Home Page (VM2)**
* **/upload → Upload Page (VM1)**
* **403 / 502 Errors → error.html from Azure Blob Static Website**

---

## 🌍 Regions Used

* **Central US**
* **West US**

Traffic is distributed optimally between both regions using **Azure Traffic Manager**.

---

## 🧩 Components Used

* Azure Traffic Manager
* Azure Application Gateway (Path-based routing)
* Azure Virtual Machines (Linux)
* Azure Virtual Networks (VNet-VNet Peering)
* Azure Blob Storage (Static Website + Upload Container)
* GitHub Repository
* Python (Flask)

---

## 📂 Web Pages Deployed

| Page        | URL Path  | Hosted On          |
| ----------- | --------- | ------------------ |
| Home Page   | `/`       | VM2                |
| Upload Page | `/upload` | VM1                |
| Error Page  | 403 / 502 | Azure Blob Storage |

---

## 📦 Storage Account Configuration

### 1️⃣ Static Website

* Enabled **Static Website** on the Storage Account
* Hosted `error.html` (from GitHub repository)
* Used for:

  * **403 Forbidden**
  * **502 Bad Gateway**

### 2️⃣ Blob Container

* Created a container named:

  ```
  upload
  ```
* Used by the Flask application to upload files

---

## 🖥️ Virtual Machine Configuration

### Common Steps (VM1 & VM2)

```bash
git clone https://github.com/azcloudberg/azproject
cd azproject
```

---

### VM1 – Upload Page

```bash
./vm1.sh
```

After running the script:

1. Edit `config.py`
2. Enter:

   * Storage account name
   * Storage account access key
   * Container name (`upload`)

Run the application:

```bash
sudo python3 app.py
```

---

### VM2 – Home Page

```bash
./vm2.sh
```

This installs and starts the home page service.

---

## 🌐 Networking Configuration

### VNet Setup

* Separate VNets created in **Central US** and **West US**
* VMs deployed inside respective VNets

### VNet Peering

* Configured **VNet-to-VNet Peering** between regions
* Ensures private communication between deployments

---

## 🚦 Application Gateway Configuration

### Path-Based Routing Rules

| Path      | Backend           |
| --------- | ----------------- |
| `/`       | VM2 (Home Page)   |
| `/upload` | VM1 (Upload Page) |

### Custom Error Pages

* **403 Error** → `error.html` (Blob Static Website)
* **502 Error** → `error.html` (Blob Static Website)

---

## 🌍 Traffic Manager Configuration

* **Routing Method:** Performance
* **Endpoints:**

  * Central US Application Gateway
  * West US Application Gateway
* Domain name:

  ```
  example.com
  ```

  (example refers to Traffic Manager DNS name)

---

## ✅ Final Outcome

✔ Multi-region deployment completed
✔ Traffic distributed optimally
✔ Path-based routing configured
✔ Upload functionality integrated with Azure Blob Storage
✔ Custom error handling using static website
✔ High availability across regions

---

## 📝 Key Learnings

* Implemented global traffic distribution using Azure Traffic Manager
* Configured Application Gateway for advanced routing
* Integrated Flask application with Azure Blob Storage
* Designed fault-tolerant, scalable Azure architecture

---

## 👤 Author

**Ankith Ak**
Cloud & DevOps Enthusiast

---

## 📌 Repository

🔗 [https://github.com/azcloudberg/azproject](https://github.com/azcloudberg/azproject)
