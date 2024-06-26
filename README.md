# resi.ai

Resi.ai is a cutting-edge flask web application designed to revolutionize the way professionals approach job applications. By leveraging the power of OpenAI's API, resi.ai provides personalized and automated assistance for creating tailored resumes and cover letters, making job applications more efficient and effective. See the [Video Demo](https://youtu.be/K7PYrwhXaPg) for a quick demo on how to use this project. The project is available at [www.useresi.com](https://www.useresi.com/register)

## Table of Contents
- [Background](#background)
- [Dependencies](#dependencies)
- [Installation](#installation)
- [Usage](#usage)
- [Features](#features)
- [File Breakdown](#file-breakdown)
- [Design Decisions](#design-decisions) 
- [Contributing](#contributing)
- [Credits](#credits)
- [License](#license)

## Background
### Problem:
Applying for jobs has gotten noticeably more difficult over the past few years. More companies are using advanced AI technologies to quickly screen candidates for potential job openings, and job boards like Indeed and LinkedIn make it trivially easy to post a new job opening to thousands of people in seconds. Applying for a job now feels like a question of quantity rather than quality.

### Solution:
This web application aims to give some of the power back to the job seekers by providing them with an easy to use tool to quickly create quality resumes customized to the job description leveraging the power of AI. All they will need is a working OpenAI API Key, an existing resume, and the job description. All of the prompting is handled by this program, so it is as easy as copying and pasting a resume and job description.

## Dependencies
This project requires the following Python libraries and packages. Ensure you have them installed to run the project successfully:

- `cs50`: For connecting the SQLite database to the Application Configuration.
- `cryptography`: For encryption of user's data before storage in the database.
- `flask`: For lightweight web application framework.
- `flask_session`: For support for sever-side sessions maintaining state and store data across different requests.
- `functools`: For providing utilities for caching, cumulative operations, and partial functions.
- `markdown`: For converting markdown language to HTML for display on website.
- `openai`: For access to OpenAI's Artificial Intelligence models.
- `os`: For retrieving environment variables for the database.
- `re`: For performing pattern matching and substitution on strings using regular expressions
- `werkzeug`: For hashing passwords before they are stored in the database for security.

You can use the following pip command to install the required Python packages from the `requirements.txt` file:

```bash
pip install -r requirements.txt
```

## Installation
This project is active and accessible at [useresi.com](https://www.useresi.com/register).

If you wish to run this project on your local machine, follow the steps below:

### Local Installation
This project is built using Python and requires a Python environment to run. Follow these steps to set up and run the project on your local machine.

#### Prerequisites
- Python 3.7 or newer
- pip (Python package installer)

#### Clone the repository
First, clone the repository to your local machine:

```bash
git clone https://github.com/jadonvanyo/resi.ai.git
cd resi.ai
```

#### Setup Python Virtual Environment
It's recommended to use a virtual environment for Python projects to manage dependencies. Create and activate a virtual environment:

```bash
python -m venv venv
# On Windows
venv\Scripts\activate
# On MacOS/Linux
source venv/bin/activate
```

#### Install Dependencies
Install the required Python libraries mentioned in the [Dependencies](#dependencies) section from the `requirements.txt` file using pip:

```bash
pip install -r requirements.txt
```

#### Final Steps
After completing the above steps, you should be ready to use the project. Proceed to the [Usage](#usage) section for instructions on running the project and analyzing potential investment properties.

## Usage
This project is active and accessible at [useresi.com](https://www.useresi.com/register).

If you wish to run this on your local machine, follow the steps below:

### Local Usage
1. Navigate to the resi.ai directory if you are not already there:

```bash
cd resi.ai
```
2. Next, open `app.py` and replace the following code:
```python
uri = os.getenv("DATABASE_URL")
if uri.startswith("postgres://"):
    uri = uri.replace("postgres://", "postgresql://")
db = SQL(uri)
```
with
```python
db = SQL("sqlite:///resi.db")
```
Save `app.py`.

3. Run the flask application in the command line:
```bash
flask run
```

4. Hold the `cmd` key and click the 'http://127.0.0.1:5000' link in the terminal window to access the application in your preferred browser.

5. Use the web application based on the prompts given within the application.

## Features
resi.ai tailors resumes and cover letters to fit a specific job description. Here are the key features that make resi.ai stand out:

### Tailored Resumes
Create expertly tailored resumes that are specifically optimized for a target job description. Simply input your target job title, industry, company, and job description, along with your existing resume, and let resi.ai generate a resume that highlights the most relevant experiences and skills for your desired role. The application uses OpenAI's API to identify and include the 3 most important job responsibilities in your tailored resume, ensuring your application stands out to potential employers.

### Dynamic Account Management
Easily manage your account settings including email, password, and OpenAI API key. Your resume is securely stored and autofilled in relevant fields to save you time. Updates to your account are made in real time using AJAX, ensuring a seamless user experience without the need for page reloads.

### Enter API Key
For new users, resi.ai offers a straightforward guide on how to set up your OpenAI API key. Enter your key through a user-friendly interface to start leveraging the power of AI in crafting your job application documents.

### Tailored Cover Letters
Generate ideas for your cover letter or complete cover letters tailored to your application. Specify details such as your current/previous job title, target job title, target company, and job description. resi.ai utilizes AJAX to deliver your custom cover letter, tailored using the OpenAI API to match your job application needs.

### Document History
Track your last 5 generated documents with ease. resi.ai stores your documents in a history table, allowing you to access and review them anytime. This feature is particularly useful for managing multiple job applications and ensuring consistency across your documents.

### Security and Privacy
resi.ai takes your privacy and security seriously. Passwords are hashed, and OpenAI API keys are encrypted before being stored in the database, ensuring your sensitive information is protected.

## File Breakdown
### HTML Pages:
#### Account:
This page allows the user to update their email, password, OpenAI API key, and resume. Once saved in the database, the resume will autofill into any felids that require a resume to improve user experience. When the user clicks the update button, the website uses **A**synchronous **J**avaScript **A**nd **X**ML (**AJAX**) to send a request for the account function from the Flask backend. The Flask backend will determine whether to return an error or update the user's information in the resi.db database using SQLite, and dynamically update the webpage using AJAX to display an alert message below the submit button showing what was wrong or what was updated. The user's password will be hashed and OpenAI API Key will be encrypted for security any time they are updated on this page.

#### Enter API:
This is the page the user is redirected to after registering for the first time. The webpage will give the user a explanation on how to set up their OpenAI API key and at the bottom of the page, it provides the user an input box to enter the API key they have generated. If the user clicks the "Enter API Key" button, the website will send a request for the api_key function from the Flask backend. The Flask backend will determine whether to return an error or encrypt and update the user's OpenAI API Key in the resi.db database with the encrypted key, and dynamically update the webpage using AJAX to display an alert message below the submit button showing what was wrong or that the API Key was successfully updated. The user can update their API Key at any time from this page.

#### Tailored Cover Letter
This feature allows the user to create a complete or partial cover letter for their target job. There are options to choose if the user wants a full or partial cover letter with information icons that display tooltips when hovered over. The user is prompted to enter their current/previous job title, target job title, target company, target job description, and an existing resume. When the user selects the "Submit Cover Letter" button, the website uses AJAX to update the web page to show a loading indicator and send a request for the `tailor_cover_letter` function from the Flask backend. The Flask backend will determine whether to return an error or use OpenAI's API to return a cover letter tailored to the user's inputs and dynamically update the page to display the tailored cover letter using JavaScript.

#### Tailored Resumes:
This is the main feature of this web application. This page gives the user all the fields that are required to create an expert resume writer to tailor their resume to their target job description. The user just needs to enter their target job title, target industry, target company, target job description, and an existing resume. When the user selects the "Submit Resume" button, the website uses AJAX to update the web page to show a loading indicator and send a request for the index function from the Flask backend. The Flask backend will determine whether to return an error or use OpenAI's API to return the 3 most important responsibilities of the job, a tailored resume, and a list of all the differences between the two and the page is dynamically updated again with all the information using JavaScript.

#### History:
This feature allows the user to view the last 5 documents that they have generated. The documents are pulled from the history table in the resi.db database and displayed in a collapsible accordion for easy viewing. The oldest document in the history is replaced whenever the user generates a new document in the index function. The old documents are displayed from newest to oldest and include the target job title, target company, document type, and when it was generated.

### app.py:
This file contains all the necessary routes for the web application: index, about, account, api_key, history, login, logout, register, and personalized_tutor.

#### Index:
This route handles the main feature of this web application: Tailoring the user's resume to a job description. 

When accessed using "POST", this route will ensure the user entered a target job title, target industry, target company, job description, and resume. In additional to ensuring the user has entered all required fields, it will verify that the target job title, target company, and target industry are within certain character limits. The job description and resume have character maximums and minimums to try and prevent bad actors. If any of these limits are exceeded or if the user does not yet have an OpenAI API key saved, the function will return an error to the user describing what is wrong.

If all checks are passed, the function will use the users OpenAI API key and a the `get_imp_resp` function from helpers to get the 3 most important responsibilities from the job description. These responsibilities are then formatted into HTML using markdown. This process is repeated to get the tailored resume and differences between the tailored resume and new resume, but using the `get_tailored_resume` and `get_differences` functions from helpers.

A resume name is then generated using the target company and target job title. This name, along with the target job title, target company, tailored resume, and date and time that the resume was generated, are stored in the history database for the user. If there are already 5 documents stored for that particular user, the oldest document is overwritten with the resume that has just been generated.

Finally, the HTML versions for the 3 most important responsibilities, tailored resume, and differences between the two resumes are sent to the JavaScript in the front end to dynamically insert into the web page.

When accessing this route using "GET" the page will load with the required input boxes. If the user has previously entered a resume in the account page, that user's resume will be selected and entered into the resume field.

#### About:
This route simply renders the about.html template that describes what this web application does.

#### Account:
This route allows the user to update: email, password, OpenAI API Key, and resume.

When accessed using "POST", this route will ensure the user entered an email and OpenAI API Key. If the user has previously entered these values, they will autofill into the input boxes. The function then verifies that the passwords match if they were changed and the password is different from the one saved. Next, it ensures the email and/or OpenAI API Key are the same as what is in the database and if not, the email and/or API Key are updated. Finally the resume length is checked if it was entered and if it is within the length requirements, it is saved into he database.

A message is then sent to the JavaScript using `jsonify` to update the user with the errors or successful fields updated in the database.

When accessing this route using "GET" the page will load with the required input boxes. If the user has previously entered an email, OpenAI Key, or resume, those fields will autofill in.

#### API Key:
This route allows the user to update their OpenAI API Key.

When accessed using "POST", this route will ensure that the user entered an API Key. It will pull the user's Open API Key from the SQL database. If no API Key is found in the database, it will validate the user's entered API Key and save it into the database. If there is an API Key already in the database, it will verify that the entered API Key is different before validating and updating the database.

A message is then sent to the JavaScript using `jsonify` to update the user with the errors or successful fields updated in the database.

When accessing this route using "GET" the page will render a template with instructions for how to get an OpenAI API Key and an input box for the API Key. If the user has previously entered an OpenAI API Key the input field will autofill in.

#### History:
This route will obtain all the documents the user has saved in the the database and render them in a template. The documents are displayed in descending order by date.

#### Login:
This route will login the user given the correct login information is given.

When accessed using "POST", the route will check if the user has entered an email and password, then check the database to determine if the email is saved. If a matching email is found in the database, it will check that the password matches the one in the database for the given email and set the session to the user's id number before redirecting them to the index page.

If any errors are found, the user will be redirected to an apology page explaining what went wrong.

When accessing this route using "GET" the page will render a template with the login input boxes.

#### Logout:
This route will logout the user by clearing their session and redirecting them to the login page.

#### Register:
This route allows the user to register using an email and password.

When accessed using "POST", the route will check that the user entered an email, password, and confirmation of password. Next, it checks that the password and confirmation match and that the email is not already contained in the database. Finally, it sets the new session for the user and enters the email and hashed password into the database before redirecting the logged in user to the api_key route.

If any errors are found, the user will be redirected to an apology page explaining what went wrong.

When accessing this route using "GET" the page will render a template with the register input boxes.

#### Tailor Cover Letter
This route allows the user to create a partial or complete cover letter tailored to a job description.

When accessed using "POST", the route will check that the user has entered a previous/current job title, target company, target job title, job description and resume that fall within certain length requirements. Next, it will lookup the user's OpenAI API Key in the database and determine whether the user wanted to generate a full or partial cover letter. If the user wanted a full cover letter, it will call the `get_personalized_tutor_full` function, and else, it will call the `get_personalized_tutor_partial`. 

A cover letter name is then generated using the target company and target job title. This name, along with the target job title, target company, tailored cover letter, and date and time that the cover letter was generated, are stored in the history database for the user. If there are already 5 documents stored for that particular user, the oldest document is overwritten with the resume that has just been generated.

Finally, the tailored cover letter is converted to HTML using the `markdown` function and sent to the JavaScript in the front end to dynamically insert into the web page.

### helper.py:
This is the helper file where all helpful functions for app.py are stored. This file contains the following functions:

#### api_key_validation
This function is used to determine if the user has entered a valid OpenAI API Key.

This function takes the `user_api_key` and returns true if the key is valid and false if not. The function will try a test call to OpenAI's gpt-3.5-turbo-1106 model and if a response is returned, the function will return true, else it will return false.

#### apology
This function is used to deliver a custom apology message to a user.

This function will take a `message` and error `code` and return a rendered template with the code and message to be used to display to the user what has gone wrong. This function will also convert any unknown symbols to known symbols. For the meme generator in apology.html.

#### decrypt_key
This function is used to decrypt the user's encrypted OpenAI API Key when it is retrieved from the database.

The function will take an `encrypted_key` and `fernet_instance` and return a decrypted OpenAI API Key that can be used to access OpenAI's API.

#### encrypt_key
This function is used to encrypt the user's OpenAI API Key when it is retrieved from the user to be updated in the database.

The function will take a `key` and `fernet_instance` and return a encrypted OpenAI API Key to be store in the database.

#### get_fernet_instance
This function will initialize and return a Fernet instance using a secret key from the server side.

The function will open a text file stored outside of the project file directory that stores the secret key for access to the OpenAI API Keys that are stored in the database. Any one wishing to clone this repository will need to generate their own secret key and save it to a file on their local machine. This allows for public sharing of this repository without jeopardizing any user's OpenAI API Key.

#### get_imp_resp
This function will use OpenAI's API to generate the 3 most important job responsibilities from the user's input of industry and job description.

The function will take the an OpenAI `api_key`, `industry`, `jobdescription`, and `temp` that is automatically set to 0.5 for a balanced response. Using this information, the function will enter the required information into the prompts that will be sent to OpenAI's model and will return the model's response in markdown. This function uses the gpt-3.5-turbo-1106 model for speed and low cost with out lose to accuracy.

#### get_differences
This function will use OpenAI's API to generate a table of the differences between the user's resume and the tailored resume from the user's input and previous OpenAI generations.

The function will take the an OpenAI `api_key`, `original_resume`, `tailored_resume`, and `temp` that is automatically set to 1 for a more creative response. Using this information, the function will enter the required information into the prompts that will be sent to OpenAI's model and will return the model's response in markdown for the differences between the original and tailored resume. This function uses the gpt-4-1106-preview model for increased accuracy and reliability in responses. The top_p is set to 0.9 to cut down some of the responses that the model considers to improve speed marginally.

#### get_personalized_tutor_full
This function will use OpenAI's API to generate a complete tailored cover letter from the user's input.

The function will take the an OpenAI `api_key`, `company`, `jobdescription`, `jobtitle`, `prevjob`, `resume`, and `temp` that is automatically set to 1 for a more creative response. Using this information, the function will enter the required information into the prompts that will be sent to OpenAI's model and will return the model's response in markdown for a cover letter tailored to a specific job description. The entered information is used to improve the prompt for the model to improve the response for the user. This function uses the gpt-4-1106-preview model for increased accuracy and reliability in responses. The top_p is set to 0.75 to cut down some of the responses that the model considers to improve speed marginally.

#### get_personalized_tutor_partial
This function will use OpenAI's API to generate a few key sentences to help the user create a tailored cover letter to the job description.

The function will take the an OpenAI `api_key`, `company`, `jobdescription`, `jobtitle`, `prevjob`, `resume`, and `temp` that is automatically set to 1 for a more creative response. Using this information, the function will enter the required information into the prompts that will be sent to OpenAI's model and will return the model's response in markdown for a few key sentences for a cover letter tailored to a specific job description. The entered information is used to improve the prompt for the model to improve the response for the user. This function uses the gpt-4-1106-preview model for increased accuracy and reliability in responses. The top_p is set to 0.75 to cut down some of the responses that the model considers to improve speed marginally.

#### get_tailored_resume
This function will use OpenAI's API to generate a tailored resume based on the user's input information and previous OpenAI generations.

The function will take the an OpenAI `api_key`, `company`, `imp_resp`, `industry`, `jobdescription`, `jobtitle`, `resume`, and `temp` that is automatically set to 1 for a more creative response. Using this information, the function will enter the required information into the prompts that will be sent to OpenAI's model and will return the model's response in markdown for a resume tailored to a specific job description. The entered information is used to improve the prompt for the model to improve the response for the user. This function uses the gpt-4-1106-preview model for increased accuracy and reliability in responses. The top_p is set to 0.8 to cut down some of the responses that the model considers to improve speed marginally.

#### login_required
This function will decorate any routes that require login. If the user is not logged in, they will be redirected to the login route.

#### usd
This function will format a value into United State's dollars.

### resi.db:
This is the main SQL database that stores the user's email, password, OpenAI API Key, resume, and any generated documents. The database contains two tables: users and history. All information that is entered into the database is sanitized using the `?` operator to prevent against injection attacks.

#### users:
The users table stores the following information:
- id: auto incrementing integer to keep track of the user (Primary Key)
- email: unique index to store the user's identifying email as text
- hash: text input to store the hash of the user's password
- api_key: text input to store the user's encrypted OpenAI API Key
- resume: text input to store the user's original resume

#### history:
The history table stores the following information:
- id: auto incrementing integer to keep track of the document created (Primary Key)
- user_id: integer to keep track of which user created a particular document (Foreign Key references users(id))
- document_name: text input to store the name of the document created
- company: text input to store the name of the target company the document was created for
- job_title: text input to store the target job title the document was created for
- document: text input to store the document that the user created
- datetime: text input to store when the document was created

> Note: Only the 5 most recent documents are stored to prevent the database from being overcrowded with too many documents.

## Design Decisions
### Models:
This web application uses OpenAI's gpt-3.5-turbo-1106 and gpt-4-1106-preview models. The GPT-3.5 Turbo model is used to generate the 3 most important responsibilities from the job description. This model showed consistent and accurate results for generating the 3 most important responsibilities similar to GPT-4 Turbo, but it was able to do so quicker and cheaper than GPT-4, so it was chosen for the initial task of finding the three most important responsibilities in the job description.

The GPT-4-Turbo model was chosen to generate the tailored resume due to its superior performance when it came to accuracy and consistency. GPT-3.5-Turbo was faster and cheaper, but it came at the cost of providing inaccurate tailored resumes and especially when it came to comparing between the tailored and original resumes. The decreased speed and increased cost were deemed worthwhile for the improved accuracy and consistency. GPT-4-Turbo appears to do much better then GPT-3.5-Turbo with the additional content that was required for this application.

Original versions of this application used gpt-3.5-turbo which resulted in inaccurate results and it lacked the context window required to handle the resumes and job descriptions. The gpt-4 model was also tested, however it was too slow and also lacked the context window required to be considered functional for this application.

A consideration was made to fine tune a model to improve the results, but this would have been costly and similar results could be achieved using prompt engineering. Additionally, the model would have lost some of the customization that can be achieved with prompting. 

There is room for additional improvements on the models with improved prompting or settings that could not be covered at this time.

### Prompts:
The prompts used to generate the resumes were derived from the following YouTube video by Jeff Su: [Land a Job using ChatGPT: The Definitive Guide!](https://www.youtube.com/watch?v=pmnY5V16GSE&t=317s). The prompts were adjusted to fit the adjustable needs of this project.

The prompts have been designed to replicate how a sample conversation would go with ChatGPT, while having room to be customized to the user's particular situation.

### Scraped Features:
This section contains any features that have been cut for the time being and descriptions of why the feature was scraped.

#### Price Estimator:
This feature would have given the user a price estimate on how much it would cost them in their OpenAI API account to generate a tailored resume or cover letter.

This feature was scrapped due to its inaccuracy and lack of usefulness after a few uses. Once a user has generated a few resumes, the price remains pretty consistent, making this a low to no value feature. Additionally, the price to generate even the largest resumes is around $0.20, so the user is not at risk of spending too much money too quickly.

### Security:
Security was a major concern on this project. The goal was for the project to be secure while also openly accessible for open source.

This was accomplished using hashes for the user's passwords so any database leaks would not result in passwords being leaked and using a secret key encryption to encrypt user's API Keys so that they cannot be decrypted by anyone other than the person who has set up the project.

All inputs into the databases are also sanitized to protect against injection attacks.

Improvements could have been made to make the sections that are being given access to the AI safer. Character limits were implemented to deter user's from accidentally entering information and prevent them from adding too much information and overloading the context window of the model

## Contributing
Thank you for your interest in contributing to this project! Contributions are welcome from anyone who wishes to improve or expand the project.

Here are some ways you can contribute:

- **Reporting bugs:** If you find a bug, please open an issue detailing the problem, how to reproduce it, and any other relevant information.
- **Suggesting enhancements:** Have an idea for a new feature or think something could be improved? Open an issue to suggest your enhancement.
- **Submitting pull requests:** Feel free to fork the repository and submit pull requests with your changes or additions. Whether it's fixing a typo, addressing an issue, or adding a new feature, all contributions are appreciated.

### How to Contribute
1. Fork the repository on GitHub.
2. Clone your fork to your local machine (`git clone YOUR_FORK`).
3. Create your Branch for changes (`git checkout -b YOUR_CHANGES`).
4. Make your changes and commit them with clear, descriptive messages (`git commit -m 'Detailed description of your amazing changes'`).
5. Push to the Branch (`git push origin YOUR_CHANGES`)
6. Submit a pull request against the main branch of this repository.
7. Wait for feedback or approval from the project maintainers.

## Credits
This project was developed by Jadon Vanyo. Special thanks to the following resources for guidance and inspiration:

- This project uses the same base structure as Harvard's C$50 Finance project. See [C$50 Finance](https://cs50.harvard.edu/college/2023/fall/psets/9/finance/) for full details.
- Additional credit to CS50's documentation for outlining how to set up a flask application in Heroku. See [CS50 Docs](https://cs50.readthedocs.io/heroku/) for full details.
- The prompts used to generate the resumes were derived from the following YouTube video by Jeff Su: [Land a Job using ChatGPT: The Definitive Guide!](https://www.youtube.com/watch?v=pmnY5V16GSE&t=317s). The prompts were adjusted to fit the adjustable needs of this project.

## License
Distributed under the MIT License. See LICENSE for more information.