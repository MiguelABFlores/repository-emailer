# Pull Request Summarizer to Email

Project to retrieve from the GitHub API the data needed to summarize the pull requests from a public repository, after data has been retrieved it will generate a report and send it to the email of a scrum master.

# Task Instructions

Using the language of your choice, write code that will use the GitHub API to retrieve a summary of all opened, closed, and in progress pull requests in the last week for a given repository and print an email summary report that might be sent to a manager or Scrum-master. Choose any public target GitHub repository you like that has had at least 3 pull requests in the last week. Format the content email as you see fit, with the goal to allow the reader to easily digest the events of the past week. Please print to console the details of the email you would send (From, To, Subject, Body). As part of the submission, you are welcome to create a Dockerfile to build an image that will run the program, however, other ways of implementing this is acceptable.

Definition of Done:

- [x] Your code demonstrates use of variables, looping structures, and control structures

- [x] Your code prints a user-friendly summary of open, merged, and closed pull requests including counts of PRs as well as their titles. Use your judgement on what you think is important information.

- [x] Your code is able to be run/compiled without errors

- [x] Your code should be configurable when it runs. Use your judgement on what needs to be configurable.

- [x] Your solution describes how this would be run to produce regular reports.

# Files and Folder Structure Explanation

1. **`/github-pr-summary/main.py`**: The main script that coordinates fetching the pull requests and formatting the email body for the project.
2. **`/github-pr-summary/github_api.py`**: Contains the function to fetch the pull requests from the GitHub API.
3. **`/github-pr-summary/email_console_formatter.py`**: Contains the function to format the pull request data into an email body that will be printed into console.
4. **`/github-pr-summary/html_formatter.py`**: Formats the pull request data into an HTML body.
5. **`/github-pr-summary/html_generator.py`**: Generates the HTML report and saves it to a file.
6. **`/github-pr-summary/config.py`**: Holds configuration values: repository owner, repository name, email details, etc.
7. **`Dockerfile`**: File used to create the Docker image, it includes everything needed to setting up the Python environment and running the main script.
8. **`requirements.txt`**: Here are the Python libraries that need to be installed in the Docker image.

# Diagrams for Strategy and Code Structure

## Strategy Diagram

![Strategy Diagram](diagrams/repository-emailer-strategy.drawio.png)

## Code Structure Diagram

![Code Structure Diagram](diagrams/repository-emailer.drawio.png)

# Prerequisites

- Docker or Rancher installed on your machine.

or

- Python 3.12

### Steps Docker

1. **Clone the repository:**

   ```bash
   git clone https://github.com/MiguelABFlores/repository-emailer.git
   cd github-pr-summary
   ```

2. **Build the Docker image:**

   ```bash
   docker build -t github-pr-summary .
   ```

3. **Run the Docker container:**

   ```bash
   docker run --rm github-pr-summary
   ```

4. **Run the Docker container with environment variables:**

   ```bash
   docker run --rm -e REPO_OWNER=someowner -e REPO_NAME=repositoryname -e EMAIL_FROM=someonesemailfrom@example.com -e EMAIL_TO=someonesemailto@example.com -e EMAIL_SUBJECT="Some Public Repository Weekly PR Summary" github-pr-summary
   ```

### Steps Python

1. **Clone the repository:**

   ```bash
   git clone https://github.com/MiguelABFlores/repository-emailer.git
   cd github-pr-summary
   ```

2. **Install Python dependencies:**

   ```bash
   pip3 install PyGithub requests
   ```

   or

   ```bash
   brew install python-requests
   ```

3. **Run the main python script:**

   ```bash
   python3 github-pr-summary/main.py
   ```

# Summary Report

If done the steps correctly you should get an output in the console with relevant information of the repository about pull requests.
There will be a generated file named "github-pr-summary.html" inside the report folder. You can open the file to read a html generated, it is easier to read and more human friendly. But to open it easily my suggestion is to run with the python interpreter not containerizing it.

# Scheduling

## Scheduling with a Cronjob

**Edit the crontab**

```bash
 crontab -e
```

**Create a cronjob in the terminal and add the docker run to the instruction**

```bash
0 0 * * * docker run --rm github-pr-summary
```

or

```bash
0 0 * * * docker run --rm -e REPO_OWNER=someowner -e REPO_NAME=repositoryname -e EMAIL_FROM=someonesemailfrom@example.com -e EMAIL_TO=someonesemailto@example.com -e EMAIL_SUBJECT="Some Public Repository Weekly PR Summary" github-pr-summary
```

## Scheduling in Kubernetes

**Create a Kubernetes secret for your Artifactory credentials:**

```bash
kubectl create secret docker-registry artifactory-secret \
  --docker-server=artifactory.somedns.com \
  --docker-username=<artifactory-username> \
  --docker-password=<artifactory-password> \
  --docker-email=<email>
```

**Apply the CronJob to your Kubernetes cluster:**

```bash
kubectl apply -f scheduling/github-pr-summary-cronjob.yaml
```

# Python Requirements

Dependencies needed:

- requests

  ```bash
  pip3 install PyGithub requests
  ```

  or

  ```bash
  brew install python-requests
  ```

# Sources

- [using-github-api-in-python](https://thepythoncode.com/article/using-github-api-in-python)
- [Isoformat() Method Of Datetime Class In Python](https://www.geeksforgeeks.org/isoformat-method-of-datetime-class-in-python/)
- [Python DateTime – Timedelta Class](https://www.geeksforgeeks.org/python-datetime-timedelta-class/?ref=lbp)
- [GitHub API Docs](https://docs.github.com/en/rest/pulls?apiVersion=2022-11-28)
- [GitHub API Docs PR](https://docs.github.com/en/rest/pulls/pulls?apiVersion=2022-11-28#list-pull-requests)
