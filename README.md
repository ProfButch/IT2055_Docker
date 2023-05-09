# IT2055 MongoDB/Anaconda/Jupyter Docker Setup
This is a simple Docker setup that gives you
* MongoDB server (running latest version)
* Anaconda server (running the latest version)
    * Jupyter notebooks



# Creating Your Virtual Environment
To use this docker setup:
* open up a command prompt/terminal window ad `cd` into this directory.
* type `docker compose create`.  You should see the following output:
```
[+] Running 3/3
 ✔ Network it2055-mongo-conda_default  Created           0.0s
 ✔ Container mongo-it2055              Created           0.1s
 ✔ Container anaconda-it2055           Created           0.0s
 ```
 * In the Docker Dashboard, click "Containers".  You should see `it2055-mongo-conda`.
 * Click the play button to start the mongodb server and Anaconda server.

That's it.  You now have MongoDB and Anaconda and Jupyter all running inside virtual machines on your computer. Congratulations.


# Using Your Virtual Environment

## Connecting MongoDB Compass to the Database
Connecting Compass to the DB is the same as if the DB was running locally.  You can use the following connection string;
```
mongodb://localhost:27017
```

## Launching Jupyter
This Jupyter setup requires a token to log into the server that is running.  This token is printed out at the end of the logs.  This token will be remembered, but you may need to find it in the logs from time to time.  Luckily a link with the token is printed in the Log and you can just click on it through the Docker Dashboard.

 * In Docker Dashboard, under "Containers" expand `it2055-mongo-conda` and click `anaconda-it2055`.
 * Select "Logs".
 * At the end of the log you should see something similar to below.  If you don't, wait a little while, it might not be done starting yet.
```
     To access the notebook, open this file in a browser:
         file:///root/.local/share/jupyter/runtime/nbserver-1105-open.html
     Or copy and paste one of these URLs:
         http://75575090b3e5:8888/?token=adsfasdfasfdasdfasdfasdfasdfasfdadsfadsf
      or http://127.0.0.1:8888/?token=adsfasdfasfdasdfasdfasdfasdfasfdadsfadsf
```
 * You should be able to click on these, like any other link.  Click on the `127.0.0.1` link and it will open a Jupyter in your browser.

 Optionally, you can use your browser to go to `127.0.0.1:8888`.  This will prompt you for a token.  You can copy the token from the output in Log window.  Or you can copy the entire link and paste it.  Once you have logged in once, you should be able to just go to `127.0.0.1:8888`.

 ## Connecting Jupyter to Mongo
 Instead of using `localhost` or `127.0.0.1` we must use the containter name to create a connection to the Mongo container from the Jupyter container.
 ```
 client = pymongo.MongoClient('mongo-it2055', 27017)
 ```

 # Install Packages for Anaconda
 If you need to install packages on your Anaconda server (which you will need to do for class), you must do so on the Anaconda server.  You can use the Terminal in the Docker Dashboard to get access to the server and run your various installs.

 INSERT IMAGE HERE


# Where are my notebooks and other such files?
Once the containers are up and running you will see a `volumes` directory created in this folder.  These directories will continue to exist even if you stop or delete your containers.  You can interact with these directories directly and the results will be visible on the server, and vice versa.