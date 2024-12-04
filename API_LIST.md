# goKraken.net Service Interface API List

# 1\. Introduction

- - -

## 1.1 Purpose

* Passes the Atlas Backend API framework feature items.    

# 2\. Authorization API

- - -

## 2.1 POST atlas/auth/sign-up

* This is an email-based membership registration API.    

### 2.1.1 Request

**Info**

|     |     |     |
| --- | --- | --- |
| **Info** |     |     |
| Method | `POST` |     |
| Content-Type | `application/json` |     |
| **Body** |     |     |
| **Key** | **Type** | **Description** |
| `email` | `string` | User Email |
| `password` | `string` | User Password<br><br>* At least 10 characters<br> <br>* Contains at least 1 uppercase and lowercase letter<br> <br>* Contains at least 1 special character<br> <br>* Contains at least 1 number |
| `nickname` | `string` | User nickname |

### 2.1.2 Response

#### 2.1.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 201 | Membership registration completed | |
| **Body** |     |     |
| **key** | **Type** | **Description** |
|     |     |     |

#### 2.1.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 400 | * If the input is invalid | |
| 409 | * If the email is duplicated | |
| 500 | * Email external module error or unexpected error | |
| **Body** |     |     |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |
- - -

## 2.2 POST atlas/auth/sign-In

* This is an email-based login API.    

### 2.2.1 Request

**Info**

|     |     |     |
| --- | --- | --- |
| **Info** |     |     |
| Method | `POST` |     |
| Content-Type | `application/json` |     |
| **Body** |     |     |
| **Key** | **Type** | **Description** |
| `id` | `string` | User Email |
| `password` | `string` | User Password (10 characters or more) |

### 2.2.2 Response

#### 2.2.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 201 | Login Complete | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `accessToken` | `string` | accessToken information including account, session information (Expire: 1h)<br><br>Ex)<br><br>`{ accessToken: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIwMUo2NlYwS0hXQzMyMThTOUEyVzE2RlQ0MSIsInJvbGUiOiJTVVBFUl9BRE1JTiIsImlhdCI6MTcyNTg0MzYxNiwiZXhwIjoxNzI1OTMwMDE2fQ.ggTmD5JnjvZa-CwOQqIt_fnclrzHORAxVMfwdcWD0v8" }` |
| `refreshToken` | `string` | refreshToken information including session information (Expire: 14d)<br><br>Ex)<br><br>`{ "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIwMUo4NkVNTUpGUVhUU1dYWFFOUjI1TUhLVyIsInNlc3Npb25JZCI6Ijg4Mzk1NjdjLTljOTktNGQxMy1hZWNlLTIwMDZmYTg3OTJlNiIsImlhdCI6MTcyNjc5MzUzNiwiZXhwIjoxNzI4MDAzMTM2fQ.XNUDCHAHd7z1v4HiGW9E1rLwFqr6Hntxe2Y33FNyyc8" }` |

Response Body Example

`{ "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIwMUo4NkVNTUpGUVhUU1dYWFFOUjI1TUhLVyIsInJvbGUiOiJTVVBFUl9BRE1JTiIsInNlc3Npb25JZCI6Ijg4Mzk1NjdjLTljOTktNGQxMy1hZWNlLTIwMDZmYTg3OTJlNiIsImlhdCI6MTcyNjc5MzUzNiwiZXhwIjoxNzI2Nzk3MTM2fQ.mqR9R3xHoEpwcsJGYTBkzr_98XggeIAHjnU1JSuVEtg", "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIwMUo4NkVNTUpGUVhUU1dYWFFOUjI1TUhLVyIsInNlc3Npb25JZCI6Ijg4Mzk1NjdjLTljOTktNGQxMy1hZWNlLTIwMDZmYTg3OTJlNiIsImlhdCI6MTcyNjc5MzUzNiwiZXhwIjoxNzI4MDAzMTM2fQ.XNUDCHAHd7z1v4HiGW9E1rLwFqr6Hntxe2Y33FNyyc8" }`

