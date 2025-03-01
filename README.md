# REST-API-Server-Seekora
REST API Server project
REST API Server Documentation
Overview
This REST API server allows clients to perform the following operations:

Save User via a POST endpoint.

Retrieve All Users via a GET endpoint.

Filter Users based on a search string via a GET endpoint.

Convert a given string into a vector representation via a POST endpoint.

Technologies Used
Backend Framework: Django REST Framework (DRF)

Database: PostgreSQL (can be replaced with SQLite or other databases)

Vectorization: TF-IDF with PCA for dimensionality reduction (Scikit-learn)

Testing: Postman / cURL

Installation & Setup
Prerequisites
Python 3.8+

Virtual Environment (recommended)

PostgreSQL / SQLite

Installation Steps
Clone the repository:

git clone <repository-url>
cd rest_api_project
Create a virtual environment:

python -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate
Install dependencies:

pip install -r requirements.txt
Apply migrations:

python manage.py migrate
Create a superuser (optional, for admin access):

python manage.py createsuperuser
Start the development server:

python manage.py runserver
API Endpoints
1. Add User
Endpoint: /api/user/

Method: POST

Request Body (JSON):

{
  "name": "John Doe",
  "email": "john@example.com"
}
Response (Success):

{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com"
}
2. Get All Users
Endpoint: /api/users/

Method: GET

Response:

[
  {
    "id": 1,
    "name": "John Doe",
    "email": "john@example.com"
  }
]
3. Filter Users
Endpoint: /api/filter/

Method: GET

Query Parameter: ?query=<search_string>

Example: /api/filter/?query=user1

Response:

[
  {
    "id": 2,
    "name": "user1 Doe",
    "email": "user1@example.com"
  }
]
4. String Vectorization
Endpoint: /api/vectorize/

Method: POST


Request Body (JSON):
http://127.0.0.1:8000/api/vectorize/
add key on body- text key 
![image](https://github.com/user-attachments/assets/0d05916a-671d-463d-83a2-ded4be5e76c6)


{
  "text": "Python is a great programming language"
}
Response:

{
  "vector": [0.312, 0.215, 0.576, 0.109]
}
Testing Instructions
Using Postman:
Open Postman and create a new request.

Select the appropriate HTTP Method (GET/POST).

Enter the API URL (e.g., http://127.0.0.1:8000/api/user/).

For POST requests, set Body → raw → JSON and enter the request payload.

Click Send and verify the response.

Using cURL:
Add User:
curl -X POST http://127.0.0.1:8000/api/user/ -H "Content-Type: application/json" -d '{"name": "John Doe", "email": "john@example.com"}'
Get Users:
curl -X GET http://127.0.0.1:8000/api/users/
Filter Users:
curl -X GET "http://127.0.0.1:8000/api/filter/?query=john"
Vectorize String:
curl -X POST http://127.0.0.1:8000/api/vectorize/ -H "Content-Type: application/json" -d '{"text": "Python is great"}'
Error Handling
Invalid JSON format: 400 Bad Request

Missing required fields: 400 Bad Request

Resource not found: 404 Not Found

Server error: 500 Internal Server Error

Additional Notes
The project uses TF-IDF for vectorization and PCA for dimensionality reduction.

You can modify the number of PCA components in views.py.

To deploy, use gunicorn with Docker or AWS/GCP for production setup.

For further assistance, feel free to contact the developer. 🚀

