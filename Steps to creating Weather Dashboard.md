
![github-header-image](https://github.com/user-attachments/assets/7f893a01-4364-424d-b33d-dfb5444d47f0)

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

Collect Data from the Weather app API and store it in a S3 bucket
&nbsp;
&nbsp;
&nbsp;
<br>This Diagram explains the architecture of the project</br>
<center><img width="453" alt="Screenshot 2025-01-07 at 1 48 51 PM" src="https://github.com/user-attachments/assets/ac771a5b-441a-482b-abf6-29e144734325" /></center>

&nbsp;
&nbsp;
&nbsp;
&nbsp;

  
1. Go over to Open Weather App website and create an account in order to generate your API key <a href="https://openweathermap.org" target="_blank">Visit OpenWeatherMap</a>
   
![Screenshot 2025-01-11 at 6 05 43 PM](https://github.com/user-attachments/assets/787adef6-2d90-4792-8216-2759b0aff21b)



&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

2. Now click your username and then click on your API keys and copy this API for later

![Screenshot 2025-01-11 at 7 19 16 PM](https://github.com/user-attachments/assets/9337b93c-4898-4de3-b79e-18162423297d)



&nbsp;
&nbsp;
&nbsp;
&nbsp;




<br> 3. Make a directory for your project. I name mine DevOpsProjects and Weather-Dasboard-Demo but you can name it whatever you would like 
<br> ![Screenshot 2025-01-07 at 1 58 19 PM](https://github.com/user-attachments/assets/0a23f0d2-7c48-43a2-a774-a024996f6d09) </br>
&nbsp;
&nbsp;
&nbsp;
&nbsp;


```bash
mkdir DevOpsProjects
cd DevOpsProjects
mkdir Weather-Dashboard-Demo
cd Weather-Dashboard-Demo
mkdir src tests data
```

<br>4. Continue making directories </br>
<br><img width="1238" alt="Screenshot 2025-01-11 at 8 43 57 PM" src="https://github.com/user-attachments/assets/7ce19f86-cb0f-4e49-ae2b-cb0234731d56" /></br>

```bash
mkdir src tests data
```

<br>5. Create two files that will hold the python code to be stored in the src directory. These specific files are to power up the weather dashboard and the init script

<br> Intialiaze git
<br> ![Screenshot 2025-01-07 at 3 09 44 PM](https://github.com/user-attachments/assets/abf62f64-f304-4c89-b75e-c0f5f26e906b) </br>

```bash
git init
```


Ignore python cache files and any zip files from git repository.
<br>![Screenshot 2025-01-11 at 11 08 33 PM](https://github.com/user-attachments/assets/ed39297d-6830-4ea3-aa7b-c257bc482d66)</br>

```bash
echo "__pycache__/" >> .gitignore
echo "*.zip" >> .gitignore
```

<br>Append 3 packages to the requirements text file using echo cmd. Specify the version for package.</br>
&nbsp;
&nbsp;
<br>boto3: A library for interacting with Amazon Web Services (AWS) to manage cloud resources.</br> 
<br>python-dotenv: A tool to load environment variables from a .env file into your Python app, for managing sensitive data like API keys.</br> 
<br>requests: A library for making HTTP requests, such as sending and receiving data from websites or APIs.</br>
&nbsp;
<br>![Screenshot 2025-01-11 at 11 21 16 PM](https://github.com/user-attachments/assets/63d3fe13-3eeb-43d8-a4a4-a08c239ea0e1)</br>

```bash
echo "boto3==1.26.137" >> requirements.txt
echo "python-dotenv==1.0.0" >> requirements.txt
echo "requests==2.28.2" >> requirements.txt
```

You will need to be in the venv environment in order to continue on with the rest of the commands that include python
<br> ![Screenshot 2025-01-07 at 5 59 11 PM](https://github.com/user-attachments/assets/0b698b8a-88fb-4635-b7d0-2599228cbaa3) </br>
 
```bash
python3 -m venv venv
sudo apt install python3.12-venv
python3 -m venv venv
source venv/bin/activate
```
Install pip dependencies to the requirements txt file.

```bash
pip install -r requirements.txt
```
Configure AWS to enter credentials for access 

<br>![Screenshot 2025-01-12 at 12 29 38 AM](https://github.com/user-attachments/assets/523603f1-20e7-4726-8703-e10aea171c81)</br>

```bash
aws configure
```
Go to your AWS account. Login and in the search bar type in IAM. You are now going to retrieve yout AWS Access Key ID, AWS Secret Access Key and your Default region name.

<br>![Screenshot 2025-01-12 at 12 17 34 AM](https://github.com/user-attachments/assets/2bbcc0f0-dcc8-4a2d-be9a-dc3a878a8769)</br>

You will click on security credentials and the you will click create access key 

<br><img width="954" alt="Screenshot 2025-01-07 at 4 18 08 PM" src="https://github.com/user-attachments/assets/d8853f0c-f52f-43ab-be08-de7e56129787" /></br>

Then your access key will be revealed. Please save your access key and secret access key for later use.

<br> <img width="914" alt="Screenshot 2025-01-07 at 4 19 40 PM" src="https://github.com/user-attachments/assets/50995631-bbd6-441c-a2f8-6ee39fbee4e5" /> </br>

Then you will go back to the command line to input the following information. Your access key and your secret access key. It will also prompt you to enter the region name and the output format which is json.

<br>![Screenshot 2025-01-12 at 12 31 29 AM](https://github.com/user-attachments/assets/a2c1e568-cd9a-42a8-b721-d9b594fe7cdb)</br>

Create a variable for the Weather API and redirect to the environment variable file. 
<br><img width="1033" alt="Screenshot 2025-01-12 at 1 12 39 AM" src="https://github.com/user-attachments/assets/1a41d8fb-ff7b-4357-98b1-3c792e28ef3d" /></br>

```bash
echo "OPENWEATHER_API KEY= " enter the api key here ">> .env
```
                                                                                                                                                        

<br> Then you will create a random generated s3 bucket name that is redirected to the environment variable file </br>
<br> You will now generate your python code </br>
<br> ![Screenshot 2025-01-07 at 5 45 42 PM](https://github.com/user-attachments/assets/e2b1b23e-0350-4381-aaa5-7c1ef9420a3a) </br>
```bash
echo "AWS_BUCKET_NAME=weather-dashboard-${RANDOM}" >> .env
```
```bash
python3 src/weather_dashboard.py
```

Once you run that code you will be able to see the AWS a3 bucket and confirm its creation under general purpose buckets
<br> <img width="1151" alt="Screenshot 2025-01-07 at 5 46 42 PM" src="https://github.com/user-attachments/assets/d65bc874-734c-4785-bebd-fc069c05b390" /> </br>

Then click on the weather-data to see the three objects you also created
<br> <img width="1137" alt="Screenshot 2025-01-07 at 5 50 42 PM" src="https://github.com/user-attachments/assets/bba7a8ea-fd08-4150-afd6-eae203e77065" /> </br>

Here are the three objects you have created.
<br><img width="1136" alt="Screenshot 2025-01-07 at 5 51 05 PM" src="https://github.com/user-attachments/assets/7a11232e-6a30-448c-82a7-3abd25ef0375" /> </br>
















