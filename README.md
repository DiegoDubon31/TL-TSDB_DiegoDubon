
---
# Creating a GitHub Action

I created a GitHub Action that triggers when a pull request is opened targeting the main branch. The GitHub Action prints two messages in the console: one with an environment variable, and another with an environment secret. 

Here is the result:  
![GitHubAction](https://i.postimg.cc/3wJVWKWJ/PR-7.png)

But how did I do that?  
Here is a quick guide to help you create your GitHub Action.

1. **Create your variable and secret:**
   Go to your repository’s **Settings**.  
   Here’s where to go:  
   ![Settings](https://i.postimg.cc/xdx7zWbG/PR-P1.png)

2. **Navigate to Secrets and Variables:**
   Go to **Secrets and variables**, then go to **Actions**.  
   ![Secrets&Variables](https://i.postimg.cc/h4zF9PsX/PR-2.png)

3. **Create a secret:**
   At the top, select **Secrets** and click on the green button to create a new secret.  
   ![Create_secret](https://i.postimg.cc/PrYBR3Bh/PR-3.png)

4. **Create a variable:**
   Now do the same for variables.  
   ![Create_var](https://i.postimg.cc/T3xZMj6b/PR-4.png)

5. **Create and edit a GitHub Action:**
   Now that you have created your secret and variable, go to the **Actions** tab in your repository, create a new workflow file (`.yml`), and edit it. Here is an example of what mine looks like:

```yaml
# This is a basic workflow to help you get started with Actions

name: Pull Request Opened Workflow

# Controls when the workflow will run
on:
  # Triggers the workflow on pull request events but only for the "main" branch
  pull_request:
    branches: [ "main" ]

# Allows you to run this workflow manually from the Actions tab
workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    env:
      pswd: ${{ secrets.MY_PSWRD }}
      nm: ${{ vars.MY_NAME }}
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v4

      # Runs a single command using the runner's shell
      - name: "Print environment variable"
        run: echo "Environment Variable: ${{ env.nm }}"

      # Runs a single command using the runner's shell
      - name: "Print secret variable"
        run: echo "Secret: ${{ env.pswd }}"
```

Basically, what I did was create an environment for my secret and variable, set the trigger for when a pull request targets the main branch, and display my variable and secret in the console, as you can see at the top.

After you add, commit, and push these changes to your repository, every time you create a pull request targeting the main branch, you will see your variable and secret. 

**DISCLAIMER:** You won’t be able to see your secret; it will be masked because, as the name suggests, it is a secret. This information is kept secure and hidden, displaying only three stars "***" as shown here:  
![PR-7-1.png](https://i.postimg.cc/QxCqBHJz/PR-7-1.png)

---