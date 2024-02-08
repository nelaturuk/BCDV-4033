# Create a First Job

- Build - Execute Shell option 

```
    cd /etc
    ls -l
```

# Builds Examples

- Create Job to echo hello. 
```
echo "hello" >> Message.txt
cd /var/lib/jenkins 
ls
cd workspace

// If you dont have any jobs this will be empty

```

- Add a job that triggers previous job
```
echo "The current build no is $BUILD_NUMBER" >> Info // Choose env variable

```

**Lab 2 - Install Jenkins, create a Job that is triggered by another Job and that creates a txt file with the Job Name and Build Number in the txt file**

# SCM on Jenkins

- Create a new JOB to integrate SCM to Git. 
- Add build step to echo. 
- Show build updates.
- Automatically update build by adding webhook.
- SocketXp to expose

```
socketxp connect http://<local>:8080

```

**Lab 2 - Connect your Lab 1 GitHub repo as a Webhook to Jenkins. Create a Job that will build your project whenever there is a commit on the repo.**

# Testing in Jenkins

- Install Node JS and Jest plugin using Jenkins. 
- Create JOb using Jenkins Pipeline file for testing Lab 1 repo project
- There should be two stages: Build and test in this pipeline.

**Lab 2 - Test your Lab 1 Repo  by adding Job for testing in Jenkins.**

# Notification in Jenkins

- Enable email notification. 
- Enable app passwords for Google. 
- Fail a job

```
cd /nofolder
```

**Lab 2 - Create a new notification job that will send email to GMAIl whenever your build fails.**

# Plugins in Jenkins

- Install and Manage plugins. 
- Uninstall ANT plugin and reinstall it. 
- Install monitoring plugin. 



# Auditing and Credentials

- Global configuration. 
- Disable remember password. 
- Security Realm options. 
- Authorization options. 
- Using Security Matix by adding new user. 

**Lab 2 - Create non-admin user in your local jenkins environment and assign the user permissions to create job.**

# Artifacts Demo

```
touch testarchive
tar -czvf archive01.tar.gz testarchive

// Post-build

```

**Lab 2 - Create a artifact for Lab 1 build folder in Jenkins by using post-build task.**

# Parameters

**Lab 2 - Create a parameter for your job (any type). Execute a batch script to display the parameter value**
