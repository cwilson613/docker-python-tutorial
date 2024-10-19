# Python/Docker Interactive

## Overview

This project demonstrates a basic Python web application built with Flask, containerized using Docker. It includes instructions for setting up a local development environment, building and running the application, and containerizing it with Docker.

## Python Project Structure

```
/src
├── LICENSE
├── README.md
├── requirements.txt
├── routes.py
├── static
│   ├── css
│   │   └── main.css
│   └── images
│       ├── durga.jpg
│       ├── naam_tamilar_flag.jpg
│       └── tiger.jpg
└── templates
├── base.html
├── index.html
├── myth.html
└── symbol.html
```

The application serves static content and HTML templates, using Flask to handle routing and backend logic.

## Basic Python Application

### Set Up Local Environment

1. **Create a python virtual environment**:

This will keep our dependencies and python binaries isolated so that we don't pollute our system's python environment.

```bash
python3 -m venv venv
```

The `.gitignore` file is already configured to exclude the venv/ and env/ directories.

2.	**Activate the virtual environment**:

```bash
source venv/bin/activate
```

### Install Dependencies

Install the required Python packages using requirements.txt:

```bash
pip install -r src/requirements.txt
```

```bash
Collecting appdirs==1.4.4 (from -r src/requirements.txt (line 1))
  Using cached appdirs-1.4.4-py2.py3-none-any.whl.metadata (9.0 kB)
Collecting blinker==1.8.2 (from -r src/requirements.txt (line 2))
  Using cached blinker-1.8.2-py3-none-any.whl.metadata (1.6 kB)
Collecting click==8.1.7 (from -r src/requirements.txt (line 3))
  Using cached click-8.1.7-py3-none-any.whl.metadata (3.0 kB)
Collecting Flask==3.0.3 (from -r src/requirements.txt (line 4))
  Using cached flask-3.0.3-py3-none-any.whl.metadata (3.2 kB)
Collecting itsdangerous==2.2.0 (from -r src/requirements.txt (line 5))
  Using cached itsdangerous-2.2.0-py3-none-any.whl.metadata (1.9 kB)
Collecting Jinja2==3.1.4 (from -r src/requirements.txt (line 6))
  Using cached jinja2-3.1.4-py3-none-any.whl.metadata (2.6 kB)
Collecting MarkupSafe==3.0.2 (from -r src/requirements.txt (line 7))
  Using cached MarkupSafe-3.0.2-cp313-cp313-macosx_11_0_arm64.whl.metadata (4.0 kB)
Collecting packaging==24.1 (from -r src/requirements.txt (line 8))
  Using cached packaging-24.1-py3-none-any.whl.metadata (3.2 kB)
Collecting pyparsing==3.2.0 (from -r src/requirements.txt (line 9))
  Using cached pyparsing-3.2.0-py3-none-any.whl.metadata (5.0 kB)
Collecting six==1.16.0 (from -r src/requirements.txt (line 10))
  Using cached six-1.16.0-py2.py3-none-any.whl.metadata (1.8 kB)
Collecting Werkzeug==3.0.4 (from -r src/requirements.txt (line 11))
  Using cached werkzeug-3.0.4-py3-none-any.whl.metadata (3.7 kB)
Using cached appdirs-1.4.4-py2.py3-none-any.whl (9.6 kB)
Using cached blinker-1.8.2-py3-none-any.whl (9.5 kB)
Using cached click-8.1.7-py3-none-any.whl (97 kB)
Using cached flask-3.0.3-py3-none-any.whl (101 kB)
Using cached itsdangerous-2.2.0-py3-none-any.whl (16 kB)
Using cached jinja2-3.1.4-py3-none-any.whl (133 kB)
Using cached MarkupSafe-3.0.2-cp313-cp313-macosx_11_0_arm64.whl (12 kB)
Using cached packaging-24.1-py3-none-any.whl (53 kB)
Using cached pyparsing-3.2.0-py3-none-any.whl (106 kB)
Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Using cached werkzeug-3.0.4-py3-none-any.whl (227 kB)
Installing collected packages: appdirs, six, pyparsing, packaging, MarkupSafe, itsdangerous, click, blinker, Werkzeug, Jinja2, Flask
Successfully installed Flask-3.0.3 Jinja2-3.1.4 MarkupSafe-3.0.2 Werkzeug-3.0.4 appdirs-1.4.4 blinker-1.8.2 click-8.1.7 itsdangerous-2.2.0 packaging-24.1 pyparsing-3.2.0 six-1.16.0
```

### Build, Test, and Run the Application

1.	Run the Flask application:

```bash
python src/routes.py
```

```bash
 * Serving Flask app 'routes'
 * Debug mode: on
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:8080
 * Running on http://172.17.0.2:8080
Press CTRL+C to quit
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 440-851-870
```

