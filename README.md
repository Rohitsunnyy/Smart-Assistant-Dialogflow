# Smart-Assistant-Dialogflow (Food Ordering Chatbot)

![Project Image](./img.webp)

## Introduction

This project is a **food ordering chatbot** built using **FastAPI** for the backend and **Dialogflow** for natural language understanding. It allows users to add, remove, and track orders through a conversational interface. The chatbot interacts with a MySQL database to store and manage orders and uses ngrok to expose the local server for testing with Dialogflow.

## Features
- Add items to an ongoing order.
- Remove items from the order.
- Complete and confirm an order.
- Track an existing order using the order ID.
- Built using FastAPI and connected to a MySQL database.
- Integrated with Dialogflow to handle natural language inputs.
  
## Requirements

Before running the project, make sure you have the following installed:

- **Python 3.8+**
- **FastAPI**
- **MySQL**
- **ngrok** (for exposing localhost to the internet for webhook integration with Dialogflow)
  
## Project Setup

### 1. **Clone the Repository**

```bash
git clone https://github.com/Rohitsunnyy/Smart-Assistant-Dialogflow.git
cd Smart-Assistant-Dialogflow
```

### 2. **Install Required Dependencies**

It's recommended to create a virtual environment before installing dependencies:

```bash
# Create virtual environment
python3 -m venv venv

# Activate virtual environment
source venv/bin/activate  # On Windows use `venv\Scripts\activate`

# Install dependencies
pip install -r requirements.txt
```

### 3. **Set Up the Database**

Ensure you have a MySQL database running. You can create a new database and run the following SQL to set up the required tables:

```sql
CREATE DATABASE pandeyji_eatery;

USE pandeyji_eatery;

CREATE TABLE food_items (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    price DECIMAL(10, 2)
);

CREATE TABLE orders (
    order_id INT AUTO_INCREMENT PRIMARY KEY
);

CREATE TABLE order_tracking (
    order_id INT,
    status VARCHAR(255),
    FOREIGN KEY (order_id) REFERENCES orders(order_id)
);
```

### 4. **Run the FastAPI Server**

To run the server locally, use `uvicorn`:

```bash
uvicorn main:app --reload --port 8000
```

### 5. **Expose Localhost Using ngrok**

To test the webhook with Dialogflow, use ngrok to expose your local server:

```bash
ngrok http 8000
```

Copy the HTTPS URL from ngrok and paste it in the webhook section of your Dialogflow agent settings.

### 6. **Dialogflow Integration**

1. Create a Dialogflow agent.
2. Set up the intents:
   - `order.add - context: ongoing-order`
   - `order.remove - context: ongoing-order`
   - `order.complete - context: ongoing-order`
   - `track.order - context: ongoing-tracking`
3. Use the ngrok HTTPS URL as the webhook for your Dialogflow agent.
4. Test the bot by interacting with it via the Dialogflow console.

### 7. **Track an Order**

To track an existing order, provide the order ID, and the chatbot will return the current status of the order.

## Project Structure

```
/Smart-Assistant-Dialogflow
│
├── db_helper.py            # Helper functions for database operations
├── generic_helper.py       # Utility functions
├── main.py                 # FastAPI app and intent handlers
├── requirements.txt        # Python dependencies
├── .gitignore              # Files to be ignored by Git
└── README.md               # Project documentation
```



## Contact

- Rohit Kumar
- Email: gaddamsreeramulu.r@northeastern.edu

Feel free to reach out if you have any questions or feedback!