#### 2.2.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 401 | * If the email address is incorrect<br> <br>* If the password is incorrect | |
| 403 | * Email authentication has not been completed. | |
| 409 | * If the user signed up with Google Social Login | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |
- - -

## 2.3 POST atlas/auth/sign-out

* This is a logout API.

* Expires the session and expires the tokens.

### 2.3.1 Request

**Info**

|     |     |
| --- | --- |
| **Info** |     |
| Method | `POST` |
| Content-Type | `application/json` |
| **Header** |     |
| `Authorization` | Token information including account information<br><br>* “Bearer `accessToken`” |

### 2.3.2 Response

#### 2.3.2.1 Success

**Code**

|     |     |
| --- | --- |
| **Code** |     |
| **Code** | **Description** |
| 200 | Logout complete |

#### 2.3.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 401 | * In case of invalid token | |
| 500 | * Unexpected system error | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |

- - -

## 2.4 POST atlas/auth/confirmation-emails/resend

* This is an API for resending authentication emails.    

### 2.4.1 Request

**Info**

|     |     |     |
| --- | --- | --- |
| **Info** |     |     |
| Method | `POST` |     |
| Content-Type | `application/json` |     |
| **Body** |     |     |
| **Key** | **Type** | **Description** |
| `email` | `string` | User Email |

### 2.4.2 Response

#### 2.4.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 201 | Verification email resend complete | |
| **Body** |     |     |
| **key** | **Type** | **Description** |
|     |     |     |

#### 2.4.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 404 | * If there is no member corresponding to the email | |
| 500 | * If an email external module error or an unexpected error occurs | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |

- - -

## 2.5 GET atlas/auth/confirm-email

* This is an email authentication API.    

### 2.5.1 Request

**Info**

|     |     |     |
| --- | --- | --- |
| **Info** |     |     |
| Method | `GET` |     |
| Content-Type | `application/json` |     |
| **Query** |     |     |
| **Key** | **Type** | **Description** |
| `email` | `string` | User Email |
| `userId` | `string` | Unique user identifier value (uuid) |

### 2.5.2 Response

#### 2.5.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 200 | 이메일 인증 완료 |     |
| **Body** |     |     |
| **key** | **Type** | **Description** |
|     |     |     |

#### 2.5.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 400 | * If email authentication fails | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |
- - -

## 2.6 GET atlas/auth/confirm-invite-email

* This is a group invitation authentication API.    

### 2.6.1 Request

**Info**

|     |     |     |
| --- | --- | --- |
| **Info** |     |     |
| Method | `GET` |     |
| Content-Type | `application/json` |     |
| **Query** |     |     |
| **Key** | **Type** | **Description** |
| `email` | `string` | 사용자 Email |
| `userId` | `string` | Unique user identifier value (uuid) |
| `groupId` | `string` | Unique group identifier value (uuid) |

### 2.6.2 Response

#### 2.6.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 200 | Membership withdrawal completed | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `email` | `string` | `email` value of the member who withdrew |

#### 2.6.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 401 | * If the token value is invalid | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |

- - -

## 2.7 POST atlas/auth/reset-password

* This is a password reset API.    

### 2.7.1 Request

**Info**

|     |     |     |
| --- | --- | --- |
| **Info** |     |     |
| Method | `POST` |     |
| Content-Type | `application/json` |     |
| **Body** |     |     |
| **Key** | **Type** | **Description** |
| `email` | `string` | User Email |
### 2.7.2 Response

#### 2.7.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 201 | Temporary password email sent | |
| **Body** |     |     |
| **key** | **Type** | **Description** |
|     |     |     |

#### 2.7.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 404 | * If the user with email fails to be retrieved | |
| 500 | * If an error occurs in the email sending module | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |

- - -

## 2.8 PATCH atlas/auth/password

* This is a password change API.    

### 2.8.1 Request

**Info**

|     |     |     |
| --- | --- | --- |
| **Info** |     |     |
| Method | `POST` |     |
| Content-Type | `application/json` |     |
| **Header** |     |     |
| `Authorization` | Token information including account information<br><br>* “Bearer `accessToken`” | |
| **Key** | **Type** | **Description** |
| `password` | `string` | Password to change |