2.	Test the application:
Open your browser and navigate to http://localhost:8080 to see the running app.
	
3.	Make changes to the code in the src directory, and Flask will automatically reload the app if you’re running in development mode.

4.  `Ctrl+C` will stop the app.

### Package/Distribution Analysis

Distributing this Flask app for other users could involve:

* Creating a `.whl` or `.tar.gz` package for Python distribution.
* Using a Docker container to ensure the environment is consistent across different systems.
* Packaging the app as a self-contained executable using tools like `pyinstaller`

## Containerize

Container Introduction (Docker)

### Run an Ubuntu Container

1.	Pull and run the Ubuntu image:

```bash
docker run -ti ubuntu:latest
```

2. **Execute basic Linux commands** inside the container:

```bash
apt update
apt install -y wget curl
curl https://google.com
whoami
cat /etc/os-release
```

3. **Exit the container:**

```bash
exit
```

4. Check image size:

```bash
docker images
```

5. Run an anternate image or other platform (e.g. alpine, linux-amd64):

```bash
docker run -ti alpine:latest
```

```bash
docker run -ti --platform=linux/amd64 alpine:latest
```

### Run Python Containers

1. Pull and run a Python image, targeting `bash`. The default entrypoint is `python`, which will just lead to an open python interpreter terminal, which we don't want.

```bash
docker run -ti python:3 bash
```

2. Check Python and pip versions:

```bash
python --version
pip --version
```

3. Inspect the system info (Should be a Debian linux flavor):

```bash
cat /etc/os-release
```

4. Exit the container and check image size:

```bash
exit
docker images
```

Example:

```bash
REPOSITORY                    TAG       IMAGE ID       CREATED        SIZE
python                        3         c4919c7c59fa   11 days ago    1.02GB
```

5. Run an alternate Python image (e.g. Alpine-based):

```bash
docker run -ti python:alpine bash
```

6. Check Python and pip versions:

```bash
python --version
pip --version
```

7. Inspect the system info (Should be a Debian linux flavor):

```bash
cat /etc/os-release
```

8. Exit the container and check the alpine image size:

```bash
exit
docker images
```

Example:

```bash
REPOSITORY                    TAG       IMAGE ID       CREATED        SIZE
python                        alpine    5957ff45e8eb   17 hours ago   48.8MB
```

Much smaller!

### Volume Mounting

For this section we're going to mount our code into the container with a volume.
For this section we're going to mount our code into the container with a volume.

1. Run a Python container with the volume mount, and ports mapped to our machine:

```bash
docker run -ti -p 8080:8080 -v $(pwd)/src:/app -w /app python:alpine sh
```

2. Inside the container, install dependencies and run the code as normal:

```bash
pip install -r requirements.txt
python routes.py
```

3.	If you modify the source code on your local machine, and the changes will reflect inside the container.

4.	Difference between container files and mounted files:
* Files in the mounted directory are accessible and editable from both the host and the container.
* Changes to mounted files update immediately.

5. Hitting http://localhost:8080 should still show the webpage; your local machine's port 8080 is bound by Docker, forwarding traffic into the container at port 8080 as well.  Since the application is listening on that port in the container, the connection is established all the way through, end to end.

6. Exit the Python run with `Ctrl+C`, and then exit the container

```bash
exit
```

### Basic Dockerfile

Create a basic Dockerfile in the project root:

```dockerfile
# Use an official Python (slim, small) runtime as a parent image
FROM python:3.12-slim

# Set the working directory
WORKDIR /app

# Copy the src directory contents into the container at /app
COPY ./src /app

# Install any necessary dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Make port 8080 available to the world outside this container
EXPOSE 8080

# Define the environment variable for Flask
ENV FLASK_APP=routes.py

# Run the application
CMD ["python", "routes.py"]
```

1.	Explanation of Dockerfile Commands:
* `FROM`: Specifies the base image.
* `WORKDIR`: Sets the working directory.
* `COPY`: Copies the source code.
* `RUN`: Executes commands to install dependencies.
* `EXPOSE`: Opens a port on the container.
* `CMD`: Defines the command to start the application.

2. Build the Docker image:

```bash
docker build -t flask-app .
```

3. Run the container:

```bash
docker run -p 8080:8080 flask-app
```

Sample Output:

```bash
 * Serving Flask app 'routes'
 * Debug mode: on
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:8080
 * Running on http://172.17.0.2:8080
Press CTRL+C to quit
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 942-332-237
```

4.	Access the application in your browser at http://localhost:8080.

## Advanced Topics

* Multistage builds to minimize image size.
* Using Docker Compose to manage multiple containers.
* Deploying the container to cloud platforms like AWS, Azure, or GCP.
* Pushing image to registry

License

This project is licensed under the MIT License - see the LICENSE file for details.

Contributing

Feel free to submit issues and feature requests. Contributions are welcome.