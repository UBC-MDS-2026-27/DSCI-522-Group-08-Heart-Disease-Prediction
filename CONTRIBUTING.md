## Contributing to DSCI-522-Group-08

Thank you for your interest in our project! We welcome feedback, suggestions, and contributions that could help us improve our work.

If you would like to contribute, please follow the guidelines below.

## Reporting Bugs

If you notice a problem with our code, data analysis, or documentation, please open a GitHub Issue.

When reporting a problem, please:

- Give the issue a clear title.

- Explain what the problem is.

- Describe how we can reproduce it, if possible.

- Include any error messages or screenshots that might help.

## Working in the container

We edit and run the code inside the container, by connecting Positron to it over ssh. Your project folder is shared with the container at /workspace, so a file you change there changes on your computer too.

Once, before your first connection
Install Positron on your computer. Its Remote SSH feature, which connects to the container, comes built in, so you don't need to install an extension.
Make sure you followed the Usage section of the README: you have an ssh key at ~/.ssh/id_ed25519.pub and you ran docker compose pull.
Check that Git knows who you are on your computer:
git config --global user.email

It should print the email of your GitHub account. If it prints nothing, set your name and email:

git config --global user.name "Your Name"
git config --global user.email "you@example.com"

docker-compose.yml shares your ~/.gitconfig with the container, so the commits you make there count as yours.

Each time you work on the project
In a terminal, in the root of this repository, start the container in the background:
docker compose up -d

docker compose ps should list analysis-env as running. 2. In Positron, open the Command Palette (Cmd+Shift+P on Mac, Ctrl+Shift+P on Windows). 3. Type and run Remote SSH: Show Remote Menu, then pick Connect to Host. 4. Type root@localhost:2222 and press Enter. A new Positron window opens.

If it asks for the platform of the remote host, pick Linux.
If it asks whether you trust the host (a "fingerprint"), click Continue.
The first time, Positron installs its server inside the container. This takes a few minutes.
Open the project folder. The bottom left corner now shows SSH: localhost:2222, but the Explorer says No folder opened and the terminal starts in /root, which has no project files. That is normal.
Click Open Folder in the Explorer.
Delete what is in the path box at the top of the window, type /workspace, and click "OK" (you may need to click "OK" a few times before this works).
The window reloads, and the Explorer shows WORKSPACE [SSH: LOCALHOST:2222] with the project files.
Pick the Python interpreter (check this every time).
Click the interpreter button at the top right of the window. The Running Interpreter Sessions menu only lists sessions that are already running (such as /usr/bin/python3, the container's system Python: not this one).
Click New Console Session... and pick Python 3.x (uv: <your-project-name>), with the path /opt/venv/bin/python. This is the environment built from uv.lock.
If it isn't in the list, run Python: Select Interpreter from the Command Palette, choose Enter interpreter path... and type /opt/venv/bin/python.
Don't pick /workspace/.venv: that is an environment from your own computer, and it doesn't run in the container.
To check, run import sys; print(sys.executable) in the Console. It should print /opt/venv/bin/python. (Positron may also open an R console. Python code gives syntax errors there, so use the Python console.)
Work as usual. The Terminal, the Console and the Render button all run inside the container.
When you are done, close the Positron window, then stop and remove the container in a terminal on your computer:
docker compose down
If it doesn't connect
~/.ssh/id_ed25519.pub is a folder: Docker made it because the key didn't exist yet. Run docker compose down, delete that folder, make the key (see the README), and start again.
~/.gitconfig is a folder, or Git in the container doesn't know your name: the same thing happened with your Git settings. Run docker compose down, delete that folder, set your name and email (see above), and start again.
It asks for a password: the container can't see your key. Check that your key is named id_ed25519.pub, or change the key path in docker-compose.yml.
"Remote host identification has changed": you are using a new image. Run ssh-keygen -R "[localhost]:2222", then connect again.
GitHub asks you to sign in when you push from the container: sign in once in the browser window Positron opens. Positron remembers it.
Linux laptops: ssh refuses the key because the file belongs to you, not root. Remove the # from the StrictModes no line in the Dockerfile and push, so the workflow publishes a fixed image.
Port 2222 is already in use: change the first 2222 in docker-compose.yml to another number (e.g. 2223), and connect to that port instead.

More detail: Working in a container over ssh with Positron.

To re-run the analysis and render the report without opening the container:

docker compose run --rm analysis-env uv run quarto render

## Adding or updating a package

On a new branch, add the package with uv add <package>==<version> (this pins the version in pyproject.toml and updates uv.lock), then commit the changed pyproject.toml and uv.lock together and push them. GitHub Actions then builds and publishes a new image on Docker Hub, and commits the new sha- tag to the image: line of docker-compose.yml on your branch. When the workflow finishes, get that commit and download the new image:

git pull
docker compose pull

Then merge the branch into main in a pull request. After the merge, wait for the workflow on main to finish, then run git pull and docker compose pull again.

## Publishing the report

The report on GitHub Pages is a copy of the rendered report in docs/index.html. Each time you re-render the report, copy it there again, commit and push:

cp <path-to-your-report>.html docs/index.html

## Pull request process
Create a new Git branch for each pull request (PR), starting from an up-to-date main. Do not commit directly to main.
Give the branch a short name that describes the work, for example fix-readme-typo or fix-eda-graphs.
Keep each branch small: one independent piece of work per branch.
Before opening the PR, render the report in the container (docker compose run --rm analysis-env uv run quarto render) to check that the analysis still runs from start to finish.
Open a PR into main and describe what changed and why. Link the related issue (e.g., "Closes #12").
At least one other team member must review and approve the PR before it is merged. The reviewer, not the author, merges it.
New code should follow the PEP8 style guide.

## Suggesting Changes

If you have an idea to improve our project, please open a GitHub Issue and explain your suggestion.

Our team would like to discuss proposed changes before someone starts working on them.

For small spelling or grammar corrections, please edit the original source file rather than a generated HTML or PDF file.

## Reviewing Pull Requests

At least one team member should review each Pull Request before it is merged.

If changes are needed, the reviewer can leave comments or suggestions. We encourage everyone to communicate respectfully and be open to feedback.

The project team is responsible for approving and merging contributions.


## Use of AI

Contributors may use AI tools, such as ChatGPT, Claude, or GitHub Copilot, to help understand concepts, troubleshoot errors, and check their work, as long as this follows the [DSCI 522-course rules](https://ubc-mds.github.io/DSCI_522_dsci-workflows_students/assignments/milestone1.html#expectations).

If you use AI, please:

- Make sure you understand the code or text you submit.

- Check that the information and suggestions are correct.

- Explain how you used AI in your contribution.

- Take responsibility for your final work.

GitHub Issues and Pull Requests must be created by people, not AI agents. Team members are also responsible for reviewing and merging Pull Requests.

AI can help us with our work, but it should not replace our own understanding or decisions.

## Code of Conduct

Please follow our [Code of Conduct](CODE_OF_CONDUCT.md) when contributing to this project.

We want everyone to feel welcome, respected, and comfortable sharing their ideas.
