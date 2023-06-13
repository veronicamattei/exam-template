# Exam #1: "CMSmall"
## Student: s310707 MATTEI VERONICA

## React Client Application Routes

- Route `/login`: display a form to execute the login
- Route `/`: redirect the users to frontoffice
- Route `/frontoffice`: display the list of the pages in view mode
- Route `/frontoffice/pages/:id`: display the required page in view mode
- Route `/backoffice`: display the list of the pages in editable mode
- Route `/backoffice/pages/:id`: display the required page in editable mode
- Route `/backoffice/pages/add`: display a form to add a new page
- Route `*`: default route (not found)

## API Server

### Pages Management

#### Get all pages

* HTTP method: `GET`  URL: `/api/pages`
* Description: Get the full list of pages of all authors (draft, published and scheduled pages for logged users) or some of them (only published pages for not logged users)
* Request body: _None_
* Request query parameter: _None_
* Response: `200 OK` (success)
* Response body: Array of objects, each describing one page:

``` JSON
[
  {
    "id": 1,
    "title": "Title1",
    "user_name": "Author1",
    "cdate": "2023-06-07",
    "pdate": null,
  },
  {
    "id": 2,
    "title": "Title2",
    "user_name": "Author1",
    "cdate": "2023-06-10",
    "pdate": "2023-06-20",
  },
  ...
]
```

* Error responses:  `500 Internal Server Error` (generic error)

#### Get pages by id

* HTTP method: `GET`  URL: `/api/pages/:id`
* Description: Get the pages corresponding to the id
* Request body: _None_
* Request query parameter: The id of the page
* Response: `200 OK` (success)
* Response body: One object describing the requires page:

``` JSON
  {
    "id": 1,
    "title": "Title1",
    "user_name": "Author1",
    "cdate": "2023-06-07",
    "pdate": null,
  }
```

* Error responses:  `500 Internal Server Error` (generic error), `404 Not Found` (not present or unavailable)

#### Add a new page

* HTTP method: `POST`  URL: `/api/pages`
* Description: Add a new page to the pages of Author1
* Request body: description of the object to add (pages id value is not required and is ignored)

``` JSON
{
    "id": 3,
    "title": "Title3",
    "user_name": "Author1",
    "cdate": "2023-06-11",
    "pdate": "2023-06-11",
  }
```

* Response: `200 OK` (success)
* Response body: the object as represented in the database

* Error responses: `503 Service Unavailable` (database error)

#### Update an existing page

* HTTP method: `PUT`  URL: `/api/pages/:id`
* Description: Update values of an existing page, except the id
* Request body: description of the object to update

``` JSON
{
    "id": 1,
    "title": "Title1",
    "user_name": "Author1",
    "cdate": "2023-06-10",
    "pdate": null,
  }
```

* Response: `200 OK` (success)
* Response body: the object as represented in the database

* Error responses: `503 Service Unavailable` (database error)

#### Delete an existing page

* HTTP method: `DELETE`  URL: `/api/pages/:id`
* Description: Delete an existing page
* Request body: _None_

* Response: `200 OK` (success)
* Response body: an empty object

* Error responses:  `503 Service Unavailable` (database error)

### User management

#### Login

* HTTP method: `POST`  URL: `/api/sessions`
* Description: authenticate the user who is trying to login
* Request body: credentials of the user who is trying to login

``` JSON
{
    "username": "author1",
    "password": "password"
}
```

* Response: `200 OK` (success)
* Response body: authenticated user

``` JSON
{
    "id": 1,
    "username": "author1@polito.it", 
    "name": "Author1"
}
```

* Error responses:  `500 Internal Server Error` (generic error), `401 Unauthorized User` (login failed)

#### Check if user is logged in

* HTTP method: `GET`  URL: `/api/sessions/current`
* Description: check if current user is logged in and get him/her data
* Request body: _None_
* Response: `200 OK` (success)

* Response body: authenticated user

``` JSON
{
    "id": 1,
    "username": "user1@polito.it", 
    "name": "User1"
}
```

* Error responses: `500 Internal Server Error` (generic error), `401 Unauthorized User` (user is not logged in)

#### Logout

* HTTP method: `DELETE`  URL: `/api/sessions/current`
* Description: logout current user
* Request body: _None_
* Response: `200 OK` (success)

* Response body: _None_

* Error responses: `500 Internal Server Error` (generic error), `401 Unauthorized User` (user is not logged in)

## Database Tables

- Table `user` - contains id, name, email, role, password, salt
- Table `page` - contains id, title, cdate, pdate,user_id
- Table `block` - contains id, type, content, page_id
- ...

## Main React Components

- `ListOfSomething` (in `List.js`): component purpose and main functionality
- `GreatButton` (in `GreatButton.js`): component purpose and main functionality
- ...

(only _main_ components, minor ones may be skipped)

## Screenshot

![Screenshot](./img/screenshot.jpg)

## Users Credentials

|         email         |   name   | plain-text password |
|-----------------------|----------|---------------------|
| author1@polito.it    | Author1     | password            |
| user1@polito.it | User1   | password            |
| admin1@polito.it    | Admin1 | password            |
