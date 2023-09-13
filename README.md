# Introduction
This document explains how to run an API test with Postman. 

# Summery    
I have Completed an API test of Create Booking, Get Booking Info, Token Generate, Update Booking, Get Update Booking Info, Delete Booking.
https://restful-booker.herokuapp.com
<p align="center">
  <img src="https://github.com/SHANJIDA-HRIDE/API-Testing/assets/62147630/754d1056-5fdd-4d01-952a-28711facf993" />
</p>


Here in this API Booking Info are viewed and different tests are performed like GET, POST, PUT,DELETE.

**Summary:** Test Scripts 4 and a Total of 16 assertions were done. All of them passed with 0 skipped tests. The number of iteration was 1.



# Requirements  
**Java**  
https://www.oracle.com/java/technologies/downloads/   
**Postman**   
https://www.postman.com/   
**Node JS**   
https://nodejs.org/en/    



# Assertions Details    
#### Create Booking
**Body**
```bash
   {
	"firstname" : "{{firstName}}",
	"lastname" : "{{lastName}}",
	"totalprice" : {{price}},
	"depositpaid" : {{paid}},
	"bookingdates" : {
    	"checkin" : "{{checkin}}",
    	"checkout" : "{{checkout}}"
	},
	"additionalneeds" : "{{needs}}"
}

```
**Pre-Request Scripts**
```bash   
var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
console.log("First Name Value:  "+ firstName)
pm.environment.set("firstName",firstName)

var lastName = pm.variables.replaceIn("{{$randomLastName}}")
console.log("Last Name Value:  "+ lastName)
pm.environment.set("lastName",lastName)

var price = pm.variables.replaceIn("{{$randomInt}}")
console.log("Price Value:  "+ price)
pm.environment.set("price",price)

var paid = pm.variables.replaceIn("{{$randomBoolean}}")
console.log("Deposit paid Value:  "+ paid)
pm.environment.set("paid",paid)

const moment = require('moment')
const today = moment()
console.log(today.format("YYYY-MM-DD"))
pm.environment.set("checkin",today.add(1,'d').format("YYYY-MM-DD"))

pm.environment.set("checkout",today.add(5,'d').format("YYYY-MM-DD"))

var needs = pm.variables.replaceIn("{{$randomJobArea}}")
console.log("Additional need Value:  "+ needs)
pm.environment.set("needs",needs)
```
**Test Script**
```bash   
var jsonData = pm.response.json()
pm.environment.set("id", jsonData.bookingid)
```

#### Get Booking Info
**Test Script**
```bash   
var ststuscode = pm.response.code
console.log(ststuscode)

if(ststuscode==200){
var jsonData = pm.response.json()
pm.test("Status code is 200", function(){
    pm.response.to.have.status(200);
});

var code = pm.response.code
console.log(code)
pm.test("Firstname Validate", function(){
    pm.expect(jsonData.firstname).to.eql(pm.environment.get("firstName"));

});

pm.test("Lastname Validate", function(){
    pm.expect(jsonData.lastname).to.eql(pm.environment.get("lastName"));

});

pm.test("Price Validate", function(){
    pm.expect(jsonData.totalprice).to.eql(parseInt(pm.environment.get("price")));

});

pm.test("Deposit paid Validate", function(){
    pm.expect(String(jsonData.depositpaid)).to.eql((pm.environment.get("paid")));

});

pm.test("Date Validate", function(){
    pm.expect(jsonData.bookingdates.checkin).to.eql(pm.environment.get("checkin"));

});

pm.test("Date Validate", function(){
    pm.expect(jsonData.bookingdates.checkout).to.eql(pm.environment.get("checkout"));

});

pm.test("Additional Need Validate", function(){
    pm.expect(jsonData.additionalneeds).to.eql((pm.environment.get("needs")));

});


}

else if(ststuscode==404){

    pm.test("Not Found", function(){
    pm.response.to.have.status(404);
    });
}

else if(ststuscode==200){

    pm.test("OK", function(){
    pm.response.to.have.status(200);
    });
}

else if(ststuscode==201){

    pm.test("Created", function(){
    pm.response.to.have.status(201);
    });
}

else if(ststuscode==202){

    pm.test("Accepted", function(){
    pm.response.to.have.status(202);
    });
}

else if(ststuscode==400){

    pm.test("Bad Request", function(){
    pm.response.to.have.status(400);
    });
}

else if(ststuscode==401){

    pm.test("Unauthorized", function(){
    pm.response.to.have.status(401);
    });
}

else if(ststuscode==403){

    pm.test("Fordidden", function(){
    pm.response.to.have.status(403);
    });
}

else if(ststuscode==405){

    pm.test("Method Not Allowed", function(){
    pm.response.to.have.status(405);
    });
}

else if(ststuscode==500){

    pm.test("Internal Server Error", function(){
    pm.response.to.have.status(500);
    });
}

else if(ststuscode==501){

    pm.test("Not Implimented", function(){
    pm.response.to.have.status(501);
    });
}

else if(ststuscode==502){

    pm.test("Bad Gateway", function(){
    pm.response.to.have.status(502);
    });
}

else if(ststuscode==503){

    pm.test("Service Unavailable", function(){
    pm.response.to.have.status(503);
    });
}

else{
    pm.test("Something Else!!!!")
}
```
 
