---
title: "Flask - Celery - Redis Boiler Plate"
datePublished: Tue Nov 05 2024 15:07:28 GMT+0000 (Coordinated Universal Time)
cuid: cm34l3br5000209jsdpkrc5qv
slug: flask-celery-redis-boiler-plate
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1730819053055/581dd79e-e49f-4011-ac1f-410afc55faba.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1730818928107/b53737f4-fd3d-46c5-85f2-8e3c6cf3ce7d.png
tags: redis, python, flask, celery

---

## Synchronous Tasks

1. **Execution Flow**:
    
    * Synchronous tasks are executed sequentially, meaning that the application will wait for a task to complete before moving on to the next one.
        
    * The main thread of the application is blocked while a synchronous task is running. For example, if a request handler is executing a synchronous task, it will not handle other requests until the current task completes.
        
2. **Blocking**:
    
    * The application is blocked during the execution of the task. This can lead to performance issues if tasks are long-running or if there are many simultaneous tasks.
        
3. **Use Case**:
    
    * Suitable for tasks that are quick and do not require waiting for external resources or services. It is also simpler to implement and understand.
        

## Asynchronous Tasks

1. **Execution Flow**:
    
    * Asynchronous tasks are executed independently of the main execution flow. The application can continue to handle other requests while an asynchronous task is running.
        
    * Tasks are typically handled by background workers or threads, which do not block the main thread.
        
2. **Non-Blocking**:
    
    * The application is not blocked by the execution of asynchronous tasks. This improves responsiveness and can handle a higher volume of concurrent tasks.
        
3. **Use Case**:
    
    * Ideal for long-running tasks, I/O-bound operations, or tasks that involve waiting for external resources. It requires more complex implementation but can significantly improve performance and scalability.
        

# What is Celery?

Celery is an asynchronous task queue/job queue used to execute tasks in the background. It allows you to offload time-consuming tasks (like sending emails, processing files, etc.) from the main application to background workers, improving the user experience and performance.

* **Purpose in Backend**:
    
    * To **offload long-running tasks** to a background worker.
        
    * Handle tasks such as sending emails, image processing, or interacting with external APIs asynchronously.
        

## What is Redis ?

Redis is an in-memory data structure store, primarily used as a database, cache, and message broker. In a Flask application, Redis typically acts as the message broker for Celery, but it can also be used for caching.

* **Purpose in backend**:
    
    * **Message Broker** for Celery (to queue tasks and manage communication).
        
    * **Caching** data to improve performance by storing frequent queries or results in memory.
        

# **How Redis and Celery Work Together in a Flask App:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726294557526/b8d5632f-f447-4a51-890e-ca528785a9d3.png align="center")

1. **User Initiates Request:**
    
    * The process begins with a user making an HTTP request to the system.
        
2. **Request Handling by Gunicorn:**
    
    * The request is received by Gunicorn, which is a WSGI server that handles HTTP requests.
        
3. **Forwarding Request to Flask:**
    
    * Gunicorn forwards the HTTP request to the Flask application.
        
4. **Flask Processes Request:**
    
    * The Flask application processes the request. If the request involves asynchronous tasks, Flask will call Celery.
        
5. **Celery Manages Asynchronous Task:**
    
    * Flask sends an asynchronous task to Celery, which is responsible for managing background tasks.
        
6. **Task Queued in Redis:**
    
    * Celery adds the task to the Redis queue. Redis serves as a message broker, queuing tasks for processing.
        
7. **Worker Retrieves Task:**
    
    * Celery workers pull tasks from the Redis queue.
        
8. **Worker (Optional):**
    
    * The worker may perform additional actions such as storing results in a database, if applicable.
        
9. **Task Completion Notification (Optional):**
    
    * After completing the task, the worker may notify Flask (optional step depending on the architecture).
        
10. **Immediate Response Sent to User:**
    
    * Regardless of the background task, Flask sends an immediate response back to the user.
        

## Let’s Do a POC.

