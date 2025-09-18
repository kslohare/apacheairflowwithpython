# Setup of Apache Airflow in vscode project
## Adding 
cd /home/ksl/code/apacheairflowwithpython
touch .gitignore
## Virtual Envirnment creation
cd /home/ksl/code/apacheairflowwithpython # Make sure you are in project root folder \
python3 -m venv airflow_env  # It will create airflow_env folder in root folder. \
source airflow_env/bin/activate \
pip install apache-airflow \
airflow db init #Only once at the beginning \

## To  create new user and pwd for Airflow web application
airflow users create \
    --username admin \
    --password admin \
    --firstname kishor \
    --lastname Lohare \
    --role Admin \
    --email loharekishor@gmail.com

## Start Scheduler deamon job
### It creates Log File named airflow-scheduler.log
#nohup airflow scheduler > airflow-scheduler.log 2>&1 &
nohup airflow scheduler > "airflow-scheduler-$(date +%Y%m%d).log" 2>&1 &

## Start webserver deamon job
#nohup airflow webserver --port 8080 > airflow-web.log 2>&1 &
nohup airflow webserver --port 8080 > "airflow-web-$(date +%Y%m%d).log" 2>&1 &
 
## Hit below url to open web page
http://localhost:8080

## To see dag list
airflow dags list
 
## If your database is corrupted, missing DAGs, or behaving strangely, you can reset it:
airflow db reset
 
## To kill the deamon processes of airflow
ps aux | grep airflow
killl -9 pid

## Restart the Airflow Webserver:
### Find the process ID (look for the airflow webserver command)
ps aux | grep "airflow webserver"
### Kill the process (replace <PID> with the actual process ID)
kill <PID>
### Wait a few seconds, then restart it (using your preferred method)
nohup airflow webserver --port 8080 > "airflow-web-$(date +%Y%m%d).log" 2>&1 &
