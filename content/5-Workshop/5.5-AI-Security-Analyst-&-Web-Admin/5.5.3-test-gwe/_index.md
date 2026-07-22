---
title : "Connecting from the Bastion Host to the private EC2 instance and preparing the AI ​​environment"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.5.3 </b> "
---

### Connecting from Bastion Host to Sandbox

![alt text](image.png)

### Checking for Python and Sandbox Libraries

- After successfully connecting, the next step is to update the system: **sudo dnf update -y**

- Check for Python; if not installed, use the command: **sudo dnf install python3 -y**

- Check for pip; if not installed, use the command: **sudo dnf install python3-pip -y**

![alt text](image-1.png)

### Creating the AI ​​Directory and Activating the Environment

- Use the command **mkdir ai-server** to create the directory

- Use the command **python3 -m venv venv** to create the environment

- Use the command **source venv/bin/activate** to activate the virtual environment

![alt text](image-2.png)

### Upgrading pip

![alt text](image-3.png)

### Installing Libraries in the AI ​​Directory

- Use the command **pip install flask** to install Flask

- Use the command **pip install tensorflow** to install TensorFlow

- Use the command **pip install numpy** to install NumPy

- Use the command **pip install pandas** to install Pandas

- Use the command **pip install scikit-learn** to install scikit-learn

- Use the command **pip install requests** to install Requests

- Use the command **pip install beautifulsoup4** to install BeautifulSoup

![alt text](image-4.png)

### Uploading Source Code to the Sandbox

- Upload source code from the local machine -> Bastion Host (EC2 public) -> Sandbox

- First, use the command **scp -i "C:\Users\ASUS\Downloads\sandbox-key.pem" -r AI_Project ubuntu@44.214.180.89:~** to upload to the Bastion Host; then, from the Bastion Host, copy the code to the Sandbox using the command **scp -i ~/sandbox-key.pem -r AI_Project ec2-user@10.0.1.xxx:~**

![alt text](image-5.png)

### Launching the Environment school

![alt text](image-6.png)













