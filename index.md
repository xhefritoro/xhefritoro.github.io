
# 1. Professional Self-Assessment

---

During my years at Souther New Hampshire University I was able to experience many new concepts which fortunately I had the chance to understand their importance, and often finding myself implementing them at my work place. The area that streaked me the most was in the realms of data science. 

Nowadays, there are plenty of systems that produce data, which can be used to better serve the community and with the skills I have learned on this program, I was able to better understand the data and mine it to solve problems.

Another interesting concept I learned throughout this program, was from CS310 course where I learned about testing the code to ensure that I deliver a high-quality work with better code and fewer bugs. This approach has led me to make sure I provide coverage for my code and eliminate any unwanted behavior on code changes/releases.

All of the tools learned in this program guided me throughout my career and continue to support my decision-making when it comes to my professional achievements. Based on the knowledge gained from this program, now I’m able to look for the right solution on my daily tasks. Thanks to the knowledge foundation built from Computer Science Program at Southern New Hampshire University, it has also facilitated me in solving complex projects.

# 2. Code Review

---

[![Watch the video](https://i.imgur.com/XhaHoBu.png)](https://shelter.xhefri.net/assets/video/code_review.mov)]

# 3. Software Designer and Engineering

---

## 1. Overview

![Overview_SDE](https://github.com/xhefritoro/xhefritoro.github.io/blob/master/assets/Untitled.png)

Artifact chosen for Software Design and Engineering is called Animal Shelter which is an inventory of rescued animals. It came from CS-340 course, and I’m using this artifact for Software Engineering/Design category. My plan to enhance this artifact is to run it through Lambda and API gateway as a Rest API and move the front end from python to TypeScript using Angular Framework. By doing so, I will be able to integrate the API with OIDC provider authentication such as Cognito, host the website as a static through CloudFront and S3 Buckets, and enable the ability to orchestrate cloud services using infrastructure as code by utilizing serverless application model (SAM) and satisfy course outcome 01 (Employ strategies for building collaborative environments that enable diverse audiences to support organizational decision making in the field of computer science) which enables a collaborative environment to develop, as well as course outcome 05 (Develop a security mindset that anticipates adversarial exploits in software architecture and designs to expose potential vulnerabilities, mitigate design flaws, and ensure privacy and enhanced security of data and resources) by integrating with OIDC provider and enable a secure authorization to users with JWT tokens.

## 2. Enhancement

During this category enhancements I have built the project blueprint, where I have created the required resources using infrastructure as code “Cloudformation”. The project is structured as follows:

- Front End Structure using Angular `front_end_site`
    - Angular `front_end_site/angular`
    This directory contains all the front end code
        - Source Directory for the development `src`
        - Root directory all the angular configurations `/`
    - CloudFormation `front_end_site/cloudformation`
    This directory contains the infrastructure as code for the front end portion of the project
- Backend Structure using SAM `/`
    - Source Directory for the code development  `src`
    - Root directory all the SAM configurations `/`

Within this milestone, I have created the Sign In/ SignUp and authentication flow using Cognito OIDC provider, the files developed within the `front_end_site/angular`  and SAM template under `template.yaml` as follows:

- File `front_end_site/angular/src/app/cognito.service.ts` was created to facilitate the authentication helper functions and authentication APIs to Cognito using `aws-amplify` package to simplify methods.
    - Functions
        - public signUp() →  function to perform new user signup.
        - public confirmSignUp() → Checks against the temporary code sent on users email.
        - public signIn() → Performs user sign in retrieving and storing the authentication token.
        - public signOut() → Performs user sign out by clearing all the Authorization tokens
        - public isAuthentication() → Checks the authentication against Cognito to make sure that token are not expired
        - public getUser() → Retrieve user attributes.
        - public getUserCreds() → Retrieve user credentials (Authorization JWT Token, Refresh JWT Token)
        - public updateUser() → Update user attributes.
    - Interfaces
        - IUser This holds the user attributes structure.
- Pages created under `app` directory `front_end_site/angular/src/app`
    - home → Implements landing page and loads the database records
    - profile → Displays user attributes from Cognito
    - sign-in →  Used to sign in users
    - sign-up → Used to register new user

## 3. Outcomes

### CS-499-01

By utilizing serverless application model and breaking the application into two parts front-end and backend, and making sure to comment all the code across the board, I was able to employ strategies for building collaborative environments that enable diverse audiences to support organizational decision-making in the field of computer science.

### CS-499-05

Using OIDC providers and JWT token I ensured to have temporary access for the users as well as a way to reduce the access to the data based on identity access manager by AWS, and the roles that lambda functions attach to gain access to the DynamoDB tables and invoked only through API Gateway. This practice was placed to develop a security mindset that anticipates adversarial exploits in software architecture and designs to expose potential vulnerabilities, mitigate design flaws, and ensure privacy and enhanced security of data and resources.

# 4. Algorithms and Data Structure

---

## 1. Overview

![Overviw_AD](https://github.com/xhefritoro/xhefritoro.github.io/blob/master/assets/Untitled%201.png)

Artifact chosen for Algorithms and Data Structure is called Animal Shelter, which is an inventory of rescued animals. It came from CS-340. I will be using this artifact for Algorithms and Data Structures category. My plan to enhance this artifact is to move from mongodb connector to SQL Alchemy package. By doing so, I will be able to use object relational mapping to simplify the interaction the database to execute (C) create (R) read (U) update (D) delete orations. This will satisfy course outcome 04 (Demonstrate an ability to use well-founded and innovative techniques, skills, and tools in computing practices for the purpose of implementing computer solutions that deliver value and accomplish industry-specific goals), by using well-founded and innovative techniques as well as outcome 03 (Design and evaluate computing solutions that solve a given problem using algorithmic principles and computer science practices and standards appropriate to its solution, while managing the trade-offs involved in design choices) of this course by constraining the application to be within the algorithmic principles and computer science practices and standards.

## 2. Enhancements

Classes created for ORM Objects

- `PetsDescription`
- `PetsOutcome`
- `PetsDates`
- `PetsLocation`
- `PetsInventory`

ORM objects with these objects I have represented Data Structure for the project. Each object has 3 functions within itself listed below:

- `__repr__ `; Used to generate string representation of the object
- `res_serialize`; Used to convert the ORM object into JSON format to be returned
- `from_json`: This is a class method to extract data from json and map them into ORM object.

All the development above can be found under src/models.py file, which is imported into the src/functions.py file.

On the functions.py file, I have implemented the Algorithms part of the project where all the logic between merging and grabbing the data is implemented. Currently there are:

- `id_generator`; This function generates a random ID for the animals upon creation.
- `get_animals`; This function gets all the inventory of the animals from the inventory table.
- `get_animal`; This function checks if the animal exists with animal_id and return its properties.
- `post_animals`; This function creates a new animal.
- `update_animals` This function checks if the animal exists with animal_id and updates its properties with the changes.
- `delete_animals` This function checks if the animal exists with animal_id and deletes it.

All of the above functions are being imported and used in  src/ app.py where I have set the routes and the router configurations. The helper package I have used to do the routes in lambda function comes from AWS Lambda Power tools, which gives me all the integration needed to do Tracing/Logging with API gateway for better visibility while debugging. The routes created are as follows:

- ` POST - /v1/pet`; This path calls the function ` post_animals ` and passes the json body received form the request.
- `GET – /v1/pet`; This path calls the function `get_anmials` and does not take and parameters.
- `GET – /v1/pet/<animal-id>` This path calls the function `get_anmial` and takes the animal_id as path parameter.
- `PUT – /v1/pet/<animal-id>` This path calls the function `update_anmial` and takes the animal_id as path parameter as well as the json body coming with the request
- `DELETE – /v1/pet/<animal-id>` This path calls the function `delete_anmial` and takes the animal_id as a path parameter.

## 3. Outcomes

### CS-499-02

By breaking down the different part of the backend into ORM Classes, Functions, and Routes I was able to design, develop, and deliver professional-quality oral, written, and visual communications that are coherent, technically sound, and appropriately adapted to specific audiences and contexts.

### CS-499-04

Utilizing the standard of REST API, I was able to make the code intuitive while going through it and demonstrate an ability to use well-founded and innovative techniques, skills,
and tools in computing practices for the purpose of implementing computer solutions that
deliver value and accomplish industry-specific goals.

# 5. Databases

---

## 1. Overview

![Overview_D](https://github.com/xhefritoro/xhefritoro.github.io/blob/master/assets/Untitled%202.png)

Artifact chosen for Databases is called Animal Shelter, which is an inventory of rescued animals. It came from CS-340 course, I will be using this artifact for the databases category. My plan is to move away from mongodb and use DynamoDB tables in AWS to make the application fully serverless. This approach will satisfy outcome 02 (Design, develop, and deliver professional-quality oral, written, and visual communications that are coherent, technically sound, and appropriately adapted to specific audiences and contexts) of the course, by explaining how this conversion will be done and satisfy the delivery of oral, written, and visual communications of the changes.

## 2. Enhancements

Within this milestone, I have created the Dashboard workflow by integrating the front-end with the backend, and by developing the code within the `front_end_site/angular`  directory as follows:

- File `front_end_site/angular/src/app/api.service.ts` was created to facilitate the functions to call the backend with the appropriate paths and methods. All of the API calls
- include the Authorization header, which is retrieved from the browser’s local storage.
    - Functions:
    - 
        - public getAnimal() →   This function makes a `GET` method api call to `v1/pet/`
        - public getAnimals() →  This function makes a `GET` method api call to `v1/pet/{animal_id}`.
        - public postAnimal() → This function makes a `POST` method api call to `v1/pet/`
        - public deleteAnimal() → This function makes a `DELETE` method api call to `v1/pet/{animal_id}`
        - private log() → Centralizes the log reporting in case of an error currently outputting the errors on the console log.
        - public handleError() → Handles errors in case the API responds with a status code other than within the range of 200-205.
    - Interfaces:
        - AnimalsInventory → holds only the initial data loaded in the table
- Pages created under `app` directory `front_end_site/angular/src/`
    - animal-profile → Invoked on view/edit, and create. Based on the action, it shows a blank modal in new animal action or pre-filled on view/edit action.
    - home → Loads Animal Inventory on the landing page.
    

## 3. Outcomes

### CS-499-03

Structuring the tables was one of the items where I spent most of the time thinking about the structure and ensuring that the approach taken would be optimized, with no overload data required to be retrieved. This way, I was able to evaluate computing solutions that solve a given problem using algorithmic principles and computer science practices and standards appropriate to its solution, while managing the trade-offs involved in design choices. 

# [Animal Shelter-LINK](https://shelter.xhefri.net/)
