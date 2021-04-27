# User Manual for VGU SQM's Questionnaire

## Home page (`/Questionnaire`)

The home page has links to the 3 applications:

  - Tables: `Questionnaire/tables/`
  - Questionnaire form: `Questionnaire/Questionnaire/`
  - Visualize: `Questionnaire/Visualize/`

## Tables (`/Questionnaire/tables`)

There are 11 tables in this page:

  - `Faculty in Academic Year`
  - `Academic Year`
  - `Semester`
  - `Faculty`
  - `Program`
  - `Module`
  - `Class`
  - `Lecturer`
  - `Teaching`
  - `Program in Faculty in Academic Year`
  - `Module in Program in Academic Year`

Each table has its own `Hide`/`Show` button, its functionality is to show or hide the corresponding table.

At the end of each record, there's a `Delete` button, it is used to delete a record. If that record does not relate to record(s) of any other tables, then it can be deleted, and the user is alerted of the successful deletion. Otherwise, the user will the alerted that the deletion is unsuccessful.

At the bottom of each table, there's a text field or drop-down selection for the user to add a new record. Upon pressing the `Add` button, if the input value is valid, an alert box telling the value has been added successfully will show up. Otherwise, an error message will appear.

After successfully adding/deleting a record, the table will be refreshed, this will update the table.

## Questionnaire (`/Questionnaire/Questionnaire`)

There are 7 fields in the questionnaire that will be used to identify questionnaires

  - `Academic Year`
  - `Semester`
  - `Faculty`
  - `Program`
  - `Module`
  - `Class`
  - `Lecturer`

To submit a questionnaire answer, the user (students) are to follow these steps:

1. Select the 7 Questionnaire-identifying fields to get the desired Class and Lecturer identifying a Questionnaire
2. Fill in the questions. All 17 multiple-choice questions must be filled, while **Comments** is optional.
3. After selecting every option, the students can press `Submit` button to submit the questionnaire, then the page will refresh.
4. If any compulsory question is not filled, the user cannot submit the form.

## Data Visualization (`/Questionnaire/Visualize`)

There are 7 fields in the questionnaire that will be used to identify what to visualize

  - `Academic Year`
  - `Semester`
  - `Faculty`
  - `Program`
  - `Module`
  - `Class`
  - `Lecturer`

To visualize questionnaire responses, the user (VGU SQM staff) are to follow these steps:

1. Choose the filters (the 7 fields) to visualize for
2. Click the **Visualize** button to get graphs corresponding to the applied filters.
3. 17 questions are then visualized as 17 bar charts. If both `Class` and `Lecturer`, comments will also be shown.

# Visualize

## JS

## ``getInfoDropDown``

Send `GET Request` through API using ajax with the following format:``/Questionnaire/api/endpoint_name?action=dump``.

Where ``endpoint_name`` is replaced with the appropriate endpoint:

```
- academicYear
- semester
- faculty
- program
- class
- module
- lecturer
```

The `data` received from each `GET Request` will be send to the appropriate ``ID_Name`` in the HTML in the form of drop down list using $("``#ID_Name``").

Where ``#`` represents ID and  ``ID_Name``s are the name we put in the html page.

## ``getComments``

When ``Visualize`` button is clicked, if `value` from Class and Lecturer are not chosen, nothing happen.

Otherwise, it will execute the following:

+ send `GET Request` with `"/Questionnaire/api/questionnaire?action=getComments&"` + `value`
+ display the comments on HTML by accessing the comment space unique ID


## ``AllQuestionnaireChart``

After chosing `value` (optional) from 7 drop down lists in HTML (recommend chossing at least 1), if choose more than 1, must have the right combination,otherwise the ``Visualize`` button won't work

example:

- ~~Academic Year: 2002-2003 Semester: WS04~~
-  [x] Academic Year:2002-2003 Semester: WS03

When ``Visualize`` button is clicked, the chosen `value`s (optional) from 7 drop down lists will be used for ``GET Request`` inside these functions:

### get_Total_Count()
---

Send `GET Request` with `"/Questionnaire/api/questionnaire?action=getMaxResponseCount&"` + `value`\

**Parameter:**
+ None

**Return** `data` (total number of students)

### get_Gender()
---

