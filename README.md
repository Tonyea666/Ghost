Ghost Docker Project

I started this project with the goal of setting up a Ghost blog platform using Docker and MySQL to manage the database, orchestrated with Docker Compose. The idea was to get both services running and properly connected for a functional blog platform.

How I Started:
I created a Docker Compose file with two main services:

Ghost (the blog platform)
MySQL (to store the blog's data)
The configuration included environment variables to link the two services. The basic setup was as follows:

Ghost Container:

It was configured to connect to MySQL using ghost_user and newpassword for authentication.
Ghost was supposed to be accessible at http://localhost:2368.
MySQL Container:

The MySQL container was set up with a root password (YourStrongPassword).
A ghost database was created, and the user ghost_user was granted permissions to connect to it from the Ghost container.
The containers were intended to communicate via Docker's internal network and to persist their data in Docker volumes (ghost-docker_db_data and ghost-docker_ghost_content).

What Went Wrong:
Despite the initial setup looking good, I ran into several issues that prevented the containers from working together:

Database Connection Failures: Ghost was continuously trying to connect to the database, but it failed every time with the error connect ECONNREFUSED 127.0.0.1:3306. Ghost was trying to connect to MySQL using localhost, but the MySQL container was actually running separately as ghost_db. Even though I set the correct host in the Docker Compose file, the containers weren't linking properly, which caused the connection issue.

Container Linking Issues: The Ghost container failed to start multiple times, exiting with errors, mainly related to the database connection. I attempted to resolve these by reconfiguring the setup, but the issue persisted.

Port and Networking Configuration: Even though I configured MySQL's port correctly and set Ghost to run on localhost:2368, there were problems with the networking setup. The Ghost container couldn't access the MySQL container properly, which blocked the connection.

How It Ended:
After many attempts to restart, reconfigure, and rebuild the containers, the issue was still unresolved. Despite modifying the Docker Compose file and ensuring the database credentials were correct, Ghost was unable to connect to MySQL. Even after pulling the latest repository changes and trying from scratch with fresh containers, the ECONNREFUSED error kept showing up.

At the end, while MySQL was running fine, the Ghost container continued to fail on startup because it couldn't establish a connection with MySQL.

In conclusion, I couldn't get the Ghost blog platform running with Docker and MySQL due to persistent networking and database connection issues. Despite repeated efforts to fix the setup, Ghost couldn't connect to the database. Moving forward, I would need to review the networking setup more carefully and double-check the configuration in the Docker Compose file for potential misconfigurations.

