# TASK 2: Bugs found

- I found 3 bugs via the front end.
- If the bug could be reproduced via the back-end, I added repo steps for that aswell.

`!!Please note that there is evidence for each bug found and named appropriately to easily be linked to each bug. The evidence can be found here in the "tests" folder of the project compressed in the testevidence.rar file.!!`

## BUG 1 - A list item can be updated to be empty

### Description/Current behaviour:

- An item in the list can be updated to be blank/empty.
- This can occur via the web front-end and the API.

### Recreation steps:

Via front-end

1. Load the Todo List `http://localhost:8081/todo`.
2. Add an item to the Todo List.
3. Without adding anything to the "Update Value" textbox of the newly created item, click on the "Update" button of the item in the list.

Via back-end

1. Make sure the list is populated with at least one item.
2. Via Postman, run `http://localhost:8081/todo/edit/{{indexValue}}?edittodo=` where `{{indexValue}}` equals the index value of the item being updated in the list array.
3. View the response or refresh the browser instance of the app.

### Expected behaviour:

For front-end

- The item should not be updated.
- A warming message should be displayed indicating what is expected of the user or why the action cannot be performed.

For back-end

- The item should not be updated.
- Validation should be applied to the API call and a `400: Bad Request` response message should be returned should no value be provided.

## NOTE: Please find test evidence `BUG1.mp4` in the project's `test` folder.

## BUG 2 - An item can be added to the list which consists of only spaces

### Description/Current behaviour:

- An item consisting of just spaces can be added to the list.
- This can occur via the web front-end and the API.

### Recreation steps:

Via front-end

1. Load the Todo List `http://localhost:8081/todo`.
2. Click inside the "Create new todo item:" textbox and hit the space bar a couple of times, at minimum, once.
3. Click the "Submit" button.

Via back-end

1. Via Postman, run `http://localhost:8081/todo/add/?newtodo=   `.
2. View the response or refresh the browser instance of the app.

### Expected behaviour:

Front-end

- The item should not be added to the list.
- A warming message should be displayed indicating what is expected of the user or why the action cannot be performed. 

The best way to solve this would be to add a trim function to the textbox which triggers once when the submit button is clicked. In my opinion, this would make for the best user experience.

For back-end

- The item should not be added to the list.
- Validation should be applied to the API call and a `400: Bad Request` response message should be returned should no value be provided.

## NOTE: Please find test evidence `BUG2.mp4` in the project's `test` folder.

## BUG 3 - Typo in the apps titel which appears in the browser tab

### Description/Current behaviour:

- When the app is loaded in the browser, the title of the app in the browser tab is misspelled.

### Recreation steps:

1. Load the Todo List `http://localhost:8081/todo`.
2. View the title of the app in the browser tab.

### Expected behaviour:

- The title should be "QE todolist".

## NOTE: Please find test evidence `BUG3.png` in the project's `test` folder.


Bugs found through exploratory testing via the API.


## BUG 4 - The todo/add API call always adds a blank item to the list

### Description/Current behaviour:

- A blank item is added to the list every time the todo/app API call is used. Regardless of the character combination or characters stipulated to name the item. 
- As a result, that created item cannot be deleted via the web front end, nor can it be deleted via the API using the todo/delete call (please see bug 7).

### Recreation steps:

1. Via Postman, run the `http://localhost:8081/todo/add/?newtodo={{value}}` call, where `{{value}}` equals the value of the item.
2. View the response.

### Expected behaviour:

- The value stipulated in the call parameter should be added as the value for the newly created item.

## NOTE: Please find test evidence `BUG4.mp4` in the project's `test` folder.

## SIDE NOTE: The fact that these items cannot be deleted, indicates to me there is a need for a seperate bug (bug 7) which hopefully addresses the way the app deletes an item. In my opinion, no matter how the item was created, the item should always be deletable. This ensures robustness of the app.

## BUG 5 - The todo/add API call allows a blank item to be added to the list

### Description/Current behaviour:

- When running the todo/add API call without stipulating a value for the item being added, the API still adds an item to the list.

### Recreation steps:

1. Via Postman, run `http://localhost:8081/todo/add/?newtodo=`.
2. View the response or refresh the browser instance of the app.

### Expected behaviour:

- Validation should be applied to the API call and a `400: Bad Request` response message should be returned.

## NOTE: Please find test evidence `BUG5.mp4` in the project's `test` folder.

## BUG 6 - The todo/edit API call strips the value of the item being edited

### Description/Current behaviour:

- When running the todo/edit API call the item which is supposed to be updated actually gets it's value stripped.

### Recreation steps:

1. Make sure the list contains valid items with values in it. 
2. Via Postman, run `http://localhost:8081/todo/edit/{{indexValue}}?edittodo={{newValue}}` where `{{indexValue}}` equals the index value of the item being updated in the list array and where `{{newValue}}` equals the new value of the list item.
3. View the response or refresh the browser instance of the app.

### Expected behaviour:

- The item should be updated with the newly specified value.

## NOTE: Please find test evidence `BUG6.mp4` in the project's `test` folder.

## BUG 7 - Depending on the way the list item was created or edited, prevents the item from being deleted

### Description/Current behaviour:

- When an item is added to the list using the todo/add API call, it always adds the item with a blank value (reference bug 4). I feel that due to the way in which the item is being created, is preventing it from being deleted.

### Recreation steps:

1. Via Postman, run the `http://localhost:8081/todo/add/?newtodo={{value}}` call, where `{{value}}` equals the value of the item.
2. View the response.
3. Via the web app, refresh the browser and try delete the newly created item by clicking on the black X (please see bug 7).
4. Via Postman, using the todo/delete API call, try delete this newly created item (please see bug 7).

### Expected behaviour:

- Regardless of how an item is created OR edited, the item should always be able to be deleted.

I am not not sure whether this bug is coincidently a result of BUG4 being present or if the way the todo/delete API call is implemented incorrectly? Regardless, I feel it is worth investigating because at the end of the day, the item should be able to be deleted regardless of how it was created or edited - to the end-user, the item exists, it should therefore be able to be deleted.

## NOTE: Please reference `BUG4.mp4` in the project's `test` folder as evidence.