Send `GET Request` with `"/Questionnaire/api/questionnaire?action=getCounts&"` + `value` + `"q=gender"`\

**Parameter:**
+ None

**Return** `data` (students participate in evaluation), `Chart_Gender(data)`

### Chart_Gender(data)
---

**Parameter:** 
+ data from get_Gender()

**Return** `Chart visualization on HTML` by accessing the gender's unique ID

### get_Question(question_i)
---

Send **GET Request** with `"/Questionnaire/api/questionnaire?action=getCounts&"` + `value` + `"q=question_i"`\
**Parameter:** 
+ question_i (loop 18 times for 18 questions)

**Return** `data`, `Chart_Questions(i,data)` 

### Chart_Question(question_i,data)
---

**Parameter:**
+ question_i (loop 18 times for 18 questions)
+ data (loop 18 times for 18 questions)

**Return** `Chart visualization on HTML` by accessing the question's unique ID

### Chart_Total()
---

Access data from get_Question(i) and sum all data for 18 questions

**Parameter:** 
+ None

**Return** `Chart visualization on HTML` by accessing the totalAnswer's unique ID

# Tables

## Notice:
- There are global variables in the 11 following JS files and can be used by any of the files:
  - DumpAcademicYear.js: `arrayData`
  - DumpClass.js: `CData`, `SizeData`, `SemData`, `MoID`, `SemIDFromSemester`, `ModIDFromModule`
  - DumpFaculty.js: `FID`
  - DumpFacultyInAcademicYear.js: `fData`, `aYData`, `FacultyIDFromFaculty`, `AYIDFromAY`
  - DumpLecturer.js: `LID`,
  - DumpModule.js: `arrayMData`
  - DumpModuleInProgramInAcademicYear.js: `moID`, `programID`, `aYearID`, `ModuleIDFromModule`, `ProgIDFromProg`, `AYearIDFromAYear`
  - DumpProgram.js: `arrayPData`
  - DumpProgramInFacultyInAcademicYear.js: `proID`, `facID`, `yearID`, `ProgramIDFromProgram`, `FacIDFromFaculty`, `AYeaIDFromAYea`
  - DumpSemester.js: `semID`, `AyIDFromAy`
  - DumpTeaching.js: `LecID`, `ClassID`, `LecIDFromLecturer`, `ClassIDFromClass`
- Consider carefully if you want to use/create/modify variables that have the same name as the listed above.

## Details of the JavaScript files:
- There are 11 tables, in the code, they are abbreviated as follows: 
  - `Faculty in Academic Year` = `FAY`
  - `Academic Year` = `AY`
  - `Semester` = `S`
  - `Faculty` = `F`
  - `Program` = `P`
  - `Module` = `M`
  - `Class` = `C`
  - `Lecturer` = `L`
  - `Teaching` = `T`
  - `Program in Faculty in Academic Year` = `PFA`
  - `Module in Program in Academic Year` = `MPA`

- In each Dump*.js file, there are 5 functions:
  - `RequestGET*()`: send `GET` requests
  - `Show*Table()`: display tables
  - `Add*()`: add new record
  - `delete*Row()`: delete a row
  - `send*Delete()`: send `DELETE` requests

- Replace the `*` with abbreviations above, for example: in DumpAcademicYear.js, there are:
  - `RequestGETAY()`
  - `ShowAYTable()`
  - `AddAY`
  - `deleteAYRow()`
  - `sendAYDelete()`


### `ShowTable(data)`:
**Parameter:**<br>
- `data` is the returned value of successful `GET` requests to dump resource.<br>

**Functionality:**<br>
- This function is called in `RequestGET*()` to take the returned values from the request and display them in a table.
- It also creates "Add" and "Delete" button to add and delete records.
- Some input fields that can be obtained from the database will be put into dropdown selection via `GET` requests.<br><br>

### `Add()`:
- This function will allow user to add new record to the table if the input does not violate any conditions in the database.
- If there's a violation, the return status is NOT `OK` (or `200`), and an alert box telling the user "Cannot add, invalid input." will pop up.
- Otherwise, upon a successful `PUT` request, an alert box will pop up telling the user "Added `value` to `*` successfully"
(where `value` is the user input and `*` is the name of the table).
- After adding, the table will be refreshed.<br><br>

