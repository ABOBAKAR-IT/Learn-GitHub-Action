# GitHub Actions Workflows
- GitHub Actions uses YAML syntax to define the workflow. Each workflow is stored as a separate YAML file in your code repository, in a directory named `.github/workflows`.
- In the .github/workflows/ directory, create a new file called `github-actions.yml` and add the following code.


# CI/CD pipeline for update static website on linux VPS
## 1
```
name: remote ssh command
on: [push]
jobs:

  build:
    name: Build
    runs-on: ubuntu-latest
    steps:
    - name: executing remote ssh commands using password
      uses: appleboy/ssh-action@master
      with:
        host: 20.68.108.xx
        username: xxx
        password: LinuxXXX786
        port: 22
        script: |
          cd /var/www/abobakar.tech
          sudo git pull 
          echo $?
          echo "welcome to server"

```
## 2 Using GitHub Secrets keys
```
name: CI/CD for static website deploy in Linux VPS
on:
  push: 
    branches: [ master ]
jobs:

  build:
    name: Build
    runs-on: ubuntu-latest
    environment: dev_portfolio
    steps:
    - name: executing remote ssh commands using password
      uses: appleboy/ssh-action@master
      with:
        host: ${{ secrets.HOST_IP }} 
        username: ${{ secrets.HOST_NAME }} 
        password: ${{ secrets.HOST_PASSWD }} 
        port: 22
        script: |
          cd /var/www/abobakar.tech
          sudo git pull
          if [[ $? ]]
          then
          echo "Congratulation Website Update"
          else
          echo " Website Not Update"
          fi


```

# CI/CD pipeline for update Nodejs website on linux VPS
```
name: CI/CD for Nodejs website deploy in Linux VPS
on:
  push: 
    branches: [ node-file ]
jobs:

  build:
    name: Build
    runs-on: ubuntu-latest
    environment: dev_portfolio
    steps:
    - name: executing remote ssh commands using password
      uses: appleboy/ssh-action@master
      with:
        host: ${{ secrets.HOST_IP }} 
        username: ${{ secrets.HOST_NAME }} 
        password: ${{ secrets.HOST_PASSWD }} 
        port: 22
        script: |
          cd /var/www/static-portfolio-github-action
          pm2 stop server
          pm2 delete server
          sudo git pull
          sudo npm install
          pm2 start server.js
          if [[ $? ]]
          then
          echo "Congratulation Website Update"
          else
          echo " Website Not Update"
          fi
          exit

```
