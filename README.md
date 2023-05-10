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
➜  IT2055_Docker-main docker compose create
[+] Running 13/13
 ✔ mongo 9 layers [⣿⣿⣿⣿⣿⣿⣿⣿⣿]      0B/0B      Pulled                                       32.8s
   ✔ f3f60f415e9a Pull complete                                                             2.0s
   ✔ 42c1bc6eb929 Pull complete                                                             2.0s
   ✔ b5af31693439 Pull complete                                                             2.2s
   ✔ 23f5afa97a66 Pull complete                                                             2.3s
   ✔ d05f20747b83 Pull complete                                                             2.4s
   ✔ ab5a4df6de08 Pull complete                                                             2.4s
   ✔ bee7bab4fd17 Pull complete                                                             2.5s
   ✔ 49156abc6ec2 Pull complete                                                            31.4s
   ✔ ddead51c266b Pull complete                                                            31.5s
 ✔ anaconda 2 layers [⣿⣿]      0B/0B      Pulled                                           43.6s
   ✔ ebc3dc5a2d72 Pull complete                                                             6.0s
   ✔ f0855f5a21c9 Pull complete                                                            42.3s
[+] Running 3/3
 ✔ Network it2055-mongo-conda_default  Created                                              0.0s
 ✔ Container anaconda-it2055           Created                                              0.4s
 ✔ Container mongo-it2055              Created                                              0.5s
➜  IT2055_Docker-main
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

<img width="1294" alt="Screenshot 2023-05-09 at 4 33 49 PM" src="https://github.com/ProfButch/IT2055_Docker/assets/109557520/fae409a2-a690-4427-a2a2-1996ddb0e040">


# Where are my notebooks and other such files?
Once the containers are up and running you will see a `volumes` directory created in this folder.  These directories will continue to exist even if you stop or delete your containers.  You can interact with these directories directly and the results will be visible on the server, and vice versa.
