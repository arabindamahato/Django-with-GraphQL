# Django-with-GraphQL

## To run this project in your system please follow the steps below :
 
1. Create a virtual environment in your system.
2. Clone this project.
3. Run the Requirements.txt (pip install -r requirements.txt) .
4. Run the migrations.
5. create superuser for accessing admin panel.
6. Run the Django Server.
7. Follow the listed Url for accessing the Project Properly . 

#### Go to the browser and use the url given below .
- http://127.0.0.1:8000/graphql

## To List all users present in database use the below query in GraphiQL interface and hit the play button		
	query {
        users {
          edges {
            node {
              username,
              archived,
              verified,
              email,
              secondaryEmail,
            }
          }
        }
      }


###### Screenshot

<p align="center"> 
<img src="Screenshots/demo.png">
</p>



## To Register a new User Use the below code on  GraphiQL interface and hit the play button: 

	mutation {
        register(
          email: "arabinda@email.com",
          username: "arabindamahato",
          password1: "Jhantulal@1994",
          password2: "Jhantulal@1994",
        ) 
        {
          success,
          errors,
          token,
          refreshToken
        }
      }


## You will get this type of result after registering new user along with token. 
    {
      "data": {
        "register": {
          "success": true,
          "errors": null,
          "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6ImFyYWJpbmRhbWFoYXRvIiwiZXhwIjoxNTk1OTk4MjY0LCJvcmlnSWF0IjoxNTk1OTk3OTY0fQ.UUQ530xfv1Xj0qYM4kMGHGzRtzhw4j3DHi4okjEFUYI",
          "refreshToken": "20540e79d27e599516fbcfa0991bc1dc3e82e840"
        }
      }
    }


## Check if the new user is really added on the database or not. Use the below code on GraphiQL interface and hit the play button: 
    query {
    users (last: 1){
    edges {
      node {
        id,
        username,
        email,
        isActive,
        archived,
        verified,
        secondaryEmail
          }
        }
      }
    }



## You will get the output like that -
    {
      "data": {
        "users": {
          "edges": [
            {
              "node": {
                "id": "VXNlck5vZGU6NQ==",
                "username": "arabindamahato",
                "email": "arabinda@email.com",
                "isActive": true,
                "archived": false,
                "verified": false,
                "secondaryEmail": null
              }
            }
          ]
        }
      }
    }


## To login with the registered user. Use the below code along with correct username and password :

     mutation {
        tokenAuth(username: "arabindamahato", password: "Jhantulal@1994") {
          success,
          errors,
          unarchiving,
          token,
          refreshToken,
          unarchiving,
          user {
            id,
            username,
          }
        }
      }


## After successfully login you will get this type of response : 

    {
      "data": {
        "tokenAuth": {
          "success": true,
          "errors": null,
          "unarchiving": false,
          "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6ImFyYWJpbmRhbWFoYXRvIiwiZXhwIjoxNTk1OTk5MTk4LCJvcmlnSWF0IjoxNT1OTk4ODk4fQ.ap-tUOkQeu2tAtQTlKtmHMHnOMtZr2BjvQMdPzvMCC8",
          "refreshToken": "863d696ef247b1953980662388fda333a363e396",
          "user": {
            "id": "VXNlck5vZGU6NQ==",
            "username": "arabindamahato"
          }
        }
      }
    }