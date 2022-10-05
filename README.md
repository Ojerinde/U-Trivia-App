# TRIVIA APP

## Introduction

Trivia app is a web-based bookshelf where user can play trivia games. They can add as well have quiz. It is an app that is built around a RESTful API which performs all CRUD operations. As part of Udacity Fullstack Nanodegree, it is a project I built using all the concepts and skills I learnt throughout the lesson.

![image](https://user-images.githubusercontent.com/104495751/194056057-7abd931d-01c9-4d15-8364-64bf2def0bcb.png)


The App does the following by the help of the built API,
* Display questions
* Delete question
* Search for questions
* Play a quiz game

## Code Style
All backend code follows [PEP8 style guidelines](https://www.python.org/dev/peps/pep-0008/). 

## Main Files: Project Structure

```
├── README.md
├── CODEOWNERS
├── LICENSE.txt
├── .gitignore
├── frontend
│   ├── public
│   ├── src
│   ├── package,json
└── backend
    ├── flaskr
    │   ├──__init__.py 
    ├── models.py # Houses all the models
    ├── requirements.txt # The dependencies we need to install with `pip3 install -r requirements.txt`
    ├── test_flaskr.py
    └── trivia.psql
```

**Overall**:

- Models are located in `models.py` file
- Controllers are located in `__init__.py` file


## Getting Started

### Pre-requisites and Local Development 
The prerequites tools for local development are:

 - Python
 - Pip
 - Node
 - virtualenv: To create an isolated Python environment
 - Postgres
 
### Set up the Database

With Postgres running, create a `trivia` database by running

```
createbd trivia
```

Populate the database using the `trivia.psql` file in the backend directory by running

```
psql trivia < trivia.psql
```

### Backend
It is a good practice to keep your app dependencies isolated by working a virtual environment.

* To Initialize a virtual enviroment, run

```
python -m virtualenv env
```

* To Activate the environment run

```
source env/bin/activate
```

**Note** - In Windows, the `env` does not have a `bin` directory. Therefore, you'd use the analogous command shown below:

```
source env/Scripts/activate
```

To run the backend application, you need to install the required packages by doing the following,

* navigate into the backend folder
* run 
  ```pip install -r requirements.txt```

After succesfull installation of the packages, you can get the app running by running the following commands

```
export FLASK_APP=myapp
export FLASK_DEBUG=True # enables debug mode
flask run

```
**Note**: For window, change export to set i.e. set FLASK_APP=myapp

The application is run on `http://127.0.0.1:5000/` by default and is a proxy in the frontend configuration. 

### Frontend
The app is built with React so there is need to install the frontend dependencies using Node.js and NPM

You can confirm if Node.js and NPM is installed successfully using the codes below

```
node -v
npm -v
```

From the frontend folder, run the following commands to start the client: 
```
npm install # run this once to install dependencies
npm start 
```

By default, the frontend will run on `localhost:3000`. 

### Tests
In order to test the API endpoints navigate to the backend folder and run the following commands: 

```
dropdb trivia_test # Executed only if there is an existing database with the same name
createdb trivia_test
psql trivia_test < trivia.psql # to populate the created databse
python test_flaskr.py
```
**Note**: All tests are written in the test_flaskr.py file.

## API Reference

### Getting Started

This application is not deployed and can only be run locally. The backend application is hosted at the default port (Base URL) which is set as a proxy in the frontend application.

* **Base URL**: http://127.0.0.1:5000/
* **Authentication**: This application doesn't require authentication or API keys.

### Error Handling

* **Errors format**: All errors are returned as a JSON object as shown below

```
{
    'success': False,
    'error': 404,
    'message': "Resources not found"
}
```

* **Error Codes and Messages**: The API will return one out of four(4) error type whenever the request fail:
    * 400: Bad request
    * 404: Resources not found
    * 405: Methods not allowed
    * 422: Request unprocessable

* **Error Mesaages possible solution**:
    * Bad Request: Check the format of your request. Make sure your format satisfies what the endpoint and the endpoint method requires.
    * Resources not found: Search for resources that exist in the database or server
    * Methods not allowed: Check if the method is allowed for the particular endpoint
    * Request unprocessable: Try again! Server error. 

### Endpoints

#### Method: GET
#### Endpoint: /categories
* General:
    * This endpoint fetches a dictionary of categories
    * Fetched results is an object with a single key `categories` whose value is a list of all category.
    * Each element of the list is an object that has `id` and `type` keys.
    * Request argument: None 
* Sample:
    * Without argument: `curl http://127.0.0.1:5000/categories`
* Response: Json
```
{
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  }
}
```

#### Method: GET
#### Endpoint: /questions?page=${integer}'
* General:
    * This endpoint fetches a dictionary of categories and questions
    * Fetched results is an object with `categories`, `questions`,  `current_category` and `total_questions` as keys.
    * The questions's value which is a list are paginated in groups of 10
    * Request argument can be included to choose page number of the questions. By default, page number is 1.
* Sample:
    * Without argument: `curl http://127.0.0.1:5000/questions`
    * With argument: `curl http://127.0.0.1:5000/questions?page=2` 
* Response: json
```
{
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  },
  "current_category": "Science",
  "questions": [
    {
      "answer": "Apollo 13",
      "category": 5,
      "difficulty": 4,
      "id": 2,
      "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
    },
    {
      "answer": "Maya Angelou",
      "category": 4,
      "difficulty": 2,
      "id": 5,
      "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
    },
    {
      "answer": "Edward Scissorhands",
      "category": 5,
      "difficulty": 3,
      "id": 6,
      "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
    },
    {
      "answer": "Muhammad Ali",
      "category": 4,
      "difficulty": 1,
      "id": 9,
      "question": "What boxer's original name is Cassius Clay?"
    },
    {
      "answer": "Brazil",
      "category": 6,
      "difficulty": 3,
      "id": 10,
      "question": "Which is the only team to play in every soccer World Cup tournament?"
    },
    {
      "answer": "Uruguay",
      "category": 6,
      "difficulty": 4,
      "id": 11,
      "question": "Which country won the first ever soccer World Cup in 1930?"
    },
    {
      "answer": "George Washington Carver",
      "category": 4,
      "difficulty": 2,
      "id": 12,
      "question": "Who invented Peanut Butter?"
    },
    {
      "answer": "Lake Victoria",
      "category": 3,
      "difficulty": 2,
      "id": 13,
      "question": "What is the largest lake in Africa?"
    },
    {
      "answer": "Agra",
      "category": 3,
      "difficulty": 2,
      "id": 15,
      "question": "The Taj Mahal is located in which Indian city?"
    },
    {
      "answer": "Escher",
      "category": 2,
      "difficulty": 1,
      "id": 16,
      "question": "Which Dutch graphic artist\u2013initials M C was a creator of optical illusions?"
    }
  ],
  "total_questions": 17
}
```

#### Method: DELETE
#### Endpoint: /questions/{question_id}
* General:
    * This endpoint deletes a question of the given question_id if it exists
    * Returned results is an object with `categories`, `questions`,  `current_category` and `total_questions` as keys.
    * The questions's value which is a list are paginated in groups of 10
    * Request argument can be included to choose page number of the questions. By default, page number is 1.
* Sample:
    * Without argument: `curl -X DELETE http://127.0.0.1:5000/questions/1`
    * With argument: `curl -X DELETE http://127.0.0.1:5000/questions/1?page=2` 
    * Response: json
```
{
   'success': True
}
```

#### Method: POST
#### Endpoint: /questions
##### Searching a question:
* General:
    * This endpoint use the submitted search term search for questions.
    * It returns all questions for whom the search term is a substring of the question. The search is case insensitive.
* Sample:
    * Without argument: `curl -X POST http://127.0.0.1:5000/questions -H "Content-Type: application/json" -d '{"searchTerm": "title"}'`
    * With argument: `curl -X POST http://127.0.0.1:5000/questions?page=2 -H "Content-Type: application/json" -d '{"searchTerm": "title"}'` 
* Request Body: json
```
{
  "searchTerm": "this is the term the user is looking for"
}
```

* Response Body: json
```
{
  "current_category": "Science",
  "questions": [
    {
      "answer": "The Liver",
      "category": 1,
      "difficulty": 4,
      "id": 20,
      "question": "What is the heaviest organ in the human body?"
    },
    {
      "answer": "Alexander Fleming",
      "category": 1,
      "difficulty": 3,
      "id": 21,
      "question": "Who discovered penicillin?"
    },
    {
      "answer": "Blood",
      "category": 1,
      "difficulty": 4,
      "id": 22,
      "question": "Hematology is a branch of medicine involving the study of what?"
    }
  ],
  "total_questions": 3
}
```      

#### Method: POST
#### Endpoint: /questions
##### Creating a question:
* General:
    * This endpoint use the submitted question, answer, difficulty, and category to create a new question
    * Returned results is an object with `questions`,  `current_category` and `total_questions` as keys.
    * The questions's value which is a list are paginated in groups of 10
    * Request argument can be included to choose page number of the questions. By default, page number is 1.
* Sample:
    * Without argument: `curl -X POST http://127.0.0.1:5000/questions -H "Content-Type: application/json" -d '{"question":"What is the fact of knowing something?", "answer":"Science", "difficulty":"3", "category":"1"}'`
    * With argument: `curl -X POST http://127.0.0.1:5000/questions?page=2 -H "Content-Type: application/json" -d '{"question":"What is the fact of knowing something?", "answer":"Science", "difficulty":"3", "category":"1"}'`
* Request Body:json
```
{
  "question": "Heres a new question string",
  "answer": "Heres a new answer string",
  "difficulty": 1,
  "category": 3
}
```
* Response Body: json
```
{
  'success': True
}
```

#### Method: GET
#### Endpoint: /categories/{category_id}/questions
* General:
    * This endpoint takes in a category id
    * It returns all questions of the given category id
    * Returned results is an object with `questions`,  `current_category` and `total_questions` as keys.
    * The questions's value which is a list are paginated in groups of 10
    * Request argument can be included to choose page number of the questions. By default, page number is 1.
* Sample:
    * Without argument: `curl http://127.0.0.1:5000/categories/1/questions`
    * With argument: ``curl http://127.0.0.1:5000/categories/1/questions?page=2`
* Response Body: json
```
{
  "current_category": "Science",
  "questions": [
    {
      "answer": "The Liver",
      "category": 1,
      "difficulty": 4,
      "id": 20,
      "question": "What is the heaviest organ in the human body?"
    },
    {
      "answer": "Alexander Fleming",
      "category": 1,
      "difficulty": 3,
      "id": 21,
      "question": "Who discovered penicillin?"
    },
    {
      "answer": "Blood",
      "category": 1,
      "difficulty": 4,
      "id": 22,
      "question": "Hematology is a branch of medicine involving the study of what?"
    }
  ],
  "total_questions": 3
}
```

#### Method: POST
#### Endpoint: /quizzes
* General:
    * This endpoint use the submitted `previous_questions` and `category` to return a question different from the previous question(s).
    * Returned results is an object with `question` key.
    * The values of `question` are `id`, `question` `answer`, `difficulty`, and `category`
    * No request argument needed.
* Sample:
    * Without argument: `curl -X POST http://127.0.0.1:5000/quizzes -H "Content-Type: application/json" -d '{'previous_questions': [],
                     'quiz_category': {'type': 'Science', 'id': '1'}}'`
* Request Body:json
```
{
  'previous_questions': [],
  'quiz_category': {'type': 'Science', 'id': '1'}
}
```
* Response Body: json
```
{
  'question': {
    'id': question.id,
    'question': question.question,
    'difficulty': question.difficulty,
    'category': question.category,
    'answer': question .answer,
  }
}
```

## Deployment
The app is not deployed

## Author
Joel Ojerinde

## Acknowledgements 
My exceptional teacher, Coach Caryn
