# custom-scripts-examples

## Installation:
![custom scripts installation](images/installation/custom_scripts_installation.gif)
1. Inside of a project, navigate to > **"Customize"** > **"Rules"** > **"+ Add rule"** > **"Create custom rule"**
   <details>
   <summary>more details</summary>

   ![add a rule](images/installation/1.png)
   ![create a custom rule](images/installation/1(2).png)
   </details>
2. Navigate to **"Do this..."** > **"External actions"** > **"Run custom script"**
   <details>
   <summary>more details</summary>

   ![run custom script action](images/installation/2.png)
   </details>
3. Click on the **"Please authenticate to proceed."** button. This will open a new tab to the **"Grant Permission"** page
   <details>
   <summary>more details</summary>
   
   ![please authenticate to proceed](images/installation/3.png)
   </details>
4. Click on **"Allow"** and close the tab
   <details>
   <summary>more details</summary>
   
   ![grant permission allow button](images/installation/4.png)
   ![close tab](images/installation/4(2).png)
   </details>
5. You should now be authenticated and be presented with the custom scripts action
   <details>
   <summary>more details</summary>
   
   ![run custom script action page](images/installation/5.png)
   </details>

## Usage:
![use custom scripts](images/installation/use_custom_scripts.gif)
1. Inside of a project navigate to > **"Customize"** > **"Rules"** > **"+ Add rule"** > **"Create custom rule"**
   <details>
   <summary>more details</summary>
   
   ![add a rule](images/installation/1.png)
   ![create a custom rule](images/installation/1(2).png)
   </details>
2. Select a trigger (e.g., **"Task is added to a project"**):
   <details>
   <summary>more details</summary>
   
   ![add a rule](images/usage/2.png)
   </details>
3. Configure a condition for the **"+ Check if..."** step or delete that step
   <details>
   <summary>more details</summary>
   
   ![configure or delete condition](images/usage/3.png)
   </details>
