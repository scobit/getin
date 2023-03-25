Spark is a library



sandbox01 - old sandbox

second password asking - is kerberos password - not yours

currently it is AD and with getindata ask was another


# Launch cell in notebook
SHift + ENter
Ctrl + Enter


Spark - yarn client mode

By default spark is configured to run in the yarn mode (new application is started on yarn)


Notebook - restart the kernel and run all cells
Notebook - change Kernel - chose Python3.6Sandbox

Accepted state means  that request fro spark application was valid (credentials valid) but it was not assigned to run in any notebooks
Basically applucation master jvm was not started

When AM finally starts and provides it's status to spark driver the state will be changed from accepted to running

Spark driver is executed on client side


Yarn RM 
http://master-02.kraken.kcell.kz:8088/cluster

Capacity scheduller link 
http://master-02.kraken.kcell.kz:8088/cluster/scheduler

application_1669883481063_37759

container in yarn is just a process started for you

container contains application id and attempt id

application_id contain 
apllication_
RM timestamp last restarted 
date -d @TimeStamp
incremented number of application that was started

Application has appattempt

AM must be able to connect to task requester

Python interpreter must be is the same version running in a worker and in drivers, THis is because when we creating function in python it is transfered to executores as the python code. And we need to ensure that theere is the same way of interpreting this function on both - driver (notebook) and on executors

When we restart kernel it release all resources from yarn


# in notebook terminal
https://gitlab.kcell.kz/kraken/analytics/training_analytics_in_dl

# study
https://gitlab.kcell.kz/kraken/analytics/training_analytics_in_dl/-/blob/master/Working%20with%20GitLab/Working%20with%20GitLab.ipynb





import os
os.environ['PYSPARK_PYTHON'] = 'python3'
from pyspark.sql import SparkSession
spark = SparkSession.builder \
    .enableHiveSupport() \
    .getOrCreate()


# function to create dataframe of some numbers (lenght of this dataframe) and show means that dataframe is printed back to you
# this is spark jvm example, not python!
spark.range(10).show()


# python function
def addone(number):
    print("Adding one to number " + str(number))
    return number + 1

spark.range(10).rdd.map(lambda r: addone(r.id)).collect()

# check what application id was assigned to our apllication
spark.sparkContext.applicationId


# logs on old sandbox are hidden and visible via docker logs
on new sandbox it will be fixed
    

spark yarn cluster way aka headless mode - because we don't have no ability to interfiew the work that was already planned
SO basically we have out spark job, this code ships to cluster and line by line this code is beeing executed in yarn

THis is prefered way to kubeflow pipeline  contains spark driver

In this way driver is not on sandbox machine, it's running on the slave

In this way we can get driver logs of the driver machine (in yarn client mode the stdout of driver was empty and logs output was redirected to stderr).

logs of the driver - stdout
python logs on the executor - stderr




http://master-02.kraken.kcell.kz:8088/proxy/application_1669883481063_38076/


http://master-02.kraken.kcell.kz:18081/history/application_1669883481063_38076/environment/


spark jobs via local[*]
intoruced on new sandbox
in this way yarn is no longer involved in the execution
we are not using hadoop resources, instead we are using k8s cluster nodes


RPC - remote procedure call


artifactory.kcell.kz:6555/datalake-jupyterlab-kubeflow:298


Spark 3 init cell

import findspark
findspark.init('/opt/spark3')

import kcellspark
from pyspark.sql import SparkSession
spark = SparkSession.builder \
    .config('spark.driver.memory', '2g') \
    .enableHiveSupport() \
    .getOrCreate()
print(kcellspark.get_ui_url())

spark.range(10).show()

https://spark3.kraken.kcell.kz/history/local-1679222126517


on sandbox01 (253.217) was AD ssh access (not FreeIPA)

username@hostname:./

gb_videos.show()

import socket 
socket.gethostname()


2 11 time
