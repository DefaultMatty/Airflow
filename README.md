### Building and running your application

When you're ready, start your application by running:
`docker compose up --build`.

Your application will be available at http://localhost:8000.

### Deploying your application to the cloud

First, build your image, e.g.: `docker build -t myapp .`.
If your cloud uses a different CPU architecture than your development
machine (e.g., you are on a Mac M1 and your cloud provider is amd64),
you'll want to build the image for that platform, e.g.:
`docker build --platform=linux/amd64 -t myapp .`.

Then, push it to your registry, e.g. `docker push myregistry.com/myapp`.

Consult Docker's [getting started](https://docs.docker.com/go/get-started-sharing/)
docs for more detail on building and pushing.

### References
* [Docker's Python guide](https://docs.docker.com/language/python/)


Create .env  with generated fernet key following Python command:
bash
Copy code
python -c "from cryptography.fernet import Fernet; print(Fernet.generate_key().decode())"


Create Necessary Directories
Create directories that will be used to store your DAGs, logs, and plugins:
bash
Copy code
mkdir dags logs plugins


Initialize the Airflow Database
Before starting the Airflow services, you need to initialize the Airflow metadata database.
Start the containers (except the webserver):
bash
Copy code
docker-compose up -d postgres


Run the database migration:
bash
Copy code
docker-compose run airflow-webserver airflow db migrate
This will migrate the database to the latest version.

Create the Admin User
After the database migration, create an admin user for the Airflow web interface:
bash
Copy code
docker-compose run airflow-webserver airflow users create --username admin --password admin --firstname Admin --lastname User --role Admin --email admin@example.com
You can replace the username, password, and email with your preferred credentials.

Start the Airflow Services
Now you can start all the Airflow services using Docker Compose:
bash
Copy code
docker-compose up -d
This will start the services in the background. The Airflow webserver will be accessible at http://localhost:8080.

Access the Airflow UI
Open your web browser and navigate to http://localhost:8080. Log in with the credentials you created earlier (e.g., username: admin, password: admin).

Stopping and Removing the Containers
When you're done, you can stop the containers with:
bash
Copy code
docker-compose down



get fernet key by doing below in terminal 
-m venv airflow_env
.\airflow_env\Scripts\activate
pip install cryptography
python fernetkey.py

Copy into .env file