### 2.8.2 Response

#### 2.8.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 200 | Password change completed | |
| **Body** |     |     |
| **key** | **Type** | **Description** |
|     |     |     |

#### 2.8.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 400 | * If the input value is invalid | |
| 404 | * If the user with userId fails to be retrieved | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |

- - -

## 2.9 DELETE atlas/auth/user

* This is a membership withdrawal API.    

### 2.9.1 Request

**Info**

|     |     |     |
| --- | --- | --- |
| **Info** |     |     |
| Method | `DELETE` |     |
| Content-Type | `application/json` |     |
| **Header** |     |     |
| `Authorization` | Token information including account information<br><br>* “Bearer `accessToken`” | |
| **Key** | **Type** | **Description** |
|     |     |     |

### 2.9.2 Response

#### 2.9.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 200 | Membership withdrawal completed | |
| **Body** |     |     |
| **key** | **Type** | **Description** |
|     |     |     |

#### 2.9.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 401 | * If the token value is invalid | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |
- - -

## 2.10 POST atlas/auth/google

* This is Google Social Login API.    

### 2.10.1 Request

**Info**

|     |     |     |
| --- | --- | --- |
| **Info** |     |     |
| Method | `POST` |     |
| Content-Type | `application/json` |     |
| **Key** | **Type** | **Description** |
| `idToken` | `string` | Google Social Login idToken value |
### 2.10.2 Response

#### 2.10.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 201 | Google Social Login Complete | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `accessToken` | `string` | accessToken information including account and session information (Expire: 1h)<br><br>Ex) |
| `refreshToken` | `string` | refreshToken information including session information (Expire: 14d)<br><br>Ex) |

Response Body Example

#### 2.10.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 401 | * If Google authentication information is invalid | |
| 409 | * If you have already signed up with the same email | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |

- - -

## 2.11 POST atlas/refresh/accessToken

* This is an accessToken reissue API.    

### 2.11.1 Request

**Info**

|     |     |
| --- | --- |
| **Info** |     |
| Method | `POST` |
| Content-Type | `application/json` |
| **Header** |     |
| `Authorization` | Token information including account information<br><br>* “Bearer `refreshToken`” |
### 2.11.2 Response

#### 2.11.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 200 | accessToken reissue success | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `accessToken` | `string` | accessToken information including account and session information (Expire: 1h)<br><br>Ex) |
#### 2.11.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 401 | * If an invalid refreshToken is used | |
| 500 | * Unexpected system error | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |

- - -

## 2.12 GET atlas/me

* This is my information inquiry API.    

### 2.12.1 Request

**Info**

|     |     |     |
| --- | --- | --- |
| **Info** |     |     |
| Method | `GET` |     |
| Content-Type | `application/json` |     |
| **Header** |     |     |
| `Authorization` | Token information including account information<br><br>* “Bearer `accessToken`” | |
| **Key** | **Type** | **Description** |
| `idToken` | `string` | Google Social Login idToken value |

### 2.12.2 Response

#### 2.12.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 200 | My information search success | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `nickname` | `string` | Current user's `nickname` value |
| `email` | `string` | Current user's `email` value |

#### 2.12.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 404 | * If there is no member | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |

- - -

# 3\. AI Model Creation API

- - -

## 3.1 POST /atlas/item/decal

* Send a request to create a 3D model (\*.glb) using the Decal AI model.    
    

### 3.1.1 Request

**Info**

|     |     |     |
| --- | --- | --- |
| **Info** |     |     |
| Method | `POST` |     |
| Content-Type | `multipart/form-data` |     |
| **Header** |     |     |
| `Authorization` | Token information including account information<br><br>* “Bearer `accessToken`” | |
| **Body** | | |
| **Key** | **Type** | **Description** |
| `itemName` | `string` | Item name |
| `deviceType` | `string` | Recording device type (currently only android) |
| `fileName` | `string` | Input video file name (considering whether to remove it by defining inputFormat name rules) |
| `payLoad` | `file` | Input video file (mp4, 20~60 seconds) |

