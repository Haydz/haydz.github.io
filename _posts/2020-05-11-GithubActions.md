---
layout: posts
title: "GitHub Actions"
---

I participated in a DevSecOps type workshop on Saturday (May 9th) in which we created some GitHub Actions. This is a post to solidify the learning and be a cheat sheet.

# What Training?
Again [DC416](https://twitter.com/defcon_toronto) hosted an online workshop. It was run by [Tanya](https://twitter.com/shehackspurple).

It was titled "DC416 DevSecOps Workshop with GitHub Actions and Azure".
![](/images/dc416devops/image_1.png)

I learned a bit and had fun. 

## What did we do?
Add a pipeline to our process to deploy code from GitHub to a web-app on Azure and use various security tooling within the pipeline

### Credential/Secret Scanning
- TruffleHog tool by Hashicorp
- Scan for passwords, keys, certs, etc
- Other Tools: Gitty Leaks, Cred Scan, etc

It was pretty cool.

Anyhow. To the Cheat sheet on GitHub actions.


# What is a GitHub Action
[Definition](https://github.com/features/actions):
> GitHub Actions makes it easy to automate all your software workflows, now with world-class CI/CD. Build, test, and deploy your code right from GitHub. Make code reviews, branch management, and issue triaging work the way you want.

For me, this means that any time I commit code I can have it check that my work email is not in my code. Why my email? Because if I have my work email hard-coded in a script, it probably means I have my work password hard-coded as well. Which is.... really bad

## Tutorial to help
The first tutorial I followed was [Hello World](https://lab.github.com/githubtraining/github-actions:-hello-world)
![](/images/dc416devops/image_2.png)


# GitHub Actions
There are many GitHub Actions people have created. You can find them on the marketplace.

Search for them like so:
![](/images/dc416devops/image_2.png)


## Flow of a GitHub Action
So a GitHub action actually ties into a workflow. 

Custom workflows are automatic processes that are setup in a GitHub repo. So you would have a workflow that executes a GitHub Action.

From the [documentation](https://help.github.com/en/actions/configuring-and-managing-workflows/configuring-a-workflow)
> Workflows must have at least one job, and jobs contain a set of steps that perform individual tasks. Steps can run commands or use an action. You can create your own actions or use actions shared by the GitHub community and customize them as needed.

# The example to walk-through:
1. Create a directory at the root named `.github/workflows`
2. Create a YAML file in the above directory with instructions on the workflow. - In our example we are going to use Trufflehog
3. Commit the changes

Note: in #2 the example will be to execute a search for the work email (Trufflehog) on a commit/push to GitHub.


## 1 - Create the directory
Simply create the directory within the GitHub Repo:
`.github/workflows`
![](/images/dc416devops/image_4.png)

## 2 - Create the YAML file:  
The .yml file needs to be created within the `workflows` directory.
![](/images/dc416devops/image_5.png)

# Layout of Yaml file:
Again, in the [documentation](https://help.github.com/en/actions/configuring-and-managing-workflows/configuring-a-workflow) there is an example workflow file.

```yaml
name: Greet Everyone
# This workflow is triggered on pushes to the repository.
on: [push]

jobs:
  build:
    # Job name is Greeting
    name: Greeting
    # This job runs on Linux
    runs-on: ubuntu-latest
    steps:
      # This step uses GitHub's hello-world-javascript-action: https://github.com/actions/hello-world-javascript-action
      - name: Hello world
        uses: actions/hello-world-javascript-action@v1
        with:
          who-to-greet: 'Mona the Octocat'
        id: hello
      # This step prints an output (time) from the previous step's action.
      - name: Echo the greeting's time
        run: echo 'The time was ${{ steps.hello.outputs.time }}.'
```
The example shows:
* that the GitHub action will execute on a push (also a commit)
* the name of the job is greeting
* It will run on Ubuntu
* steps it will run once up. This includes a name of the action, the action its running (we will use Trufflehog)

We will come back to this after we find the TruffleHog GitHub action.

## 2.5 TruffleHog
Looking for TruffleHog I found 2 types. One is based off the original but does not allow configuration changes.


![](/images/dc416devops/image_3.png)


For this example we will use [Trufflehog Actions Scan](https://github.com/marketplace/actions/trufflehog-actions-scan)

This GitHub action allows basic configuration
![](/images/dc416devops/image_6.png)

As well as custom configuration.
![](/images/dc416devops/image_7.png)

Within the custom Arguments configuration, we can see the `--rules` line with a `regexes.json` file. - This will be the file we edit to add a custom rule to look for a work email.


### Editing the Yaml File
Here we can add TruffleHog as it is without customization. To do this, follow the below:

Back to the GitHub repo where the yaml file was created. We need to add a job to execute the GitHub action.

The link for my YAML file location is:
https://github.com/Haydz/jirapull/blob/master/.github/workflows/main.yml

Edit your YAML file to like so:


```yaml

name: A workflow for ensuring credentials are not in file
on: push
jobs:
  build:
    name: Cred Checker
    runs-on: ubuntu-latest
    steps:        
       - uses: actions/checkout@master
       - name:  trufflehog-actions-scan
         uses: edplato/trufflehog-actions-scan
         
```
The above file takes the following parts from the example workflow file and the Trufflehog documentation:
* executing on a commit  
* the job to run
* running on bunutu
* the  basic steps from trufflehog

If this is commited in GitHub, it should start off the Trufflehog GitHub Action.

You can look in the actions section:
https://github.com/Haydz/jirapull/actions
![](/images/dc416devops/image_12.png)

If you click into it, it will look something like the following, but will most likely pass as your code probably does not have any secrets in it:
![](/images/dc416devops/image_13.png)

So this is an example of having Trufflehog running. 



The steps to customize Trufflehog to look for an email address are below:

# Customizing Trufflehog
Just like any GitHub repo that requires customization, forking the repo is needed.

Find the repo by clicking on use latest version:
![](/images/dc416devops/image_8.png)

Then clicking the learn more here link. Which takes us to the correct [repo](https://github.com/edplato/trufflehog-actions-scan).

To be able to edit it, we need to fork it:
![](/images/dc416devops/image_9.png)

My URL location ends up being the following, yours will be similar but with your GitHub username.
https://github.com/Haydz/trufflehog-actions-scan

## Looking into regexes.json
There was a rules file listed in the instructions. So its best to look at that.

![](/images/dc416devops/image_20.png)

In short, it is a list of regex rules that will the action will alert on:
![](/images/dc416devops/image_10.png)



Edit this with your work email, or a secret you want to find.
My example is anything with a `name.lastname@fakemail.com` format:
`  "Work email": "\\w*\\.\\w*@fakemail\\.com"`
![](/images/dc416devops/image_11.png)

This will allow Trufflehog to use the rules list and search based on the regex.

## Editing the YAML file to run the forked version 

Editing the forked versions regex rules is great. But if the YAML is configured correctly, it will still run the Trufflehog version found at "edplato/trufflehog-actions-scan" 

So the YAML file should be edited for the forked version like so:  
![](/images/dc416devops/image_14.png)

Focusing on:
* using the trufflehog that was forked
* adding the rules file

The complete file will look like:

```yaml
name: A workflow for ensuring credentials are not in file
on: push
jobs:
  build:
    name: Cred Checker
    runs-on: ubuntu-latest
    steps:        
       - uses: actions/checkout@master
       - name: Haydn trufflehog-actions-scan
         uses: haydz/trufflehog-actions-scan@master
         with:
           scanArguments: "--regex --max_depth=10  --rules /regexes.json"
           
```
My Yaml can be found [here](https://github.com/Haydz/jirapull/blob/master/.github/workflows/main.yml)



### Conducting a test
So it appears everything is in order.

We should create a file with the email address in it, and commit the file to test if the regex is working correctly.

The example here is a file called `testemail` with the contents:
* bob.jane@fakemail.com

![](/images/dc416devops/image_15.png)

Once this is commited, the Github Action will run. 
Commit the file:
![](/images/dc416devops/image_16.png)

Then go to the Actions Section, and it should be running:
![](/images/dc416devops/image_17.png)

It runs and errors:
![](/images/dc416devops/image_18.png)

Looking within the Trufflehog scan results, it successfully detected the email address:
![](/images/dc416devops/image_19.png)


Success!