#### Token Generate  
**Body**
```bash
{
	"username": "admin",
	"password": "password123"
}

```
**Test Script**
```bash
var tokendata = pm.response.json()
pm.environment.set("token", tokendata.token)

```
#### Update Booking Info
**Body**
```bash
{
	"firstname" : "{{firstName}}",
	"lastname" : "{{lastName}}",
	"totalprice" : {{price}},
	"depositpaid" : {{paid}},
	"bookingdates" : {
    	"checkin" : "{{checkin}}",
    	"checkout" : "{{checkout}}"
	},
	"additionalneeds" : "{{needs}}"
}
```
**Pre Request Script**
```bash
var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
console.log("First Name Value:  "+ firstName)
pm.environment.set("firstName",firstName)

var lastName = pm.variables.replaceIn("{{$randomLastName}}")
console.log("Last Name Value:  "+ lastName)
pm.environment.set("lastName",lastName)

var price = pm.variables.replaceIn("{{$randomInt}}")
console.log("Price Value:  "+ price)
pm.environment.set("price",price)

var paid = pm.variables.replaceIn("{{$randomBoolean}}")
console.log("Deposit paid Value:  "+ paid)
pm.environment.set("paid",paid)

const moment = require('moment')
const today = moment()
console.log(today.format("YYYY-MM-DD"))
pm.environment.set("checkin",today.add(1,'d').format("YYYY-MM-DD"))

pm.environment.set("checkout",today.add(5,'d').format("YYYY-MM-DD"))

var needs = pm.variables.replaceIn("{{$randomJobArea}}")
console.log("Additional need Value:  "+ needs)
pm.environment.set("needs",needs)
```