### 3.1.2 Response

#### 3.1.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 201 | 3D Model Creation Request Completed | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `requestId` | `string` | Unique ID of the item to be created |

#### 3.1.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 400 | * Invalid request syntax<br> <br>* Error while creating compressed file<br> <br>* Duplicate uuid error for requestId<br> <br>* Error when the corresponding item already exists | |
| 401 | * Invalid Token information | |
| 500 | * External module error (DB) | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |

- - -

## 3.2 POST /atlas/item/nerf2mesh

* Send a request to create a 3D model (\*.glb) using the Nerf2mesh AI model.  

### 3.2.1 Request

**Info**

|     |     |     |
| --- | --- | --- |
| **Info** |     |     |
| Method | `POST` |     |
| Content-Type | `multipart/form-data` |     |
| **Header** |     |     |
| `Authorization` | Token information including account information<br><br>* “Bearer `accessToken`” | |
| **Body** | | |
| **Key** | **Type** | **Description** |
| `resize` | `boolean` | Change the resolution of the input video (if 1, change the resolution of the input video to HD) |
| `itemName` | `string` | Item name |
| `Epoch` | `number` | Number of learning times (Stage 0 & 1 Epoch, 1 <= Epoch <= 100) |
| `payLoad` | `file` | Input video file (mp4)<br><br>* Length: 20 seconds ~ 180 seconds<br> <br>* Resolution: HD ~ FHD<br> <br>* Capacity: 50MB ~ 300MB |

### 3.2.2 Response

#### 3.2.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 201 | 3D Model Creation Request Completed | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `requestId` | `string` | Unique ID of the item to be created |

#### 3.2.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 400 | * Invalid request syntax<br> <br>* Error while creating compressed file<br> <br>* Duplicate uuid error for requestId<br> <br>* Error when the corresponding item already exists | |
| 401 | * Invalid Token information | |
| 500 | * External module error (DB) | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |

- - -

## 3.3 POST /atlas/item/musepose

* Send a request to create a 3D model (\*.glb) using the musepose AI model.
### 3.3.1 Request

**Info**

|     |     |     |
| --- | --- | --- |
| **Info** |     |     |
| Method | `POST` |     |
| Content-Type | `multipart/form-data` |     |
| **Header** |     |     |
| `Authorization` | Token information including account information<br><br>* “Bearer `accessToken`” | |
| **Body** | | |
| **Key** | **Type** | **Description** |
| `itemName` | `string` | Item name |
| `Epoch` | `number` | Number of learning (Stage 0 & 1 Epoch, 1 <= Epoch <= 100) |
| `Image` | `file` | Input image file<br><br>* File extension: png \| jpg \| jpeg<br> <br>* Resolution: Vertical image<br> <br>* Size: Less than 10MB |
| `payLoad` | `file` | Input video file (mp4)<br><br>* Length: Less than 20 seconds<br> <br>* Resolution: Vertical video<br> <br>* Size: Less than 20MB |

### 3.3.2 Response

#### 3.3.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 201 | 3D Model Creation Request Completed | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `requestId` | `string` | Unique ID of the item to be created |

#### 3.3.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 400 | * Invalid request syntax<br> <br>* Error while creating compressed file<br> <br>* Duplicate uuid error for requestId<br> <br>* Error when the corresponding item already exists | |
| 401 | * Invalid Token information | |
| 500 | * External module error (DB) | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |

- - -

## 3.4 POST /atlas/item/instant-mesh

* Send a request to create a 3D model (\*.glb) using the instant-mesh AI model.    

### 3.4.1 Request

**Info**

