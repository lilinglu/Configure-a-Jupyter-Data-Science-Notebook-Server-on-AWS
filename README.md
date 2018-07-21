# Configure-a-Jupyter-Data-Science-Notebook-Server-on-AWS
git hub tutorial
## Step 1: Generating SSH keys 
1. Open Terminal.
2. Enter `ls ~/.ssh`  to see if you already have SSH keys.
3. If no such file or directory, we should generate a new SSH key.
  
   `mkdir -p .ssh`
   
   `ssh-keygen`
   
4. Enter `ls ~/.ssh` again, now you will see `id_rsa		id_rsa.pub`
 
## Step 2: Adding SSH key to GitHub account
1. Copy SSH keys to the Desktop.
   
   `cat ~/.ssh/id_rsa.pub`  
   
   `cat ~/.ssh/id_rsa.pub | pbcopy`
   
   `cp ~/.ssh/id_rsa.pub ~/Desktop/`
   
2. In the upper-right corner of any page, click your profile photo, then click Settings.
3. In the user settings sidebar, click SSH and GPG keys.
4. Click New SSH key or Add SSH key. Paste your key into the "Key" field.
5. Click Add SSH key.
6. Testing SSH connection

    Run `ssh git@github.com'
    We may see a warning like this:

   `The authenticity of host 'github.com (192.30.255.113)' can't be established.
    RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
    Are you sure you want to continue connecting (yes/no)? `
    
    Verify that the fingerprint in the message and type yes to continue

## Step 3: Create an Amazon EC2 instance
1. Register a AWS acount.
2. Create Key Pairs on EC2 dashboard.
3. Create Security Groups on EC2 dashboard.
4. Launch a t2.micro instance.
## Step 4: Configure my own jupyter data science notebook server on AWS.
1. Testing AWS Operating System connection.
   
   `ssh ubuntu@<IPv4 Public IP>`
   
    We may see a warning like this:
    
    `The authenticity of host '18.217.134.208 (18.217.134.208)' can't be established.
     ECDSA key fingerprint is SHA256:psiF3Q21VkGAPHJYMF53Z0YTel7OTa6Y9U1MxZw7Wso.
     Are you sure you want to continue connecting (yes/no)?`
     
     Verify that the fingerprint in the message and type yes to continue
   
  
2. Docker Installation.
   
   `curl -sSL https://get.docker.com | sh`
 
3. Adding my user to the "docker" group.
  
   `tmux` `sudo usermod -aG docker ubuntu`   *you will have to log out and back in for this to take effect!*

4. Obtaining the correct Docker image.

   `tmux` `docker pull jupyter/datascience-notebook
   
    If we see the `Status: Downloaded newer image for jupyter/datascience-notebook:latest` at the end, we got the correct         Docker image. 
5. Running the correct Docker image as a container.
   
   `docker run -p 443:8888 -v /home/ubuntu:/home/jovyan jupyter/datascienc-notebook` 
   
   *we will get a token here*
   **`token=b524ae0c6f5e2f5c77104738179185b74bd09f75f394f4f5`**
6. Now we can visit our own own jupyter data science notebook page with the token.
   
   go to the page `<IPv4 Public IP>:443` and enter the token
   
## A diagram of the overall system.
   
![ci_with_docker](https://user-images.githubusercontent.com/40584525/43027655-83261e00-8c30-11e8-89d7-e33408cbeff2.png)

## A detailed budget of the costs of running a Jupyter Data Science Notebook Server for three months using at least three        different kinds of EC 2 instances.
   * This budget was calculated on [Amazon calculator](https://calculator.s3.amazonaws.com/index.html).
   * Here I use three types of EC2 instances: Linux on t2.micro, Linux on t2.small, Linux on t2.nano.
   * According to the calculator, the totally monthly cost is $21.09. So we need $21.09 * 3 = $63.27 for three months.
   
   ![1532125885623](https://user-images.githubusercontent.com/40584525/43028003-1bfca738-8c32-11e8-9ff8-feeb32683905.png)
   
   ![1532126050008](https://user-images.githubusercontent.com/40584525/43028058-720f8d7a-8c32-11e8-9644-0cd4142025de.jpg)
