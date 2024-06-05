# repository-emailer

Project to retrieve from the GitHub API the data needed to summarize the pull requests from a public repository, after data has been retrieved it will generate a report and send it to the email of a scrum master.

# Instructions

Using the language of your choice, write code that will use the GitHub API to retrieve a summary of all opened, closed, and in progress pull requests in the last week for a given repository and print an email summary report that might be sent to a manager or Scrum-master. Choose any public target GitHub repository you like that has had at least 3 pull requests in the last week. Format the content email as you see fit, with the goal to allow the reader to easily digest the events of the past week. Please print to console the details of the email you would send (From, To, Subject, Body). As part of the submission, you are welcome to create a Dockerfile to build an image that will run the program, however, other ways of implementing this is acceptable.

Definition of Done:

- [ ] Your code demonstrates use of variables, looping structures, and control structures

- [ ] Your code prints a user-friendly summary of open, merged, and closed pull requests including counts of PRs as well as their titles. Use your judgement on what you think is important information.

- [ ] Your code is able to be run/compiled without errors

- [ ] Your code should be configurable when it runs. Use your judgement on what needs to be configurable.

- [ ] Your solution describes how this would be run to produce regular reports.

# Requirements

Dependencies needed:

- requests
  ```
  pip3 install PyGithub requests
  ```

# Sources

- [using-github-api-in-python](https://thepythoncode.com/article/using-github-api-in-python)
- [Isoformat() Method Of Datetime Class In Python](https://www.geeksforgeeks.org/isoformat-method-of-datetime-class-in-python/)
- [Python DateTime – Timedelta Class](https://www.geeksforgeeks.org/python-datetime-timedelta-class/?ref=lbp)
- [GitHub API Docs](https://docs.github.com/en/rest/pulls?apiVersion=2022-11-28)
- [GitHub API Docs PR](https://docs.github.com/en/rest/pulls/pulls?apiVersion=2022-11-28#list-pull-requests)
