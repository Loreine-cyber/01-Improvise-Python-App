# Create a Pydantic model for the incoming POST request that accepts a field called "text" of type string.
from pydantic import BaseModel

class TextRequest(BaseModel):
    text: str  # Text field for input
    from fastapi import FastAPI
import hashlib

app = FastAPI()

# Assuming the `generate()` function looks like this:
def generate(text: str) -> str:
    # Create a checksum of the text using SHA256
    return hashlib.sha256(text.encode()).hexdigest()

# Create the new endpoint with POST method
@app.post("/generate-checksum")
async def generate_checksum(request: TextRequest):
    """
    This endpoint accepts a POST request with a JSON body containing a field 'text'.
    It returns the checksum (SHA256) of the text.
    """
    checksum = generate(request.text)
    return {"checksum": checksum}

    @app.get("/welcome")
async def welcome():
    """
    Welcome message with the participant's name.
    Replace 'Your Name' with your actual name.
    """
    return {"message": "Welcome to the FastAPI project! This is Your Name's API."}

    # FastAPI app instance
app = FastAPI()

# Endpoint to generate checksum of the provided text
@app.post("/generate-checksum")
async def generate_checksum(request: TextRequest):
    """
    Endpoint to accept text in JSON format and return its checksum (SHA256).
    
    Args:
        request (TextRequest): The request body containing 'text' as a string.
    
    Returns:
        dict: A dictionary with the checksum of the provided text.
    """
    checksum = generate(request.text)
    return {"checksum": checksum}
    from fastapi.testclient import TestClient
from main import app  # Assuming 'app' is the FastAPI instance

client = TestClient(app)

def test_generate_checksum():
    response = client.post("/generate-checksum", json={"text": "hello world"})
    assert response.status_code == 200
    assert "checksum" in response.json()
    assert len(response.json()["checksum"]) == 64  # SHA256 produces a 64-character hash

    # FastAPI Project

## Setup

1. Clone the repository.

```bash
git clone https://github.com/your-username/fastapi-project.git
cd fastapi-project
pip install -r requirements.txt
uvicorn main:app --reload

### **Final Steps to Commit to GitHub:**

- Make sure all your changes are saved.
- If you haven’t already, initialize a Git repository or use the existing one.

```bash
git init  # if you haven't already initialized a git repo
git add .
git commit -m "Added new API endpoint to generate checksum and test cases"
git push origin main
