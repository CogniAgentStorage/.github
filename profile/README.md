Cogni is a decentralized platform for storing, sharing, and retrieving AI models, datasets, and files using IPFS (InterPlanetary File System). Built for scalability, immutability, and global collaboration, Cogni leverages the power of IPFS to ensure reliable, tamper-proof data storage.

This guide provides comprehensive instructions on how to set up Cogni’s IPFS node, configure it, and interact with it using the terminal.

## **Table of Contents**

1. [About Cogni](#about-cogni)
2. [Installation Guide](#installation-guide)
   - [Windows Installation](#windows-installation)
   - [Linux Installation](#linux-installation)
   - [macOS Installation](#macos-installation)
3. [Basic IPFS Commands](#basic-ipfs-commands)
4. [Advanced IPFS Commands](#advanced-ipfs-commands)
5. [Configuration Guide](#configuration-guide)
6. [Setting Up a Custom Gateway](#setting-up-a-custom-gateway)
7. [Examples](#examples)
8. [Useful Resources](#useful-resources)

---

## **About Cogni**

Cogni is designed for AI developers, researchers, and innovators who need reliable, decentralized storage for their AI artifacts, including:
- **AI Models**: Store and retrieve large pre-trained models for machine learning and AI applications.
- **Datasets**: Host large datasets with content-based addressing for global accessibility.
- **Metadata**: Ensure reproducibility by sharing experiment results, metadata, and model versions.

By leveraging **IPFS**, Cogni ensures:
- **Decentralization**: No single point of failure.
- **Immutability**: Files are identified by their content, ensuring they remain unchanged.
- **Global Collaboration**: Anyone can retrieve and pin data using Cogni’s custom IPFS gateway.

---

## **Installation Guide**

### **Windows Installation**

1. **Download IPFS CLI**:
   - Visit the [Go-IPFS Releases](https://github.com/ipfs/go-ipfs/releases) page.
   - Download the latest version for Windows (`go-ipfs_vX.XX.X_windows-amd64.zip`).
   - Extract the ZIP file to a directory (e.g., `C:\ipfs`).

2. **Add IPFS to PATH**:
   - Open **Environment Variables** and add the extracted IPFS folder (containing `ipfs.exe`) to the `Path` variable.
   - Open a new terminal and run:
     ```bash
     ipfs --version
     ```
     If it returns the version number, the installation was successful.

3. **Initialize IPFS**:
   ```bash
   ipfs init
   ```

4. **Start the IPFS Daemon**:
   ```bash
   ipfs daemon
   ```

---

### **Linux Installation**

1. **Download the IPFS binary**:
   ```bash
   wget https://dist.ipfs.io/go-ipfs/v0.40.0/go-ipfs_v0.40.0_linux-amd64.tar.gz
   ```
2. **Extract and install IPFS**:
   ```bash
   tar -xvzf go-ipfs_v0.40.0_linux-amd64.tar.gz
   cd go-ipfs
   sudo bash install.sh
   ```

3. **Verify the installation**:
   ```bash
   ipfs --version
   ```

4. **Initialize IPFS**:
   ```bash
   ipfs init
   ```

5. **Start the IPFS daemon**:
   ```bash
   ipfs daemon
   ```

---

### **macOS Installation**

1. **Install IPFS using Homebrew**:
   ```bash
   brew install ipfs
   ```

2. **Initialize IPFS**:
   ```bash
   ipfs init
   ```

3. **Start the IPFS daemon**:
   ```bash
   ipfs daemon
   ```

---

## **Basic IPFS Commands**

### **Adding a File**
```bash
ipfs add <file_name>
```
This will return a unique **Content Identifier (CID)** for the file. You can use this CID to retrieve the file later.

### **Retrieving a File**
```bash
ipfs cat <CID>
```
This retrieves and displays the content of the file with the given CID.

### **Listing Files**
```bash
ipfs ls <CID>
```
Lists the contents of a directory CID.

---

## **Advanced IPFS Commands**

### **Pinning a File**
Pinning ensures that a file remains available on your node and isn’t removed during garbage collection.
```bash
ipfs pin add <CID>
```

### **Unpinning a File**
Unpinning a file allows it to be garbage collected.
```bash
ipfs pin rm <CID>
```

### **Checking Pinned Files**
```bash
ipfs pin ls
```

### **Swarm Peers**
View all connected peers in the IPFS network.
```bash
ipfs swarm peers
```

### **Swarm Addresses**
Display your node’s network addresses.
```bash
ipfs id
```

---

## **Configuration Guide**

### **Allow Remote API Access**
By default, the IPFS API only listens on `127.0.0.1` (localhost). To allow remote access, modify the configuration file:

1. Open the configuration file located at:
   ```
   ~/.ipfs/config
   ```
2. Find the `"API"` section and update it:
   ```json
   "API": "/ip4/0.0.0.0/tcp/5001"
   ```

3. Restart the IPFS daemon:
   ```bash
   ipfs daemon
   ```

---

## **Setting Up a Custom Gateway**

To set up a custom gateway for Cogni using your domain (e.g., `ipfs.cogni.host`), follow these steps:

1. **Set up Nginx as a reverse proxy**:
   ```nginx
   server {
       listen 80;
       server_name ipfs.cogni.host;

       location / {
           proxy_pass http://127.0.0.1:8080;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
       }
   }
   ```

2. **Enable HTTPS with Let’s Encrypt**:
   ```bash
   sudo certbot --nginx -d ipfs.cogni.host
   ```

---

## **Examples**

### **Uploading an AI Model**
```bash
ipfs add ai_model.h5
```
This will return a CID, which can be shared globally for retrieving the model.

### **Retrieving the AI Model**
```bash
ipfs cat <CID> > ai_model.h5
```

### **Pinning a Dataset**
```bash
ipfs pin add <dataset_CID>
```

---

## **Useful Resources**

- [Official IPFS Documentation](https://docs.ipfs.io/)
- [Go-IPFS GitHub Repository](https://github.com/ipfs/go-ipfs)
- [Cogni Documentation (Coming Soon)](#)

---

Feel free to contribute by submitting issues or pull requests to improve this guide!

---
