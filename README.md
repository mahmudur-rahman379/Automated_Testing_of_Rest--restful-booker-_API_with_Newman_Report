# Automated_Testing_of_Rest--restful-booker-_API_with_Newman_Report
### **Rest Booking API Testing with Postman Newman**
This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API. 

### **Features**

- Tests for GET, POST, PUT, DELETE requests
- Collection of tests covering different API endpoints
- Environment setup for easy switching between environments
- Pre-request scripts for data setup
- Test scripts for assertions and validations

## API Documentation:
- https://documenter.getpostman.com/view/33497263/2sA3e5f8bv
  
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
  git clone https://github.com/mahmudur-rahman379/Automated_Testing_of_Rest--restful-booker-_API_with_Newman_Report.git
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

## _**1. Create_booking info**_

### Request URL: https://restful-booker.herokuapp.com/booking/
### Request Method: POST
### Pre-request Script:
```console 
    var responseid = pm.response.code
console.log(responseid)

if (responseid ==200 )
{
var resdata = pm.response.json()
pm.environment.set("id",resdata.bookingid)
}
else if (responseid== 404){
    pm.test("Not Found")
}
else if(responseid== 403){
    pm.test("Forbidden")
}
```
  **Request Body:** 
 ```console 
  {
	"firstname" : "{{firstname}}",
	"lastname" : "{{lastname}}",
	"totalprice" : "{{randomtotalprice}}",
	"depositpaid" : "{{$randomBoolean}}",
	"bookingdates" : {
    	"checkin" : "{{checkin}}",
    	"checkout" : "{{checkout}}"
	},
	"additionalneeds" : "{{$randomColor}}"
}
```
  **Response Body:**
 ```console 
  {
    "bookingid": 3239,
    "booking": {
        "firstname": "Trever",
        "lastname": "Fisher",
        "totalprice": 517,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "2024-07-19",
            "checkout": "2024-07-16"
        },
        "additionalneeds": "cyan"
    }
```
 ## _**2. Get_booking info**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: GET
### Pre-request Script:
```### Pre-request Script:
```console 
   var respponsecode = pm.response.code
console.log(respponsecode)

if (respponsecode ==200 )
{
var resdata = pm.response.json()
pm.test("First Name Validation"),function(){
pm.expect(pm.environment.get("firstname")).to.eql(resdata.booking.firstname)
}

pm.test("Last Name Validation"),function(){
    pm.expect(pm.environment.get("lastname")).to.eql(resdata.booking.lastname)
}

pm.test("Total Price Validation"),function(){
    pm.expect(pm.environment.get("randomtotalprice")).to.eql(resdata.booking.totalprice)
}

pm.test("DepositPaid Validation"),function(){
pm.expect(pm.environment.get("randomdepositpaid")).to.eql(resdata.booking.depositpaid)
}

pm.test("Checkin Date Validation"),function(){
    pm.expect(pm.environment.get("checkin")).to.eql(resdata.booking.bookingdates.checkin)
}
pm.test("Checkout Date Validation"),function(){
    pm.expect(pm.environment.get("checkout")).to.eql(resdata.booking.bookingdates.checkout)
}

pm.test("Additionalneeds Validation"),function(){
    pm.expect(pm.environment.get("radditionalneeds")).to.eql(resdata.booking.additionalneeds)}
}
else if (respponsecode== 404){
    pm.test("Not Found")
}
else if(respponsecode== 403){
    pm.test("Forbidden")
}
```
### Response Body:
 ```console 
{
    "firstname": "Trever",
    "lastname": "Fisher",
    "totalprice": 517,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2024-07-19",
        "checkout": "2024-07-16"
    },
    "additionalneeds": "cyan"
}
```
## _**3. Authorizer's Token**_
### Request URL: https://restful-booker.herokuapp.com/auth
### Request Method: POST
### Pre-request Script:None
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
    "token": "06eb798bf6f2caa"
}
```

 ## _**4. Update_booking info**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: PUT
