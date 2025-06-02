# EnforceDevSecOps-Compliance
Demo Pipeline of Github Actions with AWS IODC Federation

What we are creating is a simple git workflow that automates the compliance testing of all code and the deployment of the code-base within the main branch. The workshop can be expanded to continue Pull-Requests into additional branches and deploying to other AWS accounts from a single GitHub repository with multiple long running branches.

![image](https://github.com/user-attachments/assets/2e286b35-ba17-4c6a-acc4-b7a243d94afe)

Create a GitHub Repository
In order to avoid complex security settings that would be necessary to keep your Software Development Life Cycle Organization setup and application code separate, we will store the application code in new blank git repository. Prior to starting these steps, make sure you are logged into Github.com.

Create a new repository on GitHub 
Set the repository owner to whatever GitHub organization or personal profile you want to use. Take note of the owner name as we will use this in our OIDC setup.
Add a repository name taking note of the name as you will use this later in our OIDC setup
Give a brief description in the Description text box
Click private so that your repository is not made public for all to see (this is optional but recommended)
Click Add a README file that our repository initializes with a default standard branch
Your page should look similar to the following screenshot. Click Create repository button at bottom once verified.

CI/CD Account Aware Pipeline
In this section we will be setting up the CI/CD AWS account aware pipeline. An account aware pipeline is the setup of having a specific branch map to a specified AWS account (environment).

Here we will setup three GitHub Actions:
Compliance - runs compliance checks on all pushes to the repository
Build - run a build validation on the templates on all pushes to the repository
Deploy - deploys our cloudformation template on push events only on the main branch

Furthermore, after this section - we will:
1. Add in our CloudFormation template we want to deploy
2. Fix any compliances issues in our CloudFormation template
3. Suppress applicable compliance issues in our CloudFormation template
4. Merge our code to main branch to deploy in our AWS account


Git Workflow Summary

1. Push to GitHub repo new feature branch
2. GitHub Action - Build Validation
3. aws cli cloudformation validation
4. Report back to GitHub Actions
5. GitHub - Compliance
6. Run a Guard Rule Set
7. Skips any suppressed rules
8. Reports status back to GitHub Actions page
9. Pull-Request with review and approval to merge
10. GitHub Action - Deploy
11. Runs only on main branch
12. Leverages temporary token via IdP setup
13. Deploys CloudFormation to AWS Account


