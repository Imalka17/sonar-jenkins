# SonarQube Integration with Jenkins

SonarQube : Login > Profile > My Account > Security > Generate Token

"Auth_Token_Jenkins": squ_3ef641a03e8177d7a0ef638f69fafc2414d15a59


# Jenkins Configuration for SonarQube

Manage Jenkins > Manage Plugins > Available [TAB] > Search For SonarQube > Install Plugins

Install Jenkins Plugins [SonarQube Scanner for Jenkin,Plain Credentials Plugin,Credentials Plugin]

## Add SonarQube Authentication Token Into Jenkins

Jenkins > Credentials > System > Global Credentials > Add Credentials

Kind: Secret test [squ_3ef641a03e8177d7a0ef638f69fafc2414d15a59]
Secret: SonarQube Authentication Token
Description: Provide a descriptive name

## Setup Sonar Scanner on Jenkins

Global Tool Configuration > SonarQube Scanner > [Manual Configuration]
[X]Uncheck Install automatically

Name: SonarqubeScanner-4.7
SONAR_RUNNER_HOME: /var/jenkins_home/sonar-scanner-4.7.0.2747-linux



### Create Webhook

Administration > Configuration > Webhooks > [Create]

Name: WebServer-Nodejs
URL: http://viqsonar.eastus.cloudapp.azure.com:8080/jenkins/sonarqube-webhook/


## Add SonarQube server to Jenkins environment

SonarQube servers > [X] Environment variables
Name: SonrQube
Server URL: http://viqsonar.eastus.cloudapp.azure.com:9000
Server authentication token: SonarQube-Acess-Token

# Integrate GitHub with Jenkins

## Configure GitHub - Add Jenkins server's public key into GitHub 

Profile > Settings > SSH and GPG Keys > [Add New SSH Key]

Titel: Jenkins_Auth
Key: [Add id_rsa.pub key here]

cat ~/.ssh/id_rsa.pub 

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC6jbMOPPaiQ5BSTSDrr8fYvemsQagIeo2fGqzoY9Pu6zPL/ffUH5q4aSN0muxwj2Lc/376SRJvM9eb9n5+EQ47kJ8f434CF8dpvFXTKwPAaJbkKlWSmQxOe1tFn0jziOvT37XG007EXnen+Dw74MvjedTR/Gbf8XEApuM+A8SB0/CFQoOmrggRbJk7LcAWGRRwXFEAcHtBY4zTxO1WXsK01G+afswpqwq29IDnJrRBLUShTUbjFm7TnLKcCRh/2NoMbAjoHvYil592/UhNIRILqJsh3aXNEbW36ILXvcdI6+CF8SILouLMRG0xCYnfr9nInCkIKFv7L/uRtGbECZcZ azureuser@SonaeQube-dem

## Configure Jenkins to acess private repo


Manage Jenkins > Manage Credentials > Global > [Add Credentials]


Kind: SSH Username with private key
Scope: Global
ID: Github_auth
Username: [any ID] Github_Auth
Private Key:

-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAuo2zDjz2okOQUk0g66/H2L3prEGoCHqNnxqs6GPT7uszy/33
1B+auGkjdJrscI9i3P9++kkSbzPXm/Z+fhEOO5CfH+N+AhfHabxV0ysDwGiW5CpV
kpkMTntbRZ9I84jr09+1xtNOxF53p/g8O+DL43nU0fxm3/FxAKbjPgPEgdPwhUKD
pq4IEWyZOy3AFhkUcFxRAHB7QWOM08TtVl7CtNRvmn7MKasKtvSA5ya0QS1EoU1G
4xZu05yynAkYf9jaDGwI6B72Ipefdv1ITSESC6ibId2lzRG1t+iC173HSOvghfEi
C6LizERtMQmJ36/ZyJwpCChb+y/7kbRmxAmXGQIDAQABAoIBAEfejzzM/7dDkDYk
wKoL7lHx2DQklzes/yJshHCDBQLmWe4cyX1PL6wb1Sz3Al/a3ZuGUsTZoeB1eHr9
W3311CXecW83lTP5NTnm9KmFyMw3fuon5Q+1JqiVnXQVCWXJOhFF/iG7Bn1gZ3iu
iYYH9ISOSw8azgc4XPCDWshpaysYcr9gDkuHHkQe6CQc80njKEdaq/La2Ce4t6s6
empQxQF+BEQjS55njmiDy/8Lbnxmk4er22E+6ZKvkrqjczfeFr7/tgkKZGnk9m3o
RbgxvtikejjCS/Nmz0gdoPBXMVq+UDQpmqsOV4XypHuPC/R6ZdVYBpzO4QbdGfdy
3YKJGIECgYEA6DWq/YV7TDn8v+oB3C2gPShpmFN3HMK1MqbD2xx3hHb4u0qXXr9l
S6Out2/ijbI0wcOaoHk5wLhGEAp3UwNlkvERsKjPQvYncj+qUqGZjDRjfAhgO5nO
nz6+yhUBgBc01QOBvih7nNaHia0SwAC9PZCEWsMAJxAvC7TM7J2H3RcCgYEAzaqT
Ktat7gTj4bjyjDv0mdntAoQF6VaZ6th10e8p7UP+CfK0+ePAQ0rlNsfRzZOfxY+C
Rj13/MXAB7JwiS8Nkrxh6yO6T67GzfUlqRepW447hVU54Q67b4x/78cIgmOF8Ldi
lfgm7DPubPFvFmh0c9OIHEELrRKbX0TtGt3Cq08CgYAHvtKHRk6Iil6d4CZTu8ne
gFyVUiNk+DGnENzzkA2Eg5tkU+acqHGuhjUrtTWvWEReOjIMLD766KqdmlvEjxZy
Qkw+wkK3jxJdwzXhL7a5cH3pAzaChmzX7vXaM70rEpsWh9lqCFunLZizxOwdL2kg
hpODm4GDzAxlrZAwTEjd3QKBgQCRmtfCFmbhAjlLjyK4waG0YqL3ivycbCFgMIuJ
a2clgWOTK2+REvsFKTsKA4G3p3IP7j/u9onCPUZsrJobpWJYpmI0lQDMdRJuscZN
5mCSXyoohWQKv+FXYgMZgLG3jjo/Z7W2Mw9rXoDIRE2/cYgwkGvmhO59Q5UYZ7Xt
tV6i5QKBgQCSKOtYYNPZXBOkUq3duv4SziP09oF4ozefwDZdb7m/t7XHiplWyLpk
dpe/vhhHMRwGm/rhM6emxpciUfjZDn4zQwaC2LFHJ8Hsf12AFLu8NIIED1KVuh9n
mPXCuDb1U69bd2lFZmFz+io8pgS+GYah2r79HBmKBm3u3rXcmcMJ1w==
-----END RSA PRIVATE KEY-----


