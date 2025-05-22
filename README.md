# EnableCodeInterpreter
Creating and Exporting Copilot Studio Solution
Here’s a step-by-step instruction set for creating a new Copilot Studio solution, adding existing agents, and exporting it as an unmanaged solution. This guide is based on the latest Microsoft documentation  .

### 1. Open Copilot Studio
Go to https://copilotstudio.microsoft.com and sign in.

### 2. Create a New Solution
You don't have to create a new solution here.  You are able to export the current solution that contains your agent but if there are numerous assets in the solution then finding the proper file to edit will be a little more annoying.
In the left navigation pane, click the three dots (...) and select Solutions.
Click + New solution.
Fill in:
Display Name
Name
Publisher (select or create one)
Version
Click Create.

### 3. Add Existing Agents to the Solution
Open the solution you just created.
Click Add existing → Agent → Agent again.
From the list, select the agent(s) you want to include.
Click Add.
Click the ⋮ (More Commands) next to the agent.
Select Advanced → Add required objects.

### 4. Export the Solution
Go back to the Solutions list.
Select the solution you created.
Click Export.
Choose Unmanaged (default).
Optionally run the Solution Checker.
Click Export again.
Once ready, click Download to save the .zip file.

### 5. Include Code Interpreter yml
Extract the contents of the .zip file.
Navigate to the /botcomponents
The next directory you are looking for will follow this naming convention (<prefix>_<agentName>.gpt.default) and look like the image below.  In this example my prefix is 'crce2', my agent name is 'codeGenerator'
![alt text](<Screenshot 2025-05-21 155633.png>)

Open the appropriate directory and then open the file dataand locate the field gptCapabilities:
Change the value associated with gptCapabilities: to enable Code Interpreter
```yaml
gptCapabilities:
codeInterpreter: true
codeInterpreterCapabilities:
    - codeInterpreter: true
    - codeInterpreterLanguage: python
    - codeInterpreterVersion: 3.8
    - codeInterpreterLibraries:
        - pandas
        - numpy
        - matplotlib
        - seaborn
        - scikit-learn
    - codeInterpreterFileTypes:
        - csv
        - json
        - xlsx
        - txt
```


### 6. Upload Solution
Save the file and Compress the directories into a single .zip archive.  Be sure to only include the sub-directories.  When the solution is uploaded the these files must be found at the root of the archive
solution.xml
[Content_Types].xml
customizations.xml
Import the solution to Copilot Studio.  This will overwrite the solution that was originally exported.

### 7. Confirmation
Once it has been successfully imported, click on the solution to view its contents and navigate to the Agent components section
Find the name of your agent and select it
Click on Advanced and select See solution layers
![alt text](<Screenshot 2025-05-21 161247.png>)

Click on the first layer to see the details.  Confirm you see the code detailing that code interpreter is enabled
![alt text](<Screenshot 2025-05-21 162731.png>)