> <mark>You can find the boilerplate here → </mark> [https://github.com/AKXAT/Flask-Celery-Redis](https://github.com/AKXAT/Flask-Celery-Redis)

Create the Following Directory Structure.

```bash
.
└── flask_celery_redis_flower
    ├── backend
    │   ├── __init__.py
    │   ├── tasks.py
    │   └── views.py
    ├── celery_worker.sh
    ├── config.py
    ├── flower.sh
    ├── requirements.txt
    └── run.py
```

1. First of all the `run.py` is responsible for starting the flask Application.
    
2. the `config.py` has the URLs for Redis Strored.
    
    1. ```python
         import os
         
         # Flask configuration
         SECRET_KEY = os.getenv('SECRET_KEY', 'mysecret')
         
         # Redis and Celery configuration
         BROKER_URL = os.getenv('BROKER_URL', 'redis://localhost:6379/0')
         RESULT_BACKEND = os.getenv('RESULT_BACKEND', 'redis://localhost:6379/0')
        ```
        
3. `flower.sh` starts the Flower on local port.
    

> ### What Flower Does:
> 
> 1. **Monitor Tasks:**
>     
>     * Flower provides an interface to **track the status of tasks** executed by Celery workers. You can see which tasks are pending, started, completed, or failed, along with their execution time and result.
>         
> 2. **Inspect Workers:**
>     
>     * You can get detailed information about active workers such as:
>         
>         * Number of tasks they are processing.
>             
>         * Their current workload.
>             
>         * Worker uptime, state, and performance metrics.
>             
> 3. **Real-Time Monitoring:**
>     
>     * Flower allows you to monitor the Celery workers and tasks in real-time, making it easier to debug and optimize.
>         
> 4. **Task Events:**
>     
>     * View a history of task events like task retries, failures, and completion events.
>         
> 5. **Remote Control of Workers:**
>     
>     * Flower provides the ability to remotely control Celery workers through the web interface. You can pause/resume workers or revoke tasks.
>         

4. `celery_worker.sh` Starts Celery Worker.
    
5. `backend/__ini__.py` is Responsible for Importing Blue Prints and Initialising the Celery App.
    
    1. `make_celery` Function: This function is responsible for configuring and creating a **Celery instance** that is integrated with the Flask app.
        
        * `app.import_name`: The name of the Flask app is passed to Celery to allow it to use the same module name.
            
        * `backend=app.config['RESULT_BACKEND']`: This defines where task results are stored (in Redis, in this case). This enables Celery to store results after a task completes.
            
        * `broker=app.config['BROKER_URL']`: The **broker** is the message queue (Redis in this case) that Celery uses to pass messages between the Flask app and the workers.
            
        * `celery.conf.update(app.config)`: Updates the Celery configuration with any settings defined in the Flask app's configuration (such as timeouts, result serialization, etc.).
            
        * The function **returns** the fully configured Celery instance.
            
    2. `create_app` Function: `app = Flask(__name__)`: This creates a new Flask application.
        
        1. **Configuring Redis**:
            
            * `app.config['BROKER_URL']`: Specifies Redis as the message broker (`redis://127.0.0.1:6379/0`, meaning Redis is running on [`localhost`](http://localhost), port `6379`, and using the 0th database).
                
            * `app.config['RESULT_BACKEND']`: Also specifies Redis to store the results of tasks (same Redis instance and database). <mark>You can either hardcode it here or readi it from the Config.py</mark>
                
            * `celery = make_celery(app)`: Calls the `make_celery` function to configure and initialize Celery with the Flask app’s settings.
                
        2. **Blueprint Registration**:
            
            * The line `from .views import main as main_blueprint` imports a **Flask blueprint** called `main` from the `views`module (this part isn't shown, but blueprints allow splitting a Flask app into reusable components).
                
            * `app.register_blueprint(main_blueprint)`: Registers the blueprint with the Flask app.
                
        3. The function **returns** the Flask application instance, which will be used by the Flask server to handle requests.
            
    3. Global Celery Instance:
        
        1. This creates a **global Celery instance** that can be accessed from anywhere in the application.
            
        2. It initializes Celery by calling `make_celery(create_app())`, which creates a Flask app first and passes it into `make_celery` to create the Celery instance.
            
    4. ```python
         from flask import Flask
         from celery import Celery
         import os
         
         def make_celery(app):
             celery = Celery(
                 app.import_name,
                 backend=app.config['RESULT_BACKEND'],
                 broker=app.config['BROKER_URL']
             )
             celery.conf.update(app.config)
             return celery
         
         def create_app():
             app = Flask(__name__)
             
             # Set configuration for Redis
             app.config['BROKER_URL'] = 'redis://127.0.0.1:6379/0'
             app.config['RESULT_BACKEND'] = 'redis://127.0.0.1:6379/0'
         
             # Initialize Celery with the Flask app context
             celery = make_celery(app)
         
             # Register the blueprint
             from .views import main as main_blueprint
             app.register_blueprint(main_blueprint)
         
             return app
         
         # Create a Celery instance globally to be accessed from tasks
         celery = make_celery(create_app())
        ```
        
6. Route to Trigger the `long_task`: `/longtask`
    
    1. 1. ```python
              @main.route('/longtask', methods=['GET'])
              def start_long_task():
                  task = long_task.apply_async()
              
                  return jsonify({
                      'task_id': task.id,
                      'status': 'Long task submitted!',
                  }), 202
            ```
            
    2. **What This Route Does:**
        
        * **URL Endpoint**: `/longtask` (called using a `GET` request).
            
        * **Triggering a Task**:
            
            * `long_task.apply_async()`: This is the key line that **submits the task to Celery** asynchronously.
                
                * `long_task` is a Celery task defined below, and `.apply_async()` is a method that sends the task to the Celery workers, allowing it to run in the background.
                    
                * Once the task is submitted, it does not block the Flask web server from continuing to serve other requests.
                    
            * [`task.id`](http://task.id): This is a **unique ID** that Celery generates for the task. This ID can be used later to track the task's progress or retrieve its result.
                
        * **Response**:
            
            * A JSON response is returned, which includes:
                
                * `task_id`: The unique task ID for tracking.
                    
                * `status`: A confirmation message that the task has been submitted.
                    
            * The HTTP status code is `202`, which means **"Accepted"**—the server has accepted the request, but it hasn't been completed yet (since the task will run in the background).
                
7. Example Celery Task: `long_task`
    
    1. ```python
         @current_app.task
         def long_task():
             import time
             for i in range(300):
                 print(f"Running step {i}...")
                 time.sleep(10)  # Simulate a time-consuming task
             return "Task complete!"
        ```
        
    2. **What This Task Does:**
        
        * **Task Definition**:
            
            * `@current_app.task`: This decorator registers the `long_task` function as a **Celery task**. Celery will recognize this as a function it can execute asynchronously when it's called (e.g., via `apply_async()`).
                
        * **Simulating a Long Task**:
            
            * The task simulates a long-running process by iterating over a loop with 300 steps.
                
            * In each iteration, it:
                
                * **Prints** a message (`print(f"Running step {i}...")`), which could appear in the logs.
                    
                * **Sleeps** for 10 seconds (`time.sleep(10)`), simulating a time-consuming operation.
                    
            * This means the entire task will take approximately 300 \* 10 = **3000 seconds** (or about 50 minutes) to complete.
                
        * **Return Value**:
            
            * When the loop finishes, the task returns `"Task complete!"`. This result will be saved in Redis (the result backend), and it can be retrieved via the status check endpoint (`/status/<task_id>`).
                
8. Route to Check Task Status: `/status/<task_id>`
    
    1. ```python
         @main.route('/status/<task_id>', methods=['GET'])
         def task_status(task_id):
             task = long_task.AsyncResult(task_id)
         
             if task.state == 'PENDING':
                 response = {
                     'state': task.state,
                     'status': 'Pending...',
                 }
             elif task.state == 'SUCCESS':
                 response = {
                     'state': task.state,
                     'result': task.result,
                 }
             else:
                 response = {
                     'state': task.state,
                     'status': str(task.info),  # Can contain error messages or other info
                 }
         
             return jsonify(response)
        ```
        
    2. **What This Route Does:**
        
        * **URL Endpoint**: `/status/<task_id>` (called using a `GET` request). The `<task_id>` is a variable in the URL, which represents the unique ID of the task you want to check.
            
        * **Checking Task Status**:
            
            * `long_task.AsyncResult(task_id)`: This retrieves the **task status** and result for the given `task_id`. Celery provides the `AsyncResult` object, which holds the state and result of a task.
                
        * **Task State Handling**:
            
            * `PENDING`: If the task hasn't started yet or is waiting to be executed, it returns a response with the state `"PENDING"` and a message `"Pending..."`.
                
            * `SUCCESS`: If the task has successfully completed, it returns the state `"SUCCESS"` and the actual result (`task.result`), which will be the return value of the task.
                
            * **Other States**: For any other states (e.g., `STARTED`, `RETRY`, `FAILURE`), it returns the current state and any additional information from [`task.info`](http://task.info). This might include error messages if the task failed or any relevant progress information.
                
        * **Response**:
            
            * A JSON response is returned with the task's current **state** and **status** or **result**, depending on what stage the task is in.
                

## How To Test Locally.

### Corrected Steps for Starting the Project Locally:

1. **Clone the Project:**
    
    ```bash
    git clone https://github.com/AKXAT/Flask-Celery-Redis.git
    ```
    
2. **Navigate to the Project Directory:**
    
    ```bash
    cd Flask-Celery-Redis
    ```
    
3. **Create a Virtual Environment:**
    
    ```bash
    python -m venv venv
    ```
    
4. **Activate the Virtual Environment:**
    
    * For **Linux/macOS**:
        
        ```bash
        source venv/bin/activate
        ```
        
5. **Install the Requirements:**
    
    ```bash
    pip install -r requirements.txt
    ```
    
6. **Install and Start Redis Server:**
    
    * If Redis is not installed on your system, install it first:
        
        * For **macOS** (using Homebrew):
            
            ```bash
            brew install redis
            ```
            
        * For **Ubuntu/Linux**:
            
            ```bash
            sudo apt-get install redis-server
            ```
            
    * **Start Redis** (if it's not already running):
        
        ```bash
        redis-server
        ```
        
    * **Verify Redis is Running**: You can use the following command to test if Redis is working:
        
        ```bash
        redis-cli ping
        ```
        
        If it returns `PONG`, Redis is up and running.
        
7. **Run Celery Worker:** Run the Celery worker to process background tasks.
    
    * If `celery_worker.sh` is provided in the project, run it:
        
        ```bash
        ./celery_worker.sh
        ```
        
8. **Run Flower (Optional for Monitoring):** If you want to use **Flower** for real-time monitoring of Celery tasks:
    
    * If `flower.sh` is provided, run it:
        
        ```bash
        ./flower.sh
        ```
        
9. **Start the Flask Application:** To run the Flask app, start it from `run.py`:
    
    ```bash
    python run.py
    ```
    
10. **Test the Endpoints:** Now that everything is up and running, you can test the endpoints defined in your Flask app, such as:
    
    * Submitting a long task at `/longtask`.
        
    * Checking task status at `/status/<task_id>`.
        

## **Thank you for reading!**

I’m glad you made it to the end of this article. I hope you found the insights valuable. If you did, please consider leaving a like. Your support motivates me to continue writing and sharing more content in the future.

* [**My GitHub Repos**](https://github.com/akxat)
    
* Connect with me on [**Linkedin**](https://www.linkedin.com/in/sharma-akshat/)
    
* Start [**your own blogs**](https://hashnode.com/@AkshatSharma/joinme)
    

%%[wid-1]