#### Get Update Booking Info
**Test Script**
```bash
var ststuscode = pm.response.code
console.log(ststuscode)

if(ststuscode==200){
var jsonData = pm.response.json()
pm.test("Status code is 200", function(){
    pm.response.to.have.status(200);
});

var code = pm.response.code
console.log(code)
pm.test("Firstname Validate", function(){
    pm.expect(jsonData.firstname).to.eql(pm.environment.get("firstName"));

});

pm.test("Lastname Validate", function(){
    pm.expect(jsonData.lastname).to.eql(pm.environment.get("lastName"));

});

pm.test("Price Validate", function(){
    pm.expect(jsonData.totalprice).to.eql(parseInt(pm.environment.get("price")));

});

pm.test("Deposit paid Validate", function(){
    pm.expect(String(jsonData.depositpaid)).to.eql((pm.environment.get("paid")));

});

pm.test("Date Validate", function(){
    pm.expect(jsonData.bookingdates.checkin).to.eql(pm.environment.get("checkin"));

});

pm.test("Date Validate", function(){
    pm.expect(jsonData.bookingdates.checkout).to.eql(pm.environment.get("checkout"));

});

pm.test("Additional Need Validate", function(){
    pm.expect(jsonData.additionalneeds).to.eql((pm.environment.get("needs")));

});


}

else if(ststuscode==404){

    pm.test("Not Found", function(){
    pm.response.to.have.status(404);
    });
}

else if(ststuscode==200){

    pm.test("OK", function(){
    pm.response.to.have.status(200);
    });
}

else if(ststuscode==201){

    pm.test("Created", function(){
    pm.response.to.have.status(201);
    });
}

else if(ststuscode==202){

    pm.test("Accepted", function(){
    pm.response.to.have.status(202);
    });
}

else if(ststuscode==400){

    pm.test("Bad Request", function(){
    pm.response.to.have.status(400);
    });
}

else if(ststuscode==401){

    pm.test("Unauthorized", function(){
    pm.response.to.have.status(401);
    });
}

else if(ststuscode==403){

    pm.test("Fordidden", function(){
    pm.response.to.have.status(403);
    });
}

else if(ststuscode==405){

    pm.test("Method Not Allowed", function(){
    pm.response.to.have.status(405);
    });
}

else if(ststuscode==500){

    pm.test("Internal Server Error", function(){
    pm.response.to.have.status(500);
    });
}

else if(ststuscode==501){

    pm.test("Not Implimented", function(){
    pm.response.to.have.status(501);
    });
}

else if(ststuscode==502){

    pm.test("Bad Gateway", function(){
    pm.response.to.have.status(502);
    });
}

else if(ststuscode==503){

    pm.test("Service Unavailable", function(){
    pm.response.to.have.status(503);
    });
}

else{
    pm.test("Something Else!!!!")
}
``` 

#### Delete Booking
**Headers**
```bash
Cookie
token={{token}}

 ``` 

# Create Test Suites   

### Using Newman   


  Newman is a command-line Collection Runner for Postman. It enables you to run and test a Postman Collection directly from the command line.
#### Install Command    
```bash
npm install -g newman    
```
#### Run Command    
- newman run “Path/CollectionName.json” -e Path/EnvironmentName.json
- newman run “Collection Link” -e “Path”/EnvironmentName.json    

#### Create HTML Report  
 
#### Install Command      
```bash
npm install -g newman-reporter-html
```
**or**   
```bash
npm install -g newman-reporter-htmlextra    
```
#### Run Command      
- newman run “Collection Link” -e “Path”/EnvironmentName.json -r cli,html    
**or**    
- newman run “Collection Link” -e “Path”/EnvironmentName.json -r cli,htmlextra

- #### Newman File htmlextra
 <p align="center">
	 <img src="https://github.com/SHANJIDA-HRIDE/API-Testing/assets/62147630/46299173-ee26-45c2-b534-62e3cccce636"/>
	 <img src="https://github.com/SHANJIDA-HRIDE/API-Testing/assets/62147630/58d92bec-9538-46b6-b56f-2bb42bac130d"/>
	 <img src="https://github.com/SHANJIDA-HRIDE/API-Testing/assets/62147630/a771c8c0-630d-4f52-b571-ed01ac926e65"/>
	 <img src="https://github.com/SHANJIDA-HRIDE/API-Testing/assets/62147630/439b6ae9-278a-4ca8-a6a5-b59c59f6a7cf"/>
	 <img src="https://github.com/SHANJIDA-HRIDE/API-Testing/assets/62147630/e938d3f9-207c-47e0-a789-819f113a41b7"/>
	 <img src="https://github.com/SHANJIDA-HRIDE/API-Testing/assets/62147630/eb6e220b-892d-45ef-9ca0-10b55c648e64"/>
 </p>
