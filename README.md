# FastAPI Book Management API

## Overview

This project is a RESTful API built with FastAPI for managing a book collection. It provides comprehensive CRUD (Create, Read, Update, Delete) operations for books with proper error handling, input validation, and documentation. The project includes a Continuous Integration (CI) and Continuous Deployment (CD) pipeline and is served using Nginx as a reverse proxy.

## Features

- 📚 Book management (CRUD operations)
- ✅ Input validation using Pydantic models
- 🔍 Enum-based genre classification
- 🧪 Complete test coverage
- 📝 API documentation (auto-generated by FastAPI)
- 🔒 CORS middleware enabled
- 🚀 CI pipeline for automated testing
- 🛠️ CD pipeline for automated deployment
- 🔧 Served using Nginx as a reverse proxy

## Project Structure

```
fastapi-book-project/
fastapi-book-project/
├── api/
│   ├── db/
│   │   ├── __init__.py
│   │   └── schemas.py      # Data models and in-memory database
│   ├── routes/
│   │   ├── __init__.py
│   │   └── books.py        # Book route handlers
│   └── router.py           # API router configuration
├── core/
│   ├── __init__.py
│   └── config.py           # Application settings
├── tests/
│   ├── __init__.py
│   └── test_books.py       # API endpoint tests
├── .github/
│   └── workflows/
│       ├── ci.yml          # Continuous Integration workflow
│       └── cd.yml          # Continuous Deployment workflow
├── nginx/
│   └── nginx.conf          # Nginx configuration file
├── main.py                 # Application entry point
├── requirements.txt        # Project dependencies
└── README.md
```

## Technologies Used

- Python 3.12
- FastAPI
- Pydantic
- pytest
- uvicorn
- GitHub Actions (for CI/CD)
- Nginx

## Installation

1. Clone the repository:

```bash
git clone https://github.com/LivingHopeDev/fastapi-book-project.git
cd fastapi-book-project
```

2. Create a virtual environment:

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

## Running the Application

1. Start the server:

```bash
uvicorn main:app --reload
```

2. Access the API documentation:

- Swagger UI: http://localhost:8000/docs
- ReDoc: http://localhost:8000/redoc

live url

- http://ec2-18-119-117-227.us-east-2.compute.amazonaws.com/docs

## API Endpoints

### Books

- `GET /api/v1/books/` - Get all books
- `GET /api/v1/books/{book_id}` - Get a specific book
- `POST /api/v1/books/` - Create a new book
- `PUT /api/v1/books/{book_id}` - Update a book
- `DELETE /api/v1/books/{book_id}` - Delete a book

### Health Check

- `GET /healthcheck` - Check API status

## Book Schema

```json
{
  "id": 1,
  "title": "Book Title",
  "author": "Author Name",
  "publication_year": 2024,
  "genre": "Fantasy"
}
```

Available genres:

- Science Fiction
- Fantasy
- Horror
- Mystery
- Romance
- Thriller

## Continuous Integration (CI) Setup

### CI Workflow

- File: .github/workflows/ci.yml

- Trigger: Runs on pull requests to the main branch.

- Actions:

- Set up Python environment.

- Install dependencies.

- Run pytest to execute all tests.

- Fail the workflow if any tests fail.

## Running Tests

```bash
pytest
```

## Continuous Deployment (CD) Setup

### CD Workflow

- File: .github/workflows/cd.yml

- Trigger: Runs on merging a pull request to the main branch.

- Actions:

- Deploy the FastAPI application with the latest changes.

- Restart the server to apply updates.

### Nginx Configuration

#### Setting Up Nginx as a Reverse Proxy

- Install Nginx (if not installed):

```
sudo apt update
sudo apt install nginx
```

- Configure Nginx:

Create or update the nginx/nginx.conf file with the following:

```
server {
    listen 80;

    server_name your_domain_or_ip;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

- Enable the Configuration and Restart Nginx:

```
sudo ln -s /etc/nginx/sites-available/nginx.conf /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

## Error Handling

The API includes proper error handling for:

- Non-existent books
- Invalid book IDs
- Invalid genre types
- Malformed requests

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For support, please open an issue in the GitHub repository.