|     |     |     |
| --- | --- | --- |
| **Info** |     |     |
| Method | `POST` |     |
| Content-Type | `multipart/form-data` |     |
| **Header** |     |     |
| `Authorization` | Token information including account information<br><br>* “Bearer `accessToken`” | |
| **Body** | | |
| **Key** | **Type** | **Description** |
| `itemName` | `string` | Item name |
| `Epoch` | `number` | Number of learning (Stage 0 & 1 Epoch, 1 <= Epoch <= 100) |
| `Image` | `file` | Input image file<br><br>* File extension: png \| jpg \| jpeg<br> <br>* Resolution: 300 \* 300 or more<br> <br>* Capacity: 10mb or less |

### 3.4.2 Response

#### 3.4.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 201 | 3D Model Creation Request Completed | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `requestId` | `string` | Unique ID of the item to be created |

#### 3.4.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 400 | * Invalid request syntax<br> <br>* Error while creating compressed file<br> <br>* Duplicate uuid error for requestId<br> <br>* Error when the corresponding item already exists | |
| 401 | * Invalid Token information | |
| 500 | * External module error (DB) | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |

- - -

## 3.5 POST /atlas/item/gs3d

* Send a request to create a 3D model (\*.ply) using the Gaussian-Splatting AI model.
  
### 3.5.1 Request

**Info**

|     |     |     |
| --- | --- | --- |
| **Info** |     |     |
| Method | `POST` |     |
| Content-Type | `multipart/form-data` |     |
| **Header** |     |     |
| `Authorization` | Token information including account information<br><br>* “Bearer `accessToken`” | |
| **Body** | | |
| **Key** | **Type** | **Description** |
| `itemName` | `string` | Item name |
| `Epoch` | `number` | Number of learning (Stage 0 & 1 Epoch, 1 <= Epoch <= 100) |
| `Payload` | `file` | Input video file<br><br>* File extension: mp4<br> <br>* Resolution: FHD or lower<br> <br>* Capacity: 300mb or lower<br> <br>* Length: 180 seconds or less |

### 3.5.2 Response

#### 3.5.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 201 | 3D Model Creation Request Completed | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `requestId` | `string` | Unique ID of the item to be created |

#### 3.5.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 400 | * Invalid request syntax<br> <br>* Error while creating compressed file<br> <br>* Duplicate uuid error for requestId<br> <br>* Error when the corresponding item already exists | |
| 401 | * Invalid Token information | |
| 500 | * External module error (DB) | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |
- - -

# 4\. Item API

- - -

## 4.1 GET atlas/item/detail/{requestId}

* This is an API that searches for an item corresponding to `requestId`.    

### 4.1.1 Request

**Info**

|     |     |
| --- | --- |
| **Info** |     |
| Method | `GET` |
| **Header** |     |
| `Authorization` | Token information including account information<br><br>* “Bearer `accessToken`” |
| **URL Parameter** | |
| `requestId` | Unique item ID |

### 4.1.2 Response

#### 4.1.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 200 | Completed processing of specific item lookup request | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `requestId` | `string` | Unique item number |
| `Status` | `string` | Item creation request status<br><br>`PROGRESS`: Item creation request is still in the queue or learning is in progress<br><br>`OK`: Item creation is complete<br><br>`NG`: Learning for item creation failed |
| `modelId` | `string` | Unique identifier of the model used to create the item<br><br>* `nerf2mesh : 1`<br> <br>* `gaussian-splatting : 2`<br> <br>* `decal : 3`<br> <br>* `MusePose : 4`<br> <br>* `InstantMesh : 5` |
| `modelName` | `string` | Model name used to create the item<br><br>* `nerf2mesh`<br> <br>* `gaussian-splatting`<br> <br>* `decal`<br> <br>* `MusePose`<br> <br>* `InstantMesh` |
| `uploaderId` | `string` | Unique identifier of the user who requested the creation |
| `uploaderNickname` | `string` | Nickname of the user who requested the creation |
Response Body Example

#### 4.1.2.2 Fail

**Code**

**Code**

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 401 | Invalid Token Information | |
| 500 | API Server Internal Error | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response Information |

- - -

## 4.2 GET atlas/item/download/{requestId}

* Download generated items corresponding to `requestId`    

### 4.2.1 Request

**Info**

