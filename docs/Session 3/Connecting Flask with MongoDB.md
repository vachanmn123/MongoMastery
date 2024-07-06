
Now that we have understood what we want to achieve with our schema, lets connect MongoDB to our flask app we started earlier.

1. **Install Flask-PyMongo**
	Open a new terminal in the same folder we were working before (make sure to activate the venv) and run the following command:
     ```bash
     pip install Flask-PyMongo
     ```

2. **Configure Flask to Connect to MongoDB**
   - **Update `app.py` to Include MongoDB Configuration**:
     ```python
     from flask import Flask
     from flask_pymongo import PyMongo

     app = Flask(__name__)

     # Set up MongoDB configuration
     app.config["MONGO_URI"] = "mongodb://<YOUR-CONNECTION-STRING>/<YOUR-DATABASE-NAME>"

     # Initialize PyMongo
     mongo = PyMongo(app)

     @app.route('/')
     def home():
         return "Hello, Flask and MongoDB!"

     if __name__ == '__main__':
         app.run(debug=True)
     ```

3. **Best Practices for Database Connection**
	Storing your connection string inside the code is considered bad practice and it can be hard to change in the future and can also be compromised in the event of a code leak.
   - **Use Environment Variables**: Store database connection strings and credentials securely.
     - Install `python-dotenv`:
	     Install the `python-dotenv` package using the following command:
       ```bash
       pip install python-dotenv
       ```

     - **Create a `.env` File**:
	     Create a new file called `.env` inside the same folder and add your connection string in the following format:
       ```
       MONGO_URI=mongodb://<YOUR-CONNECTION-STRING>/<YOUR-DATABASE-NAME>
       ```

     - **Load Environment Variables in `app.py`**:
       ```python
       import os
       from dotenv import load_dotenv
       from flask import Flask
       from flask_pymongo import PyMongo

       load_dotenv()  # Load environment variables from .env file

       app = Flask(__name__)

       # Set up MongoDB configuration
       app.config["MONGO_URI"] = os.getenv("MONGO_URI")

       # Initialize PyMongo
       mongo = PyMongo(app)

       @app.route('/')
       def home():
           return "Hello, Flask and MongoDB!"

       if __name__ == '__main__':
           app.run(debug=True)
       ```

Ensure there are no errors when you run the app now.