# Configure-a-Jupyter-Data-Science-Notebook-Server-on-AWS
git hub tutorial
## Generating SSH keys 
1. Open Terminal.
2. Enter `ls ~/.ssh`  to see if you already have SSH keys.
3. If no such file or directory, we should generate a new SSH key.
  
   `mkdir -p .ssh`
   
   `ssh-keygen`
   
4. Copy SSH keys to the Desktop.
   
   `cat ~/.ssh/id_rsa.pub`  
   
   `cat ~/.ssh/id_rsa.pub | pbcopy`
   
   `cp ~/.ssh/id_rsa.pub ~/Desktop/`
   
## Adding SSH key to your GitHub account
1. `ssh git@github.com`
## Create an Amazon EC2 instance
1. Register a AWS acount.
2. Create Key Pairs on EC2 dashboard.
3. Create Security Groups on EC2 dashboard.
4. Launch a t2.micro instance.
## Configure my own jupyter data science notebook server on AWS.
1. Running on my AWS Operating System.
   
   `ssh ubuntu@<IPv4 Public IP>`
  
2. Docker Installation.
   
   `curl -sSL https://get.docker.com | sh`
 
3. Adding my user to the "docker" group.
  
   `tmux` `sudo usermod -aG docker ubuntu`   *you will have to log out and back in for this to take effect!*

4. Obtaining the correct Docker image.

   `tmux` `docker pull jupyter/datascience-notebook
   
5. Running the correct Docker image as a container.
   
   `docker run -p 443:8888 -v /home/ubuntu:/home/jovyan jupyter/datascienc-notebook` *we will get a token here*
6. Now we can visit our own own jupyter data science notebook page with the token.
   
   URL: <IPv4 Public IP>:443  and enter your token
   
