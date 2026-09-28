# CS454-Project1
Project 1 of CS454 course (Intro to Cloud Computing) Meant to be a Portable-Containerized-REST-Service


## 1.) Prerequisites
To run this properly, the user will need Docker with Docker Compose. 
Before moving on, to be extra safe, I would recommend running these 2 lines of code in Command Prompt and/or PowerShell to ensure you have both:
```powershell
docker --version
docker compose version
```


## 2.) Building and Starting the Application
The 2 lines of compose code below build (1st line) and start (2nd line) the application.
```powershell
docker compose build
docker compose up -d
```


## 3.) How to View logs and Inspect Running Services.
You can double check that the application has been successfully built and has started by running:
```powershell
docker compose ps
```
Pretty much, we are checking our current containers and what is currently running. 

An example of my results can be shown below.
<img width="1852" height="145" alt="image" src="https://github.com/user-attachments/assets/5d5e44a8-80f1-4016-b941-20f48ccf9a22" />

To view logs, we can use the code seen below:
```powershell
docker compose logs api
```
An example of my results can be shown below. I ran some tests earlier before inserting the command mentioned above, so you can see some of my previous results!
<img width="775" height="237" alt="image" src="https://github.com/user-attachments/assets/699b518d-4e12-423d-8b15-0085e5651018" />



## 4.) How to stop and clean up the application.
## 



##
## 
