https://chatgpt.com/share/679b46e4-1b5c-8002-94f3-9c88f0d89b64

# wordCount
Step 1: Check If Hadoop Is Installed
Open the Terminal in Cloudera and run:

sh
Copy
Edit
hadoop version
If Hadoop is installed correctly, you will see its version. If not, let me know so I can guide you on installing it.

Step 2: Set Hadoop Classpath
If Hadoop is installed but still shows the error, try setting the classpath manually:

sh
Copy
Edit
export HADOOP_CLASSPATH=$(hadoop classpath)
To make this setting permanent, add it to your .bashrc file:

sh
Copy
Edit
echo 'export HADOOP_CLASSPATH=$(hadoop classpath)' >> ~/.bashrc
source ~/.bashrc
Now, try running:

sh
Copy
Edit
hadoop classpath
Step 3: Verify Apache Commons Logging Library
Run this command to check if the required JAR files exist:

sh
Copy
Edit
find /usr/lib/hadoop -name "commons-logging-*.jar"
If you find the JAR file, add it to your Hadoop job manually when running:

sh
Copy
Edit
hadoop jar wc1.jar wc1 -libjars /usr/lib/hadoop/lib/commons-logging-1.1.3.jar /path/to/input /path/to/output
Step 4: Run Your Hadoop Job in Eclipse
Open Eclipse in Cloudera.

Right-click your wc1 project > Properties > Java Build Path.

Under Libraries, click Add External JARs.

Add the following JAR files from Hadoop’s lib directory:

commons-logging-*.jar
hadoop-common-*.jar
hadoop-mapreduce-client-core-*.jar
Any missing dependencies
Click Apply and Close.

Run your Hadoop program inside Eclipse.

Step 5: Run the Hadoop Job Manually
If you still get an error in Eclipse, try running it manually from the terminal:

sh
Copy
Edit
hadoop jar wc1.jar wc1 /user/cloudera/input /user/cloudera/output
Then, check the output:

sh
Copy
Edit
hdfs dfs -cat /user/cloudera/output/part-r-00000
Let me know if you need further clarification! 🚀




✅ Step 1: Check If the JAR File Exists
Run this command:

sh
Copy
Edit
ls -lh /home/cloudera/wc1.jar
If the file does not exist, you need to recompile and package your JAR (see Step 2).
If the file exists but is corrupt, recreate it.
✅ Step 2: Recompile and Create the JAR File
Navigate to the directory where your wc1.java file is located:

sh
Copy
Edit
cd /home/cloudera
Then, recompile it with Hadoop dependencies:

sh
Copy
Edit
javac -classpath $(hadoop classpath) -d . wc1.java
Now, package it into a JAR:

sh
Copy
Edit
jar cf wc1.jar wc1/*.class
Check if the JAR was created:

sh
Copy
Edit
ls -lh wc1.jar
✅ Step 3: Run the Hadoop Job
Now try running your job again:

sh
Copy
Edit
hadoop jar wc1.jar wc1 /user/cloudera/input /user/cloudera/output
If you get a missing dependency error (like commons-logging), try adding:

sh
Copy
Edit
hadoop jar wc1.jar wc1 -libjars /usr/lib/hadoop/lib/commons-logging-1.1.3.jar /user/cloudera/input /user/cloudera/output
✅ Step 4: Verify the Output
If the job runs successfully, check the results:

sh
Copy
Edit
hdfs dfs -cat /user/cloudera/output/part-r-00000
Let me know if you still face issues! 🚀
