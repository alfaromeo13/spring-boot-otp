# Spring Boot OTP (One time password authentication)

Spring Boot project with demonstration of OTP authentication technique.


## Running the project  
1. Create database with name **otp**
2. Open terminal and navigate to your project
3. Type command **mvn install**
4. Type command **mvn spring-boot:run**

## Check application running state
Route: **http://localhost:8080/**


## Available profiles
- Development profile (dev)
- Production profile (prod)


## Authentication

Route: **/auth/authenticate**  
Method: **POST**  
Content-Type: **application/json**  
Request payload: `{ username: "admin", password: "admin" }`  
Response: `{ id_token: "token_hash" }`

## OTP routes that you can called after getting access token  
1. Generate OTP and send it to e-mail <br>
Route: /api/otp/generate <br>
Method: POST <br>
Empty request body in this case.

2. Validate OTP <br>
Route: /api/otp/validate <br>
Method: POST <br>
Example Request Payload: { "otp": "your otp number" }
<br>


## Packaging for production
1. **mvn clean**  
2. **mvn -Pprod package**


## Changes - Important
**15.07.2022.**  
- Removed OTPResourceController. All Otp logic is processed in AuthenticationController
- Added new column in user table -> _is_otp_required_
- Modified TokenProvided to support logic that first check if otp is required. If OTP is not needed token will be generated
instantly, but if OTP is required token will not be provided to end user (client), email will be sent with OTP code
- OTP can be verified used _/auth/verify_ route in AuthenticationController
