rying the Interpreter
Talk to us

Python scripts are simple (UTF-8) text files. You could write or edit one with any text editor. You don't compile them.

How are you going to execute them?

Answer: With a Python interpreter.
Prerequisites

You should already have a cloned copy of the workshop's code repository available in the in-browser environment. If not, use the following command to clone the correct sample code repository:

git clone --branch main https://github.com/CiscoDevNet/dne-devfun-code.git

Execute in terminal
Python Virtual Environments

Virtual environments are an elegant way to unclutter your global Python environment and isolate projects from each other. At first, they might sound somewhat mysterious, but they are conceptually simple.

When you create a virtual environment, the virtual environment module venv creates a new folder using the name you provide.

Using Python virtual environments is best practice, so how about getting some practice here. The syntax for the venv command in Python 3 is python -m venv <virtual environment name>.

First, take a look at what is installed in the in-browser environment already:

pip freeze

Execute in terminal
Click to see the currently installed library list

    Note: pip is Python's package-management system used to install and manage software packages.

Now let's create our own virtual environment:

cd ~/src/dne-devfun-code

python -m venv venv

Execute in terminal

You won't see anything in return, but if you list the directory contents, you'll see a new venv folder listed:

ls

Execute in terminal

Now you can go ahead and activate your Python virtual environment in the in-browser terminal.

Note: You want to activate your virtual environment before "pip installing" any packages or running any scripts in general. You want to activate your virtual environment any time you open a new terminal, as virtual environment activation does not persist when a terminal session is closed.
Activate Your Virtual Environment

Run one of the following commands (depending upon your platform) to activate your virtual environment.

In the in-browser environment, which is Linux, and in macOS, run:

source venv/bin/activate

Execute in terminal
Sample Output

Windows: (Use this command if you are trying this in your own Windows environment in a Git Bash window.)

source venv/Scripts/activate

    You can always tell when you are working in an activated virtual environment. The activation script prefixes your command prompt with the name of your activated virtual environment (in parentheses).

What did that action do really? Well, let's take a look at the output of pip freeze again:

pip freeze

Execute in terminal

(venv) developer:dne-devfun-code > pip freeze
(venv) developer:dne-devfun-code > 

Wow, all clear. Now you can install what you want and know exactly what's installed.

Let's try it out.

python -m pip install --upgrade pip

pip install requests

Execute in terminal

    Note: The command python -m pip install --upgrade pip avoids the version Warning you often see such as WARNING: You are using pip version 20.2.3; however, version 21.0.1 is available. This means that pip has recently upgraded. You can safely ignore this message in this environment. If you are working locally you may want to upgrade using that python -m pip install --upgrade pip command.

Now verify that our package installed successfully.

pip list

Execute in terminal

The pip list format shows the package and version in a tabular format like so:

Package            Version
------------------ ---------
certifi            2021.10.8
charset-normalizer 2.0.12
idna               3.3
pip                22.0.4
requests           2.27.1
setuptools         57.4.0
urllib3            1.26.9

Or you can get the list in another format:

pip freeze

Execute in terminal
Verify your Interpreter

If there is ever any confusion about which interpreter you are using, there are couple of commands that can help you out:

which python

Execute in terminal

Gives you the full path to the interpreter.
Sample Output

python -V

Execute in terminal
Sample Output

Without virtual environments, when you use the Python Package Installer (pip install) command to install packages on your workstation, all of those packages (and their dependencies) get installed "globally." Over time this can clutter up your global Python environment, and eventually you run into version conflicts where Project A needs version X.X of a particular package and Project B needs Y.Y.

When you create a virtual environment (like you did with the python -m venv <virtual environment name> command), the virtual environment module venv creates a new folder using the name you provided. Looking inside that folder, you will see something like the following:

venv
├── bin
├── include
├── lib
├── lib64 -> lib
└── pyvenv.cfg

Now, when working inside an activated virtual environment and you pip install some library, where do you think that gets installed?

That's right! ...in the /lib directory.

What about if you pip install some executable script?

Also correct! ...in the /bin directory.

