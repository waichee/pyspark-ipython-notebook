Setting up IPython Notebook with PySpark
==========================================

This is a brief notes on setting up environments for running pyspark via ipython notebook 
with Spark v1.4.1. The steps detailed are with running standalone spark on a single node.
If you wish to run on amazon clusters, there’s the spark’s ec2 script for running on Amazon EC2, or directly create the EMR job and 
select Spark as an add-on via AWS Web console.


Requirements
============

* Java 1.7 or greater
* Maven or Simple build tool (sbt)


Install Spark
============

Download latest spark (which is 1.4.1 as of July 2015)  from https://spark.apache.org/downloads.html
I've selected  spark-1.4.1.tar

extract the tar file

	tar -xvf spark-1.4.1.tar

build spark as per the README.md. 
alternatively you can download the pre-built version if you wish and you can skip this step.

	mvn clean package -DskipTests

Setup your environment variables for "SPARK_HOME" 
E.g. in Unix environments, add the following to ~/.bash_profile

	export SPARK_HOME=<location of the install>
	export PATH=$SPARK_HOME/bin:$PATH

verify that pyspark is installed ok

	cd <spark-distro-directory>
	./bin/pyspark
	
	import math
	testRdd = sc.parallelize([4,16,9])
	testRdd.map(math.sqrt).collect()
	
	#verify results
	
	#to quit
	exit()
	

Install Python
============


Install Anaconda
-----------------

Download Anaconda which include python 2.7 and the main scientific libraries
http://ipython.org/install.html

	conda update conda
	conda update ipython ipython-notebook ipython-qtconsole

	
Anaconda comes with free spyder IDE. There is other free IDEs and text editors such as Sublime, emacs.
There's also non-free ones such as PyCharm by Jetbrains.


Run PySpark from IPython notebook
-----------------------------------

Ipython notebook is sort of similar to Mathematica. Its a web app that allows you to write descriptions, 
images, visualization and executing run code. 

Download the following python setup script from Github to create a new pyspark profile for running Ipython notebook
https://github.com/felixcheung/vagrant-projects/blob/master/Spark-IPython-Zeppelin-Lightning/ipython-pyspark.py

Run 
	python ipython-pyspark.py
		
Start ipython notebook from terminal

	ipython notebook
	
Open your browser and navigate to to view the ipython notebooks:

	localhost:1088

If you would like to change to a different port, modify the following line in the ipython-pyspark.py script

	ip = '*' # Warning: this is potentially insecure
	port = <new-port>

Create a new notebook by 
* New-> Python(2 or 3) 
* Press + to create new cell
* Press play icon to run (or ctrl +enter)

Test that Pyspark is working from Ipython notebook by pasting the following to a cell and hit run

	import math
	testRdd = sc.parallelize([16,16,9])
	testRdd.map(math.sqrt).collect()
	








