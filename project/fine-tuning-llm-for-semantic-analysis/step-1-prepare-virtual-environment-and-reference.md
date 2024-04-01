# Step 1: Prepare Virtual Environment & Reference

## How to set up a Python virtual environment?

*   To create a Python virtual environment in your current project folder, follow these steps in your terminal or command prompt. Make sure you're in the directory of your project where you want the virtual environment to be set up.

    1.  **Navigate to your project directory** (if you're not already there):

        ```bash
        cd /path/to/your/project
        ```

        Replace `/path/to/your/project` with the actual path to your project directory.
    2.  **Create the virtual environment**:

        *   On **macOS and Linux**:

            ```bash
            python3 -m venv venv
            ```
        *   On **Windows**:

            ```cmd
            python -m venv venv
            ```

        This command creates a new directory named `venv` in your project directory, containing the virtual environment. <mark style="color:red;">You can replace</mark> <mark style="color:red;"></mark><mark style="color:red;">`venv`</mark> <mark style="color:red;"></mark><mark style="color:red;">with another name if you prefer a different name for your virtual environment.</mark>
    3. **Activate the virtual environment**:
       *   On **macOS and Linux**:

           ```bash
           source venv/bin/activate
           ```
       *   On **Windows** (using Command Prompt):

           ```cmd
           .\venv\Scripts\activate
           ```
       *   On **Windows** (using PowerShell):

           ```powershell
           .\venv\Scripts\Activate.ps1
           ```

    After activation, you should see the name of your virtual environment (`venv` in this case) prefixed to your command line prompt, indicating that the virtual environment is active. Now, any Python or pip commands you run will use the versions in the virtual environment, isolated from the rest of your system.



Hint: you can change the

## How to Use It in VS code

To use a Python virtual environment in Visual Studio Code (VS Code), follow these steps:

#### 1. Open Your Project in VS Code

First, ensure your project folder is open in VS Code. You can do this by selecting **File > Open Folder** from the menu and choosing your project directory.

#### 2. Ensure Python and Python Extension are Installed

Make sure you have Python installed on your system and the Python extension for VS Code installed. You can find the Python extension by searching for "Python" in the Extensions view (`Ctrl+Shift+X` or `Cmd+Shift+X` on macOS).

#### 3. Open a Terminal in VS Code

Open a new terminal in VS Code by using the shortcut `` Ctrl+` `` (backtick) or by selecting **Terminal > New Terminal** from the top menu. This terminal should automatically open to your project's directory.

#### 4. Create and Activate the Virtual Environment

If you haven't already created a virtual environment in your project directory, you can do so directly in the VS Code terminal by following the instructions provided earlier. To activate your virtual environment in the VS Code terminal:

*   On **macOS and Linux**:

    ```bash
    source venv/bin/activate
    ```
*   On **Windows** (using Command Prompt):

    ```cmd
    .\venv\Scripts\activate
    ```
*   On **Windows** (using PowerShell):

    ```powershell
    .\venv\Scripts\Activate.ps1
    ```

#### 5. Select the Python Interpreter

After activating your virtual environment, you should select the corresponding Python interpreter for VS Code:

1. Open the Command Palette by pressing `F1` or `Ctrl+Shift+P` (`Cmd+Shift+P` on macOS).
2. Type "Python: Select Interpreter" and select it.
3. Choose the interpreter that corresponds to your virtual environment. It should be something like `./venv/bin/python` (or `.\venv\Scripts\python.exe` on Windows) and will be located inside your project folder.

#### 6. Install Packages and Work on Your Project

With the virtual environment activated and the interpreter selected, any Python packages you install using `pip` will be confined to this environment. This setup helps keep your project's dependencies isolated from other projects and system-wide Python packages.

#### 7. Deactivate the Virtual Environment

When you're done working in your virtual environment, you can deactivate it by typing `deactivate` in the terminal.

VS Code's integration with Python and virtual environments makes it easier to manage project-specific dependencies and settings, enhancing your development workflow.





Power By OpenAI



