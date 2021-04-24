# User Interface
## HTML
Contains 7 drop down list (with no values and unique ID)
```
Academic Year
Semester
Faculty
Program
Class
Module
Lecturer
```
A ``Visualize`` button, a totalAnswer(unique ID), 18 questions(unique ID) and a comment space (unique ID)

## JS

### getInfoDropDown

send **GET Request** through API using ajax with the following format:``/Questionnaire/api/endpoint_name?action=dump``.
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
The *data* received from each **GET Request** will be send to the appropriate ``ID_Name`` on the browser in the form of drop down list using $("``#ID_Name``").
Where ``#`` represents ID and  ``ID_Name``s are that ID we name in the html page.

### AllQuestionnaireChart
After chosing *data*s `optional` from 7 drop down lists (recommend chossing at least 1), if choose more than 1, must have the right combination,otherwise the ``Visualize`` button won't work:
 ~~Academic Year: 2002-2003 Semester: WS04~~\
-  [x] Academic Year:2002-2003 Semester: WS03
When ``Visualize`` button is clicked, the chosen *data*s `optional` from 7 drop down lists will be used for ``GET Request`` inside these functions:
-``get_Total_Count()``: send **GET Request** with `"/Questionnaire/api/questionnaire?action=getMaxResponseCount&" + data` to get total number of students \
-``get_Gender()``: send **GET Request** with `"/Questionnaire/api/questionnaire?action=getCounts&&" + data + "q=gender"` to get number of students participate in evaluation,send data to Chart_Gender\

-``Chart_Gender()``: receive data from ``get_Gender`` to draw a chart\

-``get_Question(i)``: send **GET Request** with `"/Questionnaire/api/questionnaire?action=getCounts&"+ data + "q=i"` ***(loop i 18 times for 18 questions)*** to get answers ``"Never","Rarely", "Sometimes", "Often", "Always"`` from the Responsdents and send data to Chart_Question(i,data) (create and store each answer in separate variable array and sum up for 18 questions) \

-``Chart_Question(i,data)``: receive data from ``get_Question(i)``***(Also loop 18 times)*** to draw a chart and display to browser by getting the ID ``#`` of the question, also use data from ``get_Gender()`` and ``get_Total_Count()`` to calculate mean, standard deviation, ResponseRate and number of Respondents answer the question\
-``Chart_Total()``: access variable array for each answer from ``get_Question(i)`` to get total answers for 18 questions and draw a chart and display to browser by getting the ID ``#`` of the totalAnswer