You see, a virtual environment is essentially redirecting where packages get installed and where Python looks to find them. Instead of installing packages in the global environment, they are instead installed in the virtual environment directory that you told venv to create.

You can create these virtual environments in the same directory as your project files (though you usually exclude them from version control), and then everything stays nice and neat. When you go to work on a project, you can simply activate its virtual environment and you have all the packages you need to work on that project. When you want to switch from working on Project A to working on Project B, you deactivate Project A's virtual environment and then activate Project B's.

    Note: Use the deactivate command to exit out of an active virtual environment.

When you are done with a Project and perhaps delete it from your workstation, the virtual environment directory and the packages installed in are also deleted. No more cluttering up directories with unneeded files.

Also, no matter how many Python interpreters you have installed on your workstation - when you are working in your virtual environment, the python command will always refer to the python interpreter located within the virtual environment - which is a symbolic link to the interpreter that you used to create the virtual environment. As long as you are working in your virtual environment, the python command will point to the interpreter of your choice (the one you used to create the environment).
Which Interpreter Are You Using?

Because you can have multiple interpreters on any given workstation, it is important to know which interpreter you are using at any point in time.

Outside of a virtual environment, your interpreter could be called by many names:

    python
    py -3 (windows only)
    python3
    python3.8
    python3.9
    and so on

Inside a virtual environment, your interpreter will always go by the name python, which is much easier to remember and work with.
Verify Your Interpreter

If there is ever any confusion about which interpreter you are using, there are couple of commands that can help you out:

which python

Execute in terminal
Sample Output

Will give you the full path to the interpreter.

python -V

Execute in terminal
Sample Output

Will give you the version info for the interpreter.

Take a minute to ensure you have your Terminal open, virtual environment activated, and are using a Python interpreter greater than v3.9.
Install Requirements

Now that your virtual environment is active, meaning you have (venv) in your command prompt, you are ready to install the required libraries. You probably saw the requirements.txt file in the root of the repository. It lists what you are going to install in the virtual environment. You can take a look at it if you like:

cat requirements.txt

Execute in terminal

Next, you install those requirements with this special pip command.

pip install -r requirements.txt 

Execute in terminal

When you run this command, you see the libraries and dependencies progress as they install.

    At the end of any pip install command, you may see an error message about upgrading pip, which you usually can ignore. Pip is upgraded often.

To verify that you have the required libraries, run this command:

pip freeze

Execute in terminal

You'll get a long list of all the installed libraries including the dependencies of everything in requirements.txt. Now you are ready to rock-and-roll.
Accessing the Python Interactive Shell

Python comes equipped with a Read Evaluate Print Loop (REPL) (boring name) Interactive Shell! Which is awesome for playing with Python syntax, incrementally testing commands, playing with APIs and data, and so much more.

To access Python's interactive shell, just call the interpreter without providing any options or arguments.

Do this on your workstation:

python -i

Execute in terminal

    Note: On Windows within git-bash, you need to use the command python -i to explicitly start the interactive interpreter. On macOS, the interactive interpreter starts automatically with the python command.

Sample Output

You can enter any valid Python statement, and the interactive shell will execute it and display its output - if it has any output. We'll use this quite a bit as we explore some of Python's basic syntax and data types. For now, just remember that you always have this tool at your fingertips anytime you want to play with or test out some Python syntax.

Now, practice exiting the interactive interpreter

Type the Python command exit() in the interactive interpreter:

exit()

Execute in terminal

This exit() instruction does not deactivate your virtual environment. Only the deactivate command can do that.

    Note: You can also use keyboard shortcuts to exit the interactive interpreter on Windows, press Ctrl-Z and then Enter. On Linux or MacOS, press Ctrl-D.

Running a Script

Python files (again just text files) by convention end with the extension .py. To run a Python file, run the following command on the bash command line (not within the interpreter):

python intro-python/interpreter-basics/hello.py

Execute in terminal
Sample Output

    Note: You can also instruct the interpreter to run your script and then stay in the interactive shell. This can be useful to incrementally build or debug Python scripts. We'll talk more about this in the hands-on Lab with Python Types, Loops, and Tools.

For now, let's move on to talk about Python syntax.

