STEP 1: 
# 🚀 Flask DevOps App
A simple Dockerized Flask application deployed on **AWS EC2** with **Nginx** as a reverse proxy — built to showcase end-to-end DevOps deployment skills.

---

STEP 2: 
## 🛠️ Tech Stack

- **Flask** – A lightweight Python web framework for building the application.
- **Docker** – Containerized the entire application for consistent environments.
- **AWS EC2 (Ubuntu)** – Hosted the app on an AWS EC2 instance running Ubuntu 22.04.
- **Nginx** – Set up as a reverse proxy to forward traffic to the Flask app on port 5000.

---

 STEP 3: 
 ## 🌐 Live Demo

[http://your-ec2-public-ip](http://your-ec2-public-ip)

---

STEP 4: How to Run Locally (With Docker)
## 📦 How to Run Locally (With Docker)

1. Clone the repository:
   git clone https://github.com/swethad28/flask-devops-app.git
   cd flask-devops-app
2. Build the Docker image:
   docker build -t flask-app .
3. Run the container:
   docker run -p 5000:5000 flask-app
4. Visit the app in your browser:
   http://localhost:5000
---

STEP 5: Deployment (AWS EC2 + Docker + Nginx)
## ☁️ Deployment (AWS EC2 + Docker + Nginx)

This app was deployed on an AWS EC2 instance using the following steps:

1. **Launch EC2 instance** (Ubuntu 22.04, t2.micro):
   - Go to [AWS EC2 Dashboard](https://aws.amazon.com/ec2/)
   - Launch a new instance with **Ubuntu 22.04** and **t2.micro** type
   - Ensure you have SSH access (through key pairs)

2. **Install Docker**:
   - SSH into the EC2 instance:
     ```bash
     ssh -i "your-key-name.pem" ubuntu@your-ec2-public-ip
     ```
   - Update the package list and install Docker:
     ```bash
     sudo apt update
     sudo apt install -y docker.io
     sudo systemctl start docker
     sudo systemctl enable docker
     ```

3. **Clone the GitHub repository**:
   - Clone the repository containing the Flask app:
     ```bash
     git clone https://github.com/swethad28/flask-devops-app.git
     cd flask-devops-app
     ```

4. **Build and Run Docker Container**:
   - Build the Docker image:
     ```bash
     sudo docker build -t flask-app .
     ```
   - Run the container:
     ```bash
     sudo docker run -d -p 5000:5000 flask-app
     ```

5. **Install and Configure Nginx**:
   - Install Nginx:
     ```bash
     sudo apt install -y nginx
     ```
   - Configure Nginx as a reverse proxy to forward traffic to the Flask app running on port 5000. Edit the default Nginx config file:
     ```bash
     sudo nano /etc/nginx/sites-available/default
     ```
     Replace the `location /` block with:
     ```nginx
     location / {
         proxy_pass http://127.0.0.1:5000;
         proxy_set_header Host $host;
         proxy_set_header X-Real-IP $remote_addr;
         proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
         proxy_set_header X-Forwarded-Proto $scheme;
     }
     ```

6. **Restart Nginx**:
   - Restart Nginx to apply the changes:
     ```bash
     sudo systemctl restart nginx
     ```

7. **Access the app**:
   - Now, your Flask app should be accessible via:
     ```
     http://your-ec2-public-ip
     ```
     (Replace `your-ec2-public-ip` with your EC2 public IP address).