4. Navigate to  **"Do this..."** > **"External actions"** > **"Run custom script"** you should be presented with the custom scripts action.
   This is where you will want to write/provide your script.
   <details>
   <summary>more details</summary>
   
   ![run custom script action](images/usage/4.png)
   ![sample script](images/usage/4(2).png)
   ![uncommented sample script](images/usage/4(3).png)
   </details>
   
   The custom scripts action utilizes the [node-asana](https://github.com/Asana/node-asana) ([v3.X.X](https://www.npmjs.com/package/asana)) client library to make API calls to Asana.
   
   In each custom script, we provide you with the following information shown at the top of the script in a multi-lined comment:
   ```javascript
   /**
    * What's in scope?
    * 1. (number) project_gid, workspace_gid, task_gid (only if triggered on a task)
    * 2. (function) log - this behaves like console.log and takes any number of parameters
    * 3. (object) *ApiInstance - for each group of APIs, an object containing functions to call the APIs; for example:
    *    tasksApiInstance.getTask(...)
    *    goalsApiInstance.addFollowers(...)
    * For more info, see https://github.com/Asana/node-asana
    */
   ```

   You can utilize this information to write a custom script using the [node-asana](https://github.com/Asana/node-asana) ([v3.X.X](https://www.npmjs.com/package/asana)) client library.
   
   For this example usage, we will just uncomment the provided sample script. The sample script fetches the information about the triggered task and updates the task name.
5. Click on the **"Publish rule"** button
   <details>
   <summary>more details</summary>
   
   ![publish rule](images/usage/5.png)
   </details>
6. Trigger your rule. EX: In this scenario we configured our rule to trigger when a task is added to our project. The action the rule will take is updating the name of the new task.
   <details>
   <summary>more details</summary>
   
   ![custom script rule triggered](images/usage/6.png)
   ![custom script rule ran](images/usage/6(2).png)
   </details>

## Developing/Testing your script locally on your computer

The following is a way to write/test your script on your computer. You can copy the code below into your code editor and start working through the TODOs.

**Pre-requisite:**
1. Make sure you have [Node.js](https://nodejs.org/en/download) installed on your computer 
2. Make sure you have `v3.X.X` version of [node-asana](https://github.com/Asana/node-asana) ([npm](https://www.npmjs.com/package/asana)) installed on your computer
3. Create a file for your script. Copy and paste the below script into that file. EX: `test.js`
4. Go through the TODOs outlined in the below script
5. Test your script `node <YOUR_SCRIPT_FILE_NAME>.js`. EX: `node test.js`

**TIP:** You can reference the ["Documentation for API Endpoints"](https://github.com/Asana/node-asana?tab=readme-ov-file#documentation-for-api-endpoints) section of [node-asana](https://github.com/Asana/node-asana) `README.md` to reference sample code and endpoints for your script.

```javascript
/*
This is template code for you to test your custom scripts locally on your computer
1. Make sure you have Node.js installed on your computer
2. Make sure you have v3.X.X version of the node-asana client library installed on your computer
3. Create a file and copy this code over to that file (EX: test.js)
4. Go through the TODOs outlined in this script
5. Test your script by running "node test.js" in your terminal
*/

const Asana = require('asana');

let client = Asana.ApiClient.instance;
let token = client.authentications['token'];
token.accessToken = "<YOUR_PERSONAL_ACCESS_TOKEN>"; // TODO: Replace this with your Personal Access Token (PAT)

// Set your project, task and workspace gid here
// These will be provided to you when the custom script gets executed.
// We want to emulate that so we set those values here
//
// TODO: Set these values
const project_gid = 123;
const task_gid = 456;
const workspace_gid = 789;

// Set up the resource instances that you plan on using for your script here
// The custom script will make these available for you so you don't need to worry about
//
// TODO: instantiate the resources that you plan on using in your script
let tasksApiInstance = new Asana.TasksApi();

/*
----------------------------------------------------------------------------------------
Write your custom script below COPY and PASTE your script into the custom script rule.
IMPORTANT: Remember to change all of your "console.log" into "log"
----------------------------------------------------------------------------------------
*/

/**
 * What's in scope?
 * 1. (number) project_gid, workspace_gid, task_gid (only if triggered on a task)
 * 2. (function) log - this behaves like console.log and takes any number of parameters
 * 3. (object) *ApiInstance - for each group of APIs, an object containing functions to call the APIs; for example:
 *    tasksApiInstance.getTask(...)
 *    goalsApiInstance.addFollowers(...)
 * For more info, see https://github.com/Asana/node-asana
 */

const run = async () => {
   try {
      // TODO: YOUR SCRIPT HERE
   } catch (error) {
      console.log(error); // TODO: Change this to "log" before or after copy paste to custom script rule
   }
};

run();

```

<details>
<summary>Example use case</summary>

```javascript
/*
This is template code for you to test your custom scripts locally on your computer
1. Make sure you have Node.js installed on your computer
2. Make sure you have v3.X.X version of the node-asana client library installed on your computer
3. Create a file and copy this code over to that file (EX: test.js)
4. Go through the TODOs outlined in this script
5. Test your script by running "node test.js" in your terminal
*/

const Asana = require('asana');

let client = Asana.ApiClient.instance;
let token = client.authentications['token'];
token.accessToken = "<YOUR_PERSONAL_ACCESS_TOKEN>"; // TODO: Replace this with your Personal Access Token (PAT)

// Set your project, task and workspace gid here
// These will be provided to you when the custom script gets executed.
// We want to emulate that so we set those values here
//
// TODO: Set these values
const project_gid = 123;
const task_gid = 456;
const workspace_gid = 789;

// Set up the resource instances that you plan on using for your script here
// The custom script will make these available for you so you don't need to worry about
//
// TODO: instantiate the resources that you plan on using in your script
let tasksApiInstance = new Asana.TasksApi();

/*
----------------------------------------------------------------------------------------
Write your custom script below COPY and PASTE your script into the custom script rule.
IMPORTANT: Remember to change all of your "console.log" into "log"
----------------------------------------------------------------------------------------
*/

/**
 * What's in scope?
 * 1. (number) project_gid, workspace_gid, task_gid (only if triggered on a task)
 * 2. (function) log - this behaves like console.log and takes any number of parameters
 * 3. (object) *ApiInstance - for each group of APIs, an object containing functions to call the APIs; for example:
 *    tasksApiInstance.getTask(...)
 *    goalsApiInstance.addFollowers(...)
 * For more info, see https://github.com/Asana/node-asana
 */

const run = async () => {
    try {
        // Generate a random number
        const randomNum = Math.random();
        
        // Get information about the triggered task
        const task = await tasksApiInstance.getTask(task_gid, {});
        
        // Update the task name. Append random number to name of the triggered task
        await tasksApiInstance.updateTask(
            {
                data: {
                    name: `${task.data.name} - ${randomNum}`
                }
            },
            task_gid
        );
    } catch (error) {
        console.log(error); // TODO: Change this to "log" before or after copy paste to custom script rule
    }
};

run();
```

![develop script locally 1](images/usage/develop_locally_1.png)
![develop script locally 2](images/usage/develop_locally_2.png)
</details>

## Example Scripts

- [Automatically update a goal metric when a deal is closed](example_scripts/update_goal_metric.md)
- [Generate a unique UUID when task is added to a project](example_scripts/generate_unique_uuid.md)