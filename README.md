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
Example output from this command can be seen below. I ran some tests earlier before inserting the command mentioned above, so you can see some of my previous test results!
<img width="775" height="237" alt="image" src="https://github.com/user-attachments/assets/699b518d-4e12-423d-8b15-0085e5651018" />



## 4.) Testing Endpoints 
There is a lot to go through here, so I will try to organize everything by splitting everything into 3 groups (convert, stats, and health)

### 4.1.) Health
First, it would be good to make sure everything is running as desired. We can use the code below to check:
```powershell
curl http://localhost:8080/health
```
You should get a response like the one below ('{"status":"ok"}') if everything is running as desired.
<img width="823" height="142" alt="image" src="https://github.com/user-attachments/assets/84f5d290-d612-4c65-97fc-9126507abcc6" />

Or, for a more detailed response, you can use the code below:
```powershell
curl -i http://localhost:8080/health
```
<img width="877" height="285" alt="image" src="https://github.com/user-attachments/assets/d5e97b88-46d1-4aad-99ec-cf186afc678a" />



### 4.2.) Convert & Stats
This also has multiple categories, so I will split them up in attempt to organize everything.

#### 4.2.1) Positive, Finite Numbers (Unless you don't count 0)
When a positive, finite number is entered, we want the output to be the number of lbs entered, the formula used to convert it to kgs, and the number of kgs we got in the end. Also, we would like the "conversions" key to increase by 1 each time we get this kind of result (all other results should not increase the counter). Before starting, I would like to mention that my "conversions" will start at 15, as I have run many examples before this which increased the "conversions" key previously.

Example 1 (Zero) :)
Example Input w/Stats Check:
```powershell
curl http://localhost:8080/convert?lbs=0
curl http://localhost:8080/stats
```
My results can be seen below.
<img width="933" height="218" alt="image" src="https://github.com/user-attachments/assets/c794289e-2b5a-4eab-909c-71673c3e97a3" />


Example 2 (Decimals) :)
Example Input w/Stats Check: 
```powershell
curl http://localhost:8080/convert?lbs=0.5
curl http://localhost:8080/stats
```
<img width="932" height="167" alt="image" src="https://github.com/user-attachments/assets/334889b6-cab9-441b-8f97-2ea3e4d8ed54" />


Example 3 (Positive Whole Number) :) 
Example Input w/Stats Check:
```powershell
curl http://localhost:8080/convert?lbs=200
curl http://localhost:8080/stats
```
<img width="938" height="172" alt="image" src="https://github.com/user-attachments/assets/e94b5d20-dc14-4c66-9d7e-8b8eebccbb84" />


#### 4.2.2) No Input
When no input is given, we should get an error message and our "conversions" value should not go up.
Example Input w/Stats Check:
```powershell
curl http://localhost:8080/convert
curl http://localhost:8080/stats
```
<img width="935" height="187" alt="image" src="https://github.com/user-attachments/assets/4f097379-3167-415c-a3d7-24742b06ddeb" />


#### 4.2.3) Negative or Non-Finite Numbers
When a negative or non-finite number is given, we should get an error and the "conversions" value should not increase.
Example Input w/Stats Check:
```powershell
curl http://localhost:8080/convert?lbs=-4
curl http://localhost:8080/stats
```
<img width="946" height="220" alt="image" src="https://github.com/user-attachments/assets/6d08f7ab-f0bf-428c-86a6-8c2f34b0e81d" />


#### 4.2.4) Non-Number Input
When input is not a number, we should get an error and the "conversions" value should not increase.
Example Input w/Stats Check: 
```powershell
curl http://localhost:8080/convert?lbs=abc
curl http://localhost:8080/stats
```
<img width="946" height="271" alt="image" src="https://github.com/user-attachments/assets/b2e53f9b-cf9b-4bcd-b353-743dedc69ef9" />

#### Extra:) Showing that "conversions" Value Remains Even If Containers are Removed and Re-Created
Even if the current Container is removed and/or re-created, the "conversions" value should remain as it was beforehand.
```powershell
curl http://localhost:8080/stats
docker compose down
docker compose up -d
curl http://localhost:8080/stats
```
<img width="857" height="586" alt="image" src="https://github.com/user-attachments/assets/742d3d86-bfad-415a-9cde-c35611b18b0b" />
















##
## 