|     |     |
| --- | --- |
| **Info** |     |
| Method | `GET` |
| **URL** |     |
| `requestId` | Unique item ID |
| **Query** | |
| `code` | Specifies the model result format of the generated item (optional).<br><br>See the Code table below. |
| **Header** | |
| `Authorization` | Token information including account information<br><br>* “Bearer `accessToken`” |
Code Table

### 1\. `gaussian-splatting`

| `code` Value | target file |
| --- | --- |

| `code` Value | target file |
| --- | --- |
| 1(default) | \*`.ply` |

### 2\. `InstantMesh`

| `code` Value | target file |
| --- | --- |

| `code` Value | target file |
| --- | --- |
| 1(default) | \*`.glb` (Default) |
| 2   | \*`.obj` |
| 2   | \*`.obj` |

### 3\. `decal`

|     |     |
| --- | --- |
| `code` Value | target file |
|     |     |
| --- | --- |
| `code` Value | target file |
| 1(default) | \*`.glb` (Default) |
| 2   | \*`.gif` |
| 3   | \*`.tar.gz` |

### 4\. `nerf2mesh`

| `code` Value | target file |
| --- | --- |

| `code` Value | target file |
| --- | --- |
| 1(default) | \*`_1.glb` (Default) |
| 2   | \*`_0.glb` |
| 3   | \*`.gif` |

### 4.2.2 Response

#### 4.2.2.1 Success

**Code**

|     |     |
| --- | --- |
| **Code** |     |
| **Code** | **Description** |
| 200 | Item download request processing completed |
| **Body** |     |
| **${itemName}.${ext}** |     |

#### 4.2.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 401 | Invalid Token Information | |
| 404 | If the history for the item cannot be found | |
| 500 | API Server Internal Error | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response Information |

- - -

## 4.3 GET atlas/item/my/{ModelId}

* API to retrieve the list of items created by the current user

* Retrieves by model

### 4.3.1 Request

**Info**

|     |     |     |
| --- | --- | --- |
| **Info** |     |     |
| Method | `GET` |     |
| **URL** |     |     |
| `ModelId` | Required | AI model unique ID |
| `orderBy` | Required | Sorting criteria field (currently only createdAt is supported) |
| `desc` | Required | Sorting direction (true: ascending, false: descending) |
| `cursor` | Optional | Cursor value (currently only createdAt is supported)<br><br>* If null, the most recent data will be retrieved |
| `limit` | Optional | Number of items per page<br><br>* Default value 10<br> <br>* Maximum value 50 |

### 4.3.2 Response

#### 4.3.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 200 | User-created item list query request processing completed | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `requestId` | `string` | Item unique number |
| `status` | `string` | Item creation request status<br><br>`PROGRESS`: Item creation request is still in the queue or learning in progress<br><br>`OK`: Item creation is complete<br><br>`NG`: Learning for item creation failed |
| `model` | `string` | Model name used to create the item<br><br>* `nerf2mesh`<br> <br>* `gaussian-splatting`<br> <br>* `decal`<br> <br>* `MusePose`<br> <br>* `InstantMesh` |
| `itemName` | `string` | Item name |
| `createdAt` | `string` | Item creation date |
| `hasNextItem` | `boolean` | Whether there are more items to retrieve |
| `nextCursor` | `string` \| `null` | Cursor data for retrieving the next page (null if there is no next page) |
Response Body Example

#### 4.3.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 401 | Invalid Token Information | |
| 500 | API Server Internal Error | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response Information |
- - -

## 4.4 GET atlas/item/detail/my/{requestId}

* This is an API that searches for information on the `requestId` item created by the user.    

### 4.4.1 Request

**Info**

|     |     |
| --- | --- |
| **Info** |     |
| Method | `GET` |
| **URL** |     |
| `requestId` | Unique item ID |

### 4.4.2 Response

