## Steps to Install Docker and Nginx and Run a Docker Container as a Reverse Proxy

### Step 1: Install Docker on Ubuntu

First, let\'s install Docker on your Ubuntu system.

1.  **Update the package index:**

          sudo apt update

2.  **Install the necessary packages for Docker:**

         sudo apt install apt-transport-https ca-certificates curl software-properties-common

3.  **Add Docker\'s official GPG key:**

         curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

2.  **Add the Docker repository to APT sources:**

        sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

3.  **Update the package index again to include Docker's repository:**

          sudo apt update

4.  **Install Docker CE (Community Edition):**

         sudo apt install docker-ce

5.  **Verify Docker installation:**

          docker --version

    *Docker version 24.0.5, build 123456*

6.  **Start and enable the Docker service:**

1.       sudo systemctl start docker

         sudo systemctl enable docker

2.  **Add your user to the Docker group (optional):**

    To run Docker commands without *sudo*, add your user to the Docker
    group:

          sudo usermod -aG docker \$USER

### Step 2: Install Nginx and Run It as a Docker Container

Now, let\'s set up Nginx in a Docker container and configure it as a
reverse proxy.

1.  **Pull the official Nginx Docker image:**

1.     docker pull nginx

2.  **Create a directory for Nginx configuration files:**

          mkdir -p \~/nginx-reverse-proxy

3.  **Create an Nginx configuration file for the reverse proxy:**

    Create a file named *default.conf* in the *\~/nginx-reverse-proxy*
    directory with the following content:

        server {
          listen 80;
          server_name your_domain_or_IP;

          location / {
              proxy_pass http://your_backend_service:port;
              proxy_set_header Host $host;
              proxy_set_header X-Real-IP $remote_addr;
              proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
              proxy_set_header X-Forwarded-Proto $scheme;
          }
         }

    Replace *your_domain_or_IP* with your domain or IP address and
    *your_backend_service:port* with the address and port of the service
    you want to reverse proxy to.

4.  **Run the Nginx Docker container:**

         docker run -d --name nginx-reverse-proxy -p 80:80 -v ~/nginx-reverse-proxy:/etc/nginx/conf.d nginx

    This command will run the Nginx container in detached mode (*-d*),
    map port 80 on the host to port 80 in the container (*-p 80:80*),
    and mount the configuration directory (*-v
    \~/nginx-reverse-proxy:/etc/nginx/conf.d*) to the container.

### Step 3: Verify the Setup

1.  **Check the running Docker containers:**

          docker ps

    You should see an output similar to this:

    *CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES*

    *abc12345 nginx \"/docker-entrypoint....\" 5 seconds ago Up 5
    seconds 0.0.0.0:80-\>80/tcp nginx-reverse-proxy*

2.  **Verify Nginx is running:**

    Open a web browser and go to your server\'s IP address or domain
    name. You should see the Nginx welcome page or the content served by
    your backend service.

### Screenshots and Documentation

I will take a screenshot of the running Nginx and Docker container and
provide a Markdown file with the instructions.

### Step 4: Generate Screenshots

Let\'s generate the screenshots of the running Docker container and the
Nginx server.

1.  **Capture the Docker container status:**
2.  **Capture the Nginx welcome page:**

### Step 5: Create Markdown Documentation

Here is the Markdown file containing the instructions:

*\# Installing Docker and Nginx and Running Nginx as a Reverse Proxy*

*\## Step 1: Install Docker on Ubuntu*

*1. \*\*Update the package index:\*\**

      sudo apt update

2.  **Install the necessary packages for Docker:**

         sudo apt install apt-transport-https ca-certificates curl software-properties-common

3.  **Add Docker\'s official GPG key:**

         curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

4.  **Add the Docker repository to APT sources:**

          sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

5.  **Update the package index again to include Docker's repository:**

          sudo apt update

6.  **Install Docker CE (Community Edition):**

          sudo apt install docker-ce

7.  **Verify Docker installation:**

          docker --version

    *Docker version 24.0.5, build 123456*

8.  **Start and enable the Docker service:**

         sudo systemctl start docker

         sudo systemctl enable docker

3.  **Add your user to the Docker group (optional):**

    To run Docker commands without *sudo*, add your user to the Docker
    group:

          sudo usermod -aG docker \$USER

    Log out and back in for the changes to take effect.

## Step 2: Install Nginx and Run It as a Docker Container

1.  **Pull the official Nginx Docker image:**

          docker pull nginx

2.  **Create a directory for Nginx configuration files:**

          mkdir -p \~/nginx-reverse-proxy

3.  **Create an Nginx configuration file for the reverse proxy:**

    Create a file named *default.conf* in the *\~/nginx-reverse-proxy*
    directory with the following content:

          server {

          listen 80;

          server_name your_domain_or_IP;

          location / {

          proxy_pass http://your_backend_service:port;

          proxy_set_header Host \$host;

          proxy_set_header X-Real-IP \$remote_addr;*

          proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;*

          proxy_set_header X-Forwarded-Proto \$scheme;*

          }

          }

1.  
2.  **Run the Nginx Docker container:**

1.     docker run -d \--name nginx-reverse-proxy -p 80:80 -v\~/nginx-reverse-proxy:/etc/nginx/conf.d nginx

    This command will run the Nginx container in detached mode (*-d*),
    map port 80 on the host to port 80 in the container (*-p 80:80*),
    and mount the configuration directory (*-v
    \~/nginx-reverse-proxy:/etc/nginx/conf.d*) to the container.

## Step 3: Verify the Setup

1.  **Check the running Docker containers:**

          docker ps

    You should see an output similar to this:

    *CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES*

    *abc12345 nginx \"/docker-entrypoint....\" 5 seconds ago Up 5
    seconds 0.0.0.0:80-\>80/tcp nginx-reverse-proxy*

2.  **Verify Nginx is running:** <br  />

         sudo systemctl status nginx
