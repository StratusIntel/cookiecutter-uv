# Tutorial

This page contains a complete tutorial on how to create your project.

## Step 1: Install uv

To start, we will need to install uv. The full instructions to install uv can be found [here](https://astral.sh/uv/) - but here's the quick guide: 

- For MacOS, I recommend using Homebrew (`brew install uv`), or you can use the Linux command.
- For Linux, use:

```sh
curl -LsSf https://astral.sh/uv/install.sh | sh
```

- For Windows:
```sh
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

## Step 2: Generate your project

Make sure this repository is synced with the latest changes to `fpgmaas`'s main branch. Then, on your local machine, navigate to the directory in which you want to create a project directory, and run the following command:

```sh
uvx cookiecutter https://github.com/StratusIntel/cookiecutter-uv.git
```

Alternatively you can use the base version.
```sh
uvx cookiecutter https://github.com/fpgmaas/cookiecutter-uv.git
```

I suggest using the following parameters when prompted:
- author: your full name
- email: your work email address
- author_github_handle: your github handle
- project_name: a project name you will be using in github (only alphanumeric characters and optionally `-`)
- project_slug: ` ` (leave blank)
- project_description: one sentence describing your project
- layout: `src` (src is recommended for modern development)
- include_github_actions: `y`
- publish_to_pypi: `n`
- deptry: `y`
- mkdocs: `n` (unless you want to make lots of documentation, then `y`)
- codecov: `n`
- dockerfile: `n`
- devcontainer: `n`
- open_source_license: `6` / `"not open source"`

For an explanation of the prompt arguments, see [Prompt Arguments](docs/prompt_arguments.md).

## Step 3: Set up your Github repository

Create an empty new repository on Github. Give it a name that only contains alphanumeric characters and optionally `-`. **DO NOT** check any boxes under the option "Initialize this repository with."

## Step 4: Upload your project to Github

Run the following commands, replacing `<project_name>` with the name that you also gave the Github repository and `<github_author_handle>` with your Github username.

```sh
cd <project_name>
git init -b main
git add .
git commit -m "Init commit"
git remote add origin git@github.com:<github_author_handle>/<project_name>.git
git push -u origin main
```

## Step 5: Set Up Your Development Environment

Initially, the CI/CD pipeline will fail for two reasons:

1. The project does not yet contain a `uv.lock` file
2. There are a few formatting issues in the project

To fix that, we first install the environment and the pre-commit hooks with:

```sh
make install
```

This will generate the `uv.lock` file.

## Step 6: Run the pre-commit hooks

Now, to resolve the formatting issues, let's run the pre-commit hooks:

```sh
uv run pre-commit run -a
```

## Step 7: Commit the changes

Now we commit the changes made by the two steps above to the repository:

```sh
git add .
git commit -m 'Fix formatting issues'
git push origin main
```

## Step 8: You're all set!

That's it! I hope this repository saved you a lot of manual configuration. If you have any improvement suggestions, feel free to raise an issue or open a PR on Github! 

This Stratus Intel repo is our own copy of the cookiecutter-uv template, that we can adjust to our liking.

--- 
 <br>

## Optional Steps

### Optional step 1: Enable your documentation

To enable your documentation on GitHub, first navigate to **Settings > Actions > General** in your repository, and under **Workflow permissions** select **Read and write permissions**.

## Optional step 2: Create a new release

To trigger a new release, navigate to your repository on GitHub, click **Releases** on the right, and then select **Draft a new release**. If you fail to find the button, you could also directly visit:

```
https://github.com/<username>/<repository-name>/releases/new
```

Give your release a title, and add a new tag in the form `*.*.*` where the *'s are alphanumeric. To finish, press **Publish release**.

## Optional step 3: Enable your documentation (continued)

Then navigate to **Settings > Code and Automation > Pages**. If you successfully created a new release, you should see a notification saying:

```
Your site is ready to be published at https://<author_github_handle>.github.io/<project_name>/.
```

To finalize deploying your documentation, under **Source**, select the branch `gh-pages`.