#### 4.4.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 200 | Item details inquiry request processing completed | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `requestId` | `string` | Item unique number |
| `itemName` | `string` | Item name |
| `status` | `string` | Item creation request status<br><br>`PROGRESS`: Item creation request is still in the queue or learning is in progress<br><br>`OK`: Item creation is complete<br><br>`NG`: Learning for item creation failed |
| `modelId` | `string` | Unique identifier of the model used to create the item<br><br>* `nerf2mesh : 1`<br> <br>* `gaussian-splatting : 2`<br> <br>* `decal : 3`<br> <br>* `MusePose : 4`<br> <br>* `InstantMesh : 5` |
| `modelName` | `string` | AI model name |
| `uploaderId` | `string` | Unique number of the uploading user |
| `uploaderNickname` | `string` | Nickname of the uploading user |
| `createdAt` | `string` | Item creation time |

#### 4.4.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 401 | Invalid Token Information | |
| 404 | If the item cannot be found | |
| 500 | API Server Internal Error | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response Information |

- - -

## 4.5 DELETE atlas/item/{requestId}

* Delete the `requestId` item.    

### 4.5.1 Request

**Info**

|     |     |
| --- | --- |
| **Info** |     |
| Method | `DELETE` |
| **URL** |     |
| `requestId` | Unique item ID |
### 4.5.2 Response

#### 4.5.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 200 | Item deletion request completed | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `requestId` | `string` | Item unique number |

#### 4.5.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 401 | Invalid Token Information | |
| 403 | If you try to delete an item that you do not own | |
| 404 | If the item cannot be found | |
| 500 | API Server Internal Error | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response Information |
- - -

## 4.6 GET atlas/item/${type}/{requestId}

* Download metadata of `requestId` item.

* Metadata here refers to job\_log, output.zip, reply.tar.gz, request.tar.gz, thumbnail, etc.)

* Developed for viewing generated results during AI model development

### 4.6.1 Request

**Info**

|     |     |
| --- | --- |
| **Info** |     |
| Method | `GET` |
| **URL** |     |
| `requestId` | Unique item ID |
| `type` | Unique metadata type<br><br>* thumbnail<br> <br>* request<br> <br>* reply<br> <br>* output<br> <br>* log |

### 4.6.2 Response

#### 4.6.2.1 Success

**Code**

|     |     |
| --- | --- |
| **Code** |     |
| **Code** | **Description** |
| 200 | Item metadata download request completed |
| **Body** |     |
| **request.tar.gz** |     |

#### 4.6.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 401 | Invalid Token Information | |
| 404 | If the item cannot be found | |
| 500 | API Server Internal Error | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response Information |

- - -

# 5\. Role API

- - -

## 5.1 GET atlas/role

* All Role query APIs.

* Roles have an inheritance relationship, and the parent role includes all permissions of the child role.
        

### 5.1.1 Request

**Info**

|     |     |
| --- | --- |
| **Info** |     |
| Method | `GET` |
| Content-Type | `application/json` |

### 5.1.2 Response

#### 5.1.2.1 Success

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 201 | All Roles Completed | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `id` | `string` | Unique identifier of the role. (uuid) |
| `name` | `string` | Role name. (ex. Seoul National University) |
| `description` | `string` | Role description. |
| `createdAt` | `string` | Role creation date. |
| `updatedAt` | `string` | Role modification date. |

#### 5.1.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 500 | * Unexpected system error | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |

- - -

# 6\. Basic API

- - -

## 6.1 GET atlas/version

* This is the version query API.

### 6.1.1 Request

**Info**

|     |     |
| --- | --- |
| **Info** |     |
| Method | `GET` |
| Content-Type | `application/json` |

### 6.1.2 Response

#### 6.1.2.1 Success

|     |     |
| --- | --- |
|     |     |

|     |     |
| --- | --- |
|     |     |
| **Description** |     |
| All Roles Query Complete | |
| | | |
| **Type** | **Description** |
| `string` | Version Information |

#### 6.1.2.2 Fail

**Code**

|     |     |     |
| --- | --- | --- |
| **Code** |     |     |
| **Code** | **Description** |     |
| 500 | * Unexpected system error | |
| **Body** | | |
| **key** | **Type** | **Description** |
| `message` | `string` | Response information |

- End -