### `RequestGET()`:
- This function will send a `GET` request to the API endpoint corresponding to its table
- For example: a `GET` request to the following endpoint for dumping resource of Academic Year table: `/Questionnaire/api/academicYear?action=dump`
- The returned value will be used in `ShowTable(data)` and `Add()`.<br><br>

### `deleteRow(r)`:
**Parameter:**<br>
- `r` is the current row of the "Delete" button.<br>

**Functionality:**<br>
- This function will delete the current row in the interface and call `sendDelete()`.<br><br>

### `sendDelete(id)`:
**Parameter:**<br>
- `id` is the value that the the user wants to delete, this value will be obtained based on `deleteRow()`.<br>

**Functionality:**<br>
- This function will allow user to delete a record in the table if the it does not violate any conditions in the database.
- If there's a violation, the return status is NOT `OK` (or `200`), and an alert box telling the user "Cannot delete." will pop up.
- Otherwise, upon a successful `DELETE` request, an alert box will pop up telling the user "Deleted `value` from `*` successfully."
(where `value` is the value that the user wants to delete and `*` is the name of the table).
- After deleting, the table will be refreshed.

# Questionnaire form

## Submit.js
- This script has 2 functions: `GetSubmitData()` and `SendSubmitData()`
### `GetSubmitData()`:
- This function will take input values of the questionnaire form, wrap it into a JSON called `sendData` for further processing.
  - `sendData` comprise of 5 properties:
    - `lecturerID`
    - `classID`
    - `gender`
    - `qa` (an array of answers encoded using integer)
    - `comment` of the student.
- In order to submit the questionnaire form, the user must answer every question.

### `SendSubmitData(sendData)`:
**Parameter:**<br>
- `sendData` is a JSON that is described in `GetSubmitData()`.<br>

**Functionality:**
- This function is used to send a `PUT` request to the server to save information in the filled questionnaire to database.
- Upon successful submission (i.e. answering every question and pressing `Submit` button), an alert box telling the user that the form has been "Submitted" will appear.
- If the user leave any question unanswered then pressing the `Submit` button, an alert box with the following message will appear: `"Please select an option for every question."`
- If there's any unexpected error, an alert box `"Error when submitting, please try again."` will appear.
<br><br><br>
------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## getClassOptions.js

## Notice:
- There are global variables in this JS file and can be used by any of the files in the same directory:
  - `arrAY`, `arrSem`, `arrFal`, `arrPro`, `arrMod`, `arrCla`, `arrLecture`
  - `AYQuery`, `semQuery`, `falQuery`, `proQuery`, `modQuery`, `claQuery`, `lecQuery`
- Consider carefully if you want to use/create/modify variables that have the same name as the listed above.

## Details:

**Functionality:**

- There are 7 functions that send `GET` requests to different endpoints:
  1. `ShowAYDropdown()`: `/Questionnaire/api/academicYear?action=dump`<br>
	2. `ShowSDropdown()`: `/Questionnaire/api/semester?action=dump`<br>
    **- Return values are `Academic Years` and `Semesters`, respectively.<br><br>**

  3. `ShowFDropdown()`: `/Questionnaire/api/facultyInAcademicYear?action=getFaculties&yid=AcademicYearValue`<br>
	4. `ShowPDropdown()`: `/Questionnaire/api/programInFacultyInAcademicYear?action=getPrograms&yid=AcademicYearValue&fid=FacultyID`<br>
	5. `ShowMDropdown()`: `/Questionnaire/api/moduleInProgramInAcademicYear?action=getModules&yid=AcademicYearValue&pid=ProgramID`<br>
	6. `ShowCDropdown()`: `/Questionnaire/api/moduleInProgramInAcademicYear?action=getClasses&sid=SemesterID&pid=ProgramID&mid=ModuleID`<br>
	7. `ShowLDropdown()`: `/Questionnaire/api/teaching?action=getLecturers&cid=ClassID`<br>
    **- Return values of these `GET` requests are after the `?action=get*`.<br>**
    **- Return values correspond to the supplied parameters.<br><br>**

- After each `GET` request, the return data will be put into a dropdown selection.
- Every option must be selected, if not, an alert box will appear `"Please select an option"`.

