## API Testing
API Testing is a type of software testing that focuses on verifying the functionality, reliability, performance, and security of application programming interfaces (APIs). APIs allow different software systems to communicate with each other, and API testing ensures that this communication works as intended.

## Rest Booking API Testing with Postman Newman 
This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API. 

### **Features**

- Tests for GET, POST, PUT, DELETE requests
- Collection of tests covering different API endpoints
- Environment setup for easy switching between environments
- Pre-request scripts for data setup
- Test scripts for assertions and validations

## API Documentation:
- [https://documenter.getpostman.com/view/13082503/2sA2xmUAJ1](https://www.postman.com/ggh555/api-testing/documentation/dy6fuue/jasmin-sqa?workspaceId=90b9b583-89de-431c-98c6-40f403bb1efd)
  
### **Technology used:**
- Postman
- Newman

### **Prerequisite:**
- Node Js
- Newman
- Newman Html Report Library

### **Installation**

1. Postman: If you haven't already, [download and install Postman.](https://www.postman.com/downloads/)
2. Clone the repository:
 ```console 
  git clone https://github.com/jasminakterr/API-Testing-of-Rest-Booking-API-with-Postman-Newman.git
```
3. Import the Postman collection:
    - Open Postman.
    - Click on the Import button.
    - Select the file from the repository.
4. Import the Postman environment:
    - In Postman, click on the gear icon in the top right corner.
    - Select **Import** and choose the file.
5. Newman and Report Installation Process:
    - Newman Install Command:
     ```console 
      npm install -g newman
    ```
    - Newman Html Report Install Command:
     ```console 
      npm install -g newman-reporter-htmlextra
    ```
### **Usage**
1. Select Environment:
    -   In Postman, select the appropriate environment (e.g., Development, Production) from the top-right dropdown.
3. Run Collection:
    -   Select the imported collection from the Collections sidebar.
    -   Click on the Runner button to open the collection runner.
    -   Select the desired environment.
    -   Click Start Test to run the collection.
8. View Results:
    -   Once the tests are complete, view the results in the Runner tab.
    -   Detailed test results can be viewed for each request.

## **Testing**

## Test Case Scenarios:

## _**1. Create New Booking**_

### Request URL: https://restful-booker.herokuapp.com/booking/
### Request Method: POST
### Pre-request Script:
```console 
    var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
    pm.environment.set("firstName", firstName)
    console.log("First Name Value "+firstName)
    
    var lastName = pm.variables.replaceIn("{{$randomLastName}}")
    pm.environment.set("lastName", lastName)
    console.log("Last Name Value "+lastName)
    
    var totalPrice = pm.variables.replaceIn("{{$randomInt}}")
    pm.environment.set("totalPrice", totalPrice)
    console.log(totalPrice)
    
    var depositPaid = pm.variables.replaceIn("{{$randomBoolean}}")
    pm.environment.set("depositPaid", depositPaid)
    console.log(depositPaid)
    
    //Date
    const moment = require('moment')
    const today = moment()
    pm.environment.set("checkin", today.add(1,'d').format("YYYY-MM-DD"))
    pm.environment.set("checkout",today.add(7,'d').format("YYYY-MM-DD") )
    
    var additionalNeeds = pm.variables.replaceIn("{{$randomNoun}}")
    pm.environment.set("additionalNeeds", additionalNeeds)
```
  **Request Body:** 
 ```console 
  {
	  "firstname" : "{{firstName}}",
	  "lastname" : "{{lastName}}",
	  "totalprice" : {{totalPrice}},
	  "depositpaid" : {{depositPaid}},
	  "bookingdates" : {
    	  "checkin" : "{{checkin}}",
    	  "checkout" : "{{checkout}}"
	  },
	  "additionalneeds" : "{{additionalNeeds}}"
  }
```
  **Response Body:**
 ```console 
  "bookingid": 423,
    "booking": {
        "firstname": "Neha",
        "lastname": "Altenwerth",
        "totalprice": 440,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "2024-11-24",
            "checkout": "2024-12-01"
        },
        "additionalneeds": "protocol"
    }
}
```
 ## _**2. Get Booking Details By ID**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: GET
### Response Body:
 ```console 
{
    "firstname": "Neha",
    "lastname": "Altenwerth",
    "totalprice": 440,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2024-11-24",
        "checkout": "2024-12-01"
    },
    "additionalneeds": "protocol"
}
```
## _**3. Create A Token For Authentication.**_
### Request URL: https://restful-booker.herokuapp.com/auth
### Request Method: POST
### Pre-request Script: None
### Request Body:
 ```console 
{
	"username": "admin",
	"password": "password123"
}
```
  **Response Body:**
 ```console 
{
    "token": "d2e639d2d451067"
}
```

 ## _**4. Update the Booking Details**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: PUT
### Pre-request Script:
```console 
    //********** First name generate *********//
var updated_firstName = pm.variables.replaceIn("{{$randomFirstName}}")
console.log(updated_firstName)
pm.environment.set("updated_firstName", updated_firstName)
//********** Last name generate *********// 
var updated_lastName = pm.variables.replaceIn("{{$randomLastName}}")
console.log(updated_lastName)
pm.environment.set("updated_lastName", updated_lastName)
//********** Total price generate *********// 
var updated_totalPrice = pm.variables.replaceIn("{{$randomInt}}")
console.log(updated_totalPrice)
pm.environment.set("updated_totalPrice", updated_totalPrice)
//********** Deposit paid generate *********//
var Updated_depositPaid = pm.variables.replaceIn("{{$randomBoolean}}")
console.log(Updated_depositPaid)
pm.environment.set("Updated_depositPaid", Updated_depositPaid)
//********** Booking date generate *********//
const moment = require('moment')
const today = moment()
//********** Checkin date generate *********//
pm.environment.set("updated_checkin", today.add(1,'d').format("YYYY-MM-DD"))
//********** Checkout date generate *********//
pm.environment.set("updated_checkout",today.add(7,'d').format("YYYY-MM-DD") )
//********** Additional needs generate *********//    
var updated_additionalNeeds = pm.variables.replaceIn("{{$randomNoun}}")
console.log(updated_additionalNeeds)
pm.environment.set("updated_additionalNeeds", updated_additionalNeeds)
```
  **Request Body:** 
 ```console 
  {
	"firstname" : "{{updated_firstName}}",
	"lastname" : "{{updated_lastName}}",
	"totalprice" : {{updated_totalPrice}},
	"depositpaid" : {{Updated_depositPaid}},
	"bookingdates" : {
    	"checkin" : "{{updated_checkin}}",
    	"checkout" : "{{updated_checkout}}"
	},
	"additionalneeds" : "{{updated_additionalNeeds}}"
}

```
  **Response Body:**
 ```console 
 {
    "firstname": "Opal",
    "lastname": "Bergnaum",
    "totalprice": 635,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2024-11-24",
        "checkout": "2024-12-01"
    },
    "additionalneeds": "array"
}
```

 ## _**5. Delete Booking Record**_

### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: DELETE
### Response Body: None 

## Run Command:  
- Run Command for Console: 
```console 
newman run Jasmin.postman_collection.json -e Practice.postman_environment.json
```
- Run Command for Report: 
```console 
newman run Jasmin.postman_collection.json -e Practice.postman_environment.json -r htmlextra
```

## Newman Report Summary:
![Report 1](https://github.com/user-attachments/assets/627c3a6a-16e7-4095-bcb0-7d9f5b836ca4)

![Report 2](https://github.com/user-attachments/assets/2a96b220-f87b-49ed-a18e-e5d6291a5c1e)

![Report 3](https://github.com/user-attachments/assets/b55671ff-1afa-4668-8ba6-3acce8dc2754)

![Report 4](https://github.com/user-attachments/assets/e4f1b0d0-1d26-422a-90a1-34e53e10900a)


