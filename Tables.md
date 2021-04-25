## Notice:
- There are global variables in these JS files and can be used by any of the files.
- Consider carefully if you want to create/modify a global variable.

## Details of the JavaScript files:
- There are 11 files
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

- Each file have 5 functions:
  - `RequestGET()`: send `GET` requests
  - `ShowTable()`: display tables
  - `Add()`: add new record
  - `deleteRow()`: delete a row
  - `sendDelete()`: send `DELETE` requests


### `RequestGET()`:

Send `GET Request` according to their perspective table

**Parameter:** None

**Return** data, `ShowTable(data)`

### `ShowTable(data)`:
Create additional "Add" and "Delete" button for add and delete data.

**Parameter:**<br>
- `data` is the returned value of successful `GET` requests to dump resource.<br>

**Return:** Table with data.

### `Add()`:
send `PUT Request` to database to check if this record can be add.

**Parameter:** None

**Return:** Add new record to table (if not violate conditions in database).

### `deleteRow(row)`:

delete record in table (if not violate conditions in database).

**Parameter:**
- `row`: current row of the "Delete" button.<br>

**Return:** delete row, `sendDelete(id)`

### `sendDelete(id)`:

Send `DELETE Request` to database (if not violate conditions in database)

**Parameter:**<br>

- `id`: value to delete

**Return:** "Delete success"