## Setup Build Environment

Install "NodeJS" Plugin

Manage Jenkins > Global Tool Configuration > NodeJS

## Create Jenkins Project/Pipeline

New Item > Pipeline > [WebServer-Nodejs] 

Pipeline
    SCM: Git
    Repositories: 
        Reposiotry URL: git@github.com:dimuit86/nodejs-demo-app.git
        Crednetials: GitHub_Auth
        Branch: Main

# STEP 03: Integrate/Authenticate DockerHub with Jenkins

Install Docker Plugin

ACCESS TOKEN DESCRIPTION
DockerHub_Auth
ACCESS PERMISSIONS
Read, Write, Delete
To use the access token from your Docker CLI client:

1. Run docker login -u dimuit86

2. At the password prompt, enter the personal access token.

64171757-6173-4bec-b88d-b9cc78d1430e

Credentials → Global → Add credentials

Kind: username and password
UN: dimuit86
PW: 64171757-6173-4bec-b88d-b9cc78d1430e
ID: dockerhub_id

# SonarQube Configuration on Jenkins



Dashboard > Manage Jenkins > Configure System.

Name: SonarQube
Server URL: http://viqsonar.eastus.cloudapp.azure.com:9000
Server authentication token: SonarQube-Access-Token
 
# STEP 04: Adding Project to SonarQube

Manual Mode :
Login to SonarQube > Project > 

How do you want to create a project [Manually] > 
    Create a Project
        Project display name: node-js-react-npm-app
        Project key: node-js-react-npm-app

How do you want to analyze your repository? [With Jenkins]
    Select your DevOps platform [GitHub]

1. Install Install SonarQube Scanner plugin for Jenkins (Performed at step X)

2. Create a Pipeline Job on Jenkins
   1. New Item and create a Pipeline Job
   2. Under Build Triggers, choose Trigger builds remotely.
   3. Set parameters uder Pipeline section
        Definition: Pipeline script from SCM
        SCM: [Under "Branches to build" sbsction]
        Branch: Master
        Script Path: Jenkinsfile

3. Create a GitHub Webhook
   Create a Webhook in your repository to trigger the Jenkins job on push.
   1. Login to GitHub account and "Settings" under the project.
        Project [node-js-react-npm-app] > Settings > Webhook > Add Webhook > 
           Payload URL: "***JENKINS_SERVER_URL***/job/***JENKINS_JOB_NAME***/build token=***JENKINS_BUILD_TRIGGER_TOKEN***"
           Content type:
           Secret:
           Which events would you like to trigger this webhook: 
               [Let me select individual events.]: [X] Pushes
4. Configure Project Properties
   1. What option best describes your build? [Other(NodeJS)]
   2. Create a sonar-project.properties file in your repository and paste the following code:
   
      ```
      sonar.projectKey=node-js-react-npm-app
      ```
5. Create a Jenkinsfile

      ```
      node {
        stage('SCM') {
          checkout scm
        }
        stage('SonarQube Analysis') {
          def scannerHome = tool 'SonarScanner';
          withSonarQubeEnv() {
            sh "${scannerHome}/bin/sonar-scanner"
          }
        }
      }
      ```
      
    Note:  Make sure to replace SonarScanner with the name you gave to your SonarQube Scanner tool in Jenkins

