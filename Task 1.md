# TASK 1: Front-end test plan

This test plan is aimed at covering the application's current requirements. 

The current requirements for this app are:

1. Application must be able to deploy in docker
2. Multiple users should be able to view the shared public todo list (no live updates, only on refresh)
3. Todo list items should persist after browser refresh
4. Todo items should not be able to be empty
5. Should be able to add todo items
6. Should be able to delete todo items
7. Should be able to edit todo items

Steps to get up and running on a Windows machine will be listed below:

1. Downloaded the todo list app: https://drive.google.com/file/d/1UL_vI9Wy1a4skDzK9d3nQoA5SnJof10x/view.
2. Extract the compressed file and move this to a safe, file location
3. Download and install Node.js (https://nodejs.org/en/)
4. Verify the node.js install by running the `node -v` command prompt
4. Open command prompt and navigate to the root folder of the of the project and then run the `npm install` command to install all project dependancies (found in the package-lock.json file)
5. Download and install Docker: https://docs.docker.com/
6. Start up Docker and make sure it's running in the background
7. Download and install VS Code: https://code.visualstudio.com/download
8. Open VS Code and open the project root folder which was extracted 
9. Open the terminal in VS Code and run the following commands:
    - To build the Docker image in the project,`docker build -t qe-todolist .`
    - To run the docker image, `docker run -p 8081:8080 -d qe-todolist`
    The app should now be running (virtually).

10. Navigate to `http://localhost:8081` in your browser to access the Todo List app and make sure it's running succefully.

### You should now be setup and ready to test the Todo list app!

## Scenario 1:  Multiple users should be able to view the shared public Todo list (no live updates, only on refresh)

For this test, we will need to make sure that the app is shared in Docker.

1. Please follow the steps in this Docker help article to achieve this: https://docs.docker.com/get-started/04_sharing_app/

The last steps of this article explain how once the app has been pushed into the repo, it will now be available to be accessed by anyone who has a Docker Hub account.

2. Once these steps have been followed, the app should now be publically accessible. 

## Please note, I was not 100% sure about this requirement (req 2).

# Test Cases:

## Scenario 1: Load the list

- Given the app has been deployed and running in Docker
- When the user accesses http:localhost:8081/todo via their browser
- Then the ToDo list loads 
- And all elements of the app are loaded

## Scenario 2:  Add an item to the list with a value consisting of alpha, numeric and special characters

- Given the user has the app loaded
- And has typed in a item value consisting of alpha, numeric and special characters into the `Create new todo item:` textbox
- When the user clicks `Sumbit`
- Then the item is successfully added to the list

## Scenario 3:  Add an empty item to the list (valid test case due to discovered bug)

- Given the user has the app loaded
- And has left the `Create new todo item:` textbox empty
- When the user clicks `Sumbit`
- Then nothing is added to the list

## Scenario 4:  Add an item consisting of just spaces to the list (valid test case due to discovered bug)

- Given the user has the app loaded
- And has typed in an item value consisting of just spaces into the `Create new todo item:` textbox
- When the user clicks `Sumbit`
- Then nothing is added to the list

## Scenario 5:	Edit an item in the list

- Given the user has the app loaded
- And the list has existing items populating it
- And has edited the value of the item to consist of alpha, numeric and/or special characters
- When the user clicks `Update`
- Then the item is successfully updated

## Scenario 6: Edit an item to be empty (valid test case due to discovered bug)

- Given the user has the app loaded
- And the list has existing items populating it
- And has removed the value of an item to be blank/empty
- When the user clicks `Update`
- Then the item is not updated

## Scenario 7: Edit an item to consist of just spaces (valid test case due to discovered bug)

- Given the user has the app loaded
- And the list has existing items populating it
- And has added one or many spaces to the `Update Value` textbox
- When the user clicks `Update`
- Then the item is not updated

## Scenario 8: Delete an item

- Given the user has the app loaded
- And the list has existing items populating it
- When the user clicks on the black "x" to the left of an item
- Then the item is deleted from the list

## Scenario 9: Delete an item which has been edited to contain an empty value (valid test case due to discovered bug)

- Given the user has the app loaded
- And the list has existing items populating it
- When the user clicks on the black "x" to the left of an item
- Then the item is deleted from the list

## Scenario 10: Delete an item which has been edited to consist of just spaces (valid test case due to discovered bug)

- Given the user has the app loaded
- And the list has existing items populating it
- When the user clicks on the black "x" to the left of an item
- Then the item is deleted from the list

## Scenario 11:  List items should persist after the browser has been refreshed

- Given the user has the app loaded
- And the list has existing items populating it
- When the user refreshes their browser
- Then the list items should remain unchanged