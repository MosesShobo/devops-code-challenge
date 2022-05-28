# Overview
This repository contains a React frontend, and an Express backend that the frontend connects to.

# Objective
Deploy the frontend and backend to somewhere publicly accessible over the internet. The AWS Free Tier should be more than sufficient to run this project, but you may use any platform and tooling you'd like for your solution.

Fork this repo as a base. You may change any code in this repository to suit the infrastructure you build in this code challenge.

# Submission
1. A github repo that has been forked from this repo with all your code.
2. Modify this README file with instructions for:
* Any tools needed to deploy your infrastructure
* All the steps needed to repeat your deployment process
* URLs to the your deployed frontend.

# Evaluation
You will be evaluated on the ease to replicate your infrastructure. This is a combination of quality of the instructions, as well as any scripts to automate the overall setup process.

# Setup your environment
Install nodejs. Binaries and installers can be found on nodejs.org.
https://nodejs.org/en/download/

For macOS or Linux, Nodejs can usually be found in your preferred package manager.
https://nodejs.org/en/download/package-manager/

Depending on the Linux distribution, the Node Package Manager `npm` may need to be installed separately.

# Running the project
The backend and the frontend will need to run on separate processes. The backend should be started first.
```
cd backend
npm ci
npm start
```
The backend should response to a GET request on `localhost:8080`.

With the backend started, the frontend can be started.
```
cd frontend
npm ci
npm start
```
The frontend can be accessed at `localhost:3000`. If the frontend successfully connects to the backend, a message saying "SUCCESS" followed by a guid should be displayed on the screen.  If the connection failed, an error message will be displayed on the screen.

# Configuration
The frontend has a configuration file at `frontend/src/config.js` that defines the URL to call the backend. This URL is used on `frontend/src/App.js#12`, where the front end will make the GET call during the initial load of the page.

The backend has a configuration file at `backend/config.js` that defines the host that the frontend will be calling from. This URL is used in the `Access-Control-Allow-Origin` CORS header, read in `backend/index.js#14`

# Setup EC2 Server

![Select Ec2 Instance](https://github.com/MosesShobo/devops-code-challenge/blob/main/doc/Select-Ec2-console.png)

Create Ec2 instance

![Launch Ec2 Instance](https://github.com/MosesShobo/devops-code-challenge/blob/main/doc/Select-Launch-instance.png)
![Select Free tier](https://github.com/MosesShobo/devops-code-challenge/blob/main/doc/select-free-tier.png)

### Create Key

![Connect to Ec2 and Verify SSH](https://github.com/MosesShobo/devops-code-challenge/blob/main/doc/Create-key-pair.png)
![Connect to Ec2 and Verify SSH](https://github.com/MosesShobo/devops-code-challenge/blob/main/doc/verify-node-via-ssh.png)


### Verify Access

![Update Security group and allow traffic](https://github.com/MosesShobo/devops-code-challenge/blob/main/doc/update-security-group.png)



### Init Data:

![User Data](https://github.com/MosesShobo/devops-code-challenge/blob/main/doc/add-user-data.png)

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
nvm install —lts
node -v
yum install git -y
npm install pm2 -g
git clone https://github.com/MosesShobo/devops-code-challenge.git
cd backend/
npm install
cd ..
cd frontend
npm install

```

# Process Manager

![Pm2 Process Manager](https://github.com/MosesShobo/devops-code-challenge/blob/main/doc/pm2-processmanager.png)


To keep application up and running we need process manager that will keep the app running all the time on remote server

```shell
cd frontend
pm2 start npm --name "frontend-app" -- start
cd backend
pm2 start npm --name "backend-app" -- start
```


# Optional Extras
The core requirement for this challenge is to get the provided application up and running for consumption over the public internet. That being said, there are some opportunities in this code challenge to demonstrate your skill sets that are above and beyond the core requirement.

A few examples of extras for this coding challenge:
1. Dockerizing the application
2. Scripts to set up the infrastructure
3. Providing a pipeline for the application deployment
4. Running the application in a serverless environment

This is not an exhaustive list of extra features that could be added to this code challenge. At the end of the day, this section is for you to demonstrate any skills you want to show that’s not captured in the core requirement.



