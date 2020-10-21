# Airflow

## Running locally
1. Create a Virtual Environment and activate it.
2. Install Airflow requirements.
3. In one terminal in the virtual env, run:
    ```
    export AIRFLOW_HOME=./templates  # this is wherever you want to put your dags
    export OBJC_DISABLE_INITIALIZE_FORK_SAFETY=YES
    export ENV_VARIABLE1=1 # Set environment variables

    airflow initdb  # Only needs run the first time.

    airflow webserver -p 8080
    ```
4. In another terminal running the virtual env, run:
    ```
    export AIRFLOW_HOME=./templates # this is wherever you want to put your dags
    export OBJC_DISABLE_INITIALIZE_FORK_SAFETY=YES
    export ENV_VARIABLE1=1 # Set same environment variables

    airflow scheduler
    ```
5. Navigate to http://0.0.0.0:8080/admin

## Directory Set Up
* Have a "Deployment" folder, that contains a "templates" (dags) folder.
* For running locally, set AIRFLOW_HOME to a new directory and create symbolic links to the Deployment folder.
* Have a "shared" directory, that contains functions across the dags.
    * Within the shared folder, have a "dag_functions.py" file, that wraps the functions into ones usable by Airflow, and handles things like Airflow context. Import these into Airflow and point the PythonOperator at them. Do not define new functions in dags.
