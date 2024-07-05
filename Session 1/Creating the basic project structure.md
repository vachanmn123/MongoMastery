## Step 1: Create a new file named `app.py`
Create a new file named `app.py` 

## Step 2: Add the following code
```py
from flask import Flask

app = Flask(__name__)

@app.route("/")
def index():
	return "Hello, World!"

if __name__ == "__main__":
	app.run(debug=True)
```