### Pre-request Script:
```console 
    var newfirstname =pm.variables.replaceIn("{{$randomFirstName}}")
console.log(newfirstname)
pm.environment.set("update_firstname",newfirstname);
 
 var newlastname =pm.variables.replaceIn("{{$randomLastName}}")
 console.log(newlastname)
pm.environment.set("update_lastname",newlastname)

var newrandomtotalprice = pm.variables.replaceIn("{{$randomInt}}")
console.log(newrandomtotalprice)
pm.environment.set("update_randomtotalprice",newrandomtotalprice)

var newrandomdepositpaid = pm.variables.replaceIn("{{$randomBoolean}}")
console.log(newrandomdepositpaid)
pm.environment.set("update_randomdepositpaid",newrandomdepositpaid)

//date
const date = require('moment')
const today= date()
var newcheckin = today.add(5,'d').format("YYYY-MM-DD")
console.log(newcheckin)
pm.environment.set("updatecheckin",newcheckin)
var newcheckout= today.subtract(3,'d').format("YYYY-MM-DD")
console.log(newcheckout)
pm.environment.set("updatecheckout",newcheckout)

var newadditionalneeds = pm.variables.replaceIn("{{$randomColor}}")
pm.environment.set("update_radditionalneeds",newadditionalneeds)
console.log(newadditionalneeds)

```
  **Request Body:** 
 ```console 
  {
	  {
    "firstname": "{{update_firstname}}",
    "lastname": "{{update_lastname}}",
    "totalprice": "{{update_randomtotalprice}}",
    "depositpaid": "{{update_randomdepositpaid}}",
    "bookingdates": {
        "checkin": "{{updatecheckin}}",
        "checkout": "{{updatecheckout}}"
    },
    "additionalneeds": "{{update_radditionalneeds}}"
}

```
  **Response Body:**
 ```console 
  {
      "bookingid": 4334,
      "booking": {
          "firstname": "Joelle",
          "lastname": "Krajcik",
          "totalprice": 266,
          "depositpaid": true,
          "bookingdates": {
              "checkin": "2024-03-15",
              "checkout": "2024-03-20"
          },
          "additionalneeds": "monitor"
      }
  }
```

 ## _**5.Delete_booking info**_

### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: GET
### Post Response Body:
```console 
  {
var rescode= pm.response.code
console.log(rescode)

if (rescode ==200 )
{
var resdata = pm.response.json()
pm.test(" Update First Name Validation"),function(){
pm.expect(pm.environment.get("update_firstnamefirstname")).to.eql(resdata.booking.firstname)
}

pm.test("Update Last Name Validation"),function(){
    pm.expect(pm.environment.get("update_lastname")).to.eql(resdata.booking.lastname)
}

pm.test("Update Total Price Validation"),function(){
    pm.expect(pm.environment.get("update_randomtotalprice")).to.eql(resdata.booking.totalprice)
}

pm.test("Update DepositPaid Validation"),function(){
pm.expect(pm.environment.get("update_randomdepositpaid")).to.eql(resdata.booking.depositpaid)
}

pm.test("Update Checkin Date Validation"),function(){
    pm.expect(pm.environment.get("updatecheckin")).to.eql(resdata.booking.bookingdates.checkin)
}
pm.test("Update Checkout Date Validation"),function(){
    pm.expect(pm.environment.get("updatecheckout")).to.eql(resdata.booking.bookingdates.checkout)
}

pm.test("Update Additionalneeds Validation"),function(){
    pm.expect(pm.environment.get("Update radditionalneeds")).to.eql(resdata.booking.additionalneeds)}
}
else if (respponsecode== 404){
    pm.test("Not Found")
}
else if(respponsecode== 403){
    pm.test("Forbidden")
}
 }
```
 ## _**6.Delete_booking info**_

### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: DELETE
### Post Response Body: @01 CREATED
  
## _**7.Check deleted successfully**_

### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: GET
### Post Response Body:
## Post Script :
```console 
  {
var respponsecode = pm.response.code
console.log(respponsecode)

if (respponsecode ==200 )
{
var resdata = pm.response.json()
pm.test("First Name Validation"),function(){
pm.expect(pm.environment.get("firstname")).to.eql(resdata.booking.firstname)
}

pm.test("Last Name Validation"),function(){
    pm.expect(pm.environment.get("lastname")).to.eql(resdata.booking.lastname)
}

pm.test("Total Price Validation"),function(){
    pm.expect(pm.environment.get("randomtotalprice")).to.eql(resdata.booking.totalprice)
}

pm.test("DepositPaid Validation"),function(){
pm.expect(pm.environment.get("randomdepositpaid")).to.eql(resdata.booking.depositpaid)
}

pm.test("Checkin Date Validation"),function(){
    pm.expect(pm.environment.get("checkin")).to.eql(resdata.booking.bookingdates.checkin)
}
pm.test("Checkout Date Validation"),function(){
    pm.expect(pm.environment.get("checkout")).to.eql(resdata.booking.bookingdates.checkout)
}

pm.test("Additionalneeds Validation"),function(){
    pm.expect(pm.environment.get("radditionalneeds")).to.eql(resdata.booking.additionalneeds)}
}
else if (respponsecode== 404){
    pm.test("Not Found")
}
else if(respponsecode== 403){
    pm.test("Forbidden")
}
 }
```

- Run Command for Console: 
```console 
newman run Sampletest_Mahmudur(restfu_booker).postman_collection.json -e Sampletest_Mahmudur(restful_booker).postman_environment.json
```
- Run Command for Report: 
```console 
newman run Sampletest_Mahmudur(restfu_booker).postman_collection.json -e Sampletest_Mahmudur(restful_booker).postman_environment.json -r cli,htmlextra
```

## Newman Report Summary:
![Screenshot_2](https://github.com/user-attachments/assets/12587b85-ffbd-43be-b21d-31cd7e67ef61)
![Screenshot_3](https://github.com/user-attachments/assets/a31b5beb-0dc5-49e1-8ef2-f3ff3e3fa80a)

