## Water Oil Project API Reference V3.1



## 1. Login

#### POST /login

* The server will have a SET-COOKIE header in response to maintained login status, so for the front end, `withCredentials` needs to be appended to requests.
* In moany cases, the request headers need to be deleted. (Not the case for the login function)

```
this.http.post(url, userLoginRequest, { withCredentials: true, headers: new HttpHeaders().delete('Content-Type') }) as Observable<>
```

* Make sure your 'origin' in request header is not null

* `withCredentials` will be necessary for both and only login and logout requests

#### Request body: 

```
username: string
password: string
```

#### Response body:

```json
{'status': 0, 'msg': 'Login successful.', 'meta': {'attempted_username': 'aasdf', 'name': 'Todd Jastin', 'email': '123@abc.com'}}
```

```json
{'status': 1, 'msg': 'Account does not exist.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 2, 'msg': 'Password and username do not match.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 5, 'msg': 'Please fill in all required fields.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 9, 'msg': 'Error occurred, please try again later.', 'meta': {'attempted_username': 'abc'}}
```



## 2. Register

#### POST /register

#### Request body: 

```
username: string
password: string
email: string
name: string
```

#### Response body:

```json
{'status': 0, 'msg': 'Register successful.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 3, 'msg': 'Username has been used.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 5, 'msg': 'Please fill in all required fields.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 9, 'msg': 'Error occurred, please try again later.', 'meta': {'attempted_username': 'abc'}}
```



## 3. Reset Password

#### POST /resetpassword

#### Request body: 

```
username: string
password: string
email: string
```

#### Response body:

```json
{'status': 0, 'msg': 'New password has been set successfully.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 1, 'msg': 'Username does not exist.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 2, 'msg': 'Email address does not match.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 5, 'msg': 'Please fill in all required fields.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 9, 'msg': 'Error occurred, please try again later.', 'meta': {'attempted_username': 'abc'}}
```



## 4. Image Upload

#### POST /photoupload

#### Request body: 

```
gps: string
photo: file/image*
notes: string
```

```
gps sample: (No parenthesis, blank space. Latitude FIRST.)
38.8897,-77.0089
```

* If no notes inputted by user, set notes to "" with the request.
* GPS should be decimal degrees. https://en.wikipedia.org/wiki/Decimal_degrees (38° 53′ 23″ N, 77° 00′ 32″ W) ==> (38.8897,-77.0089)

#### Response body:

```json
{'status': 0, 'msg': 'Upload successful.', 'meta': {'attempted_username': 'abc', 'result': 0.12345978}}
```

```json
{'status': 2, 'msg': 'KeyError. Please upload correct image.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 4, 'msg': 'Image is not uploaded.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 5, 'msg': 'Please fill in all required fields.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 6, 'msg': 'Please upload only image file.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 6, 'msg': 'GPS error.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 8, 'msg': 'Login timeout.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 9, 'msg': 'Error occurred, please try again later.', 'meta': {'attempted_username': 'abc'}}
```



## 5. History

#### <span style="color:red">POST</span> /history

#### Request body: 

```
page: number
```

* This parameter can be ignored. If so, the first 100 entries will be returned.
* If this parameter is provided, there will be 100 entries per page.
* For the first time to send this request, “page=1” could be passed, and the total page number will be returned in “meta” part.
* PAGE STARTS FROM 1.

* This function is used for ordinary users. Only history from this user will be returned.
* GPS should be decimal degrees. https://en.wikipedia.org/wiki/Decimal_degrees (38° 53′ 23″ N, 77° 00′ 32″ W) ==> (38.8897,-77.0089)

#### Response body:

```json
{'status': 0, 'msg': {1: {'id': 2534, 'path': '123', 'gps': '30.354, 175.945', 'date': '20211212', 'result': 13.7, 'notes': 'note here.', 'tags': '#tag1#tag2#tag3'}, 2: {{'path': '123', 'gps': '30.354, 175.945', 'date': '20211212', 'result': 13.7, 'notes': 'note here.', 'tags': '#tag1#tag2#tag3'}}, 'meta': {'attempted_username': 'abc', 'total_page': 15, 'current_page': 1}}
```

```json
{'status': 8, 'msg': 'Login timeout.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 9, 'msg': 'Error occurred, please try again later.', 'meta': {'attempted_username': 'abc'}}
```



## 6. Admin - Login

#### POST /adminlogin

#### Request body: 

```
username: string
password: string
```

#### Response body:

```json
{'status': 0, 'msg': 'Login successful.', 'meta': {'attempted_username': 'aasdf', 'name': 'Todd Jastin', 'email': '123@abc.com'}}
```

```json
{'status': 1, 'msg': 'Account does not exist.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 2, 'msg': 'Password and username do not match.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 5, 'msg': 'Please fill in all required fields.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 7, 'msg': 'You are not allowed to login as administrator.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 9, 'msg': 'Error occurred, please try again later.', 'meta': {'attempted_username': 'abc'}}
```



## 7. Admin - Photo List

#### POST /adminphotolist

#### Request body: 

```
mindate: string
maxdate: string
page: number
```

* Time format: 2021-11-30
* GPS should be decimal degrees. https://en.wikipedia.org/wiki/Decimal_degrees (38° 53′ 23″ N, 77° 00′ 32″ W) ==> (38.8897,-77.0089)
* All dates on the server side and response part are UTC.
* If all photos needed, set parameters both as "-" with the request.
* Entries will be returned in descending order.



* PAGE parameter can be ignored. If so, the first 100 entries will be returned.
* If PAGE parameter is provided, there will be 100 entries per page.
* For the first time to send this request, “page=1” could be passed, and the total page number will be returned in “meta” part.
* PAGE STARTS FROM 1.

#### Response body:

```json
{'status': 0, 'msg': {1: {'id': 135345, 'path': '123', 'gps': '30.354, 175.945', 'date': '20211212', 'result': 13.7, 'notes': 'note here.', 'tags': '#tag1#tag2#tag3'}, 2: {{'path': '123', 'gps': '30.354, 175.945', 'date': '20211212', 'result': 13.7, 'notes': 'note here.', 'tags': '#tag1#tag2#tag3'}}, 'meta': {'attempted_username': 'abc', 'total_page': 15, 'current_page': 1}}
```

```json
{'status': 5, 'msg': 'Please fill in all required fields.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 8, 'msg': 'Login timeout.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 9, 'msg': 'Error occurred, please try again later.', 'meta': {'attempted_username': 'abc'}}
```



## 8. User meta

#### GET /user

#### Response body:

```json
{'status': 0, 'msg': {'username': 'aasdf', 'name': 'Todd Jastin', 'email': '123@abc.com'}, 'meta': {'attempted_username': 'aasdf'}}
```

```json
{'status': 8, 'msg': 'Login timeout.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 9, 'msg': 'Error occurred, please try again later.', 'meta': {'attempted_username': 'abc'}}
```



## 9. Admin - Update photo information(notes&tags)

#### POST /adminupdatephotoinfo

#### Request body: 

```
photo_id: number
notes: string
tags: string
```

```json
*tags format:
#tag1#tag2#tag3
```

* Notes and tags should be whole values rather than only updated parts!

* If only notes(or tags) should be updated, please also pass current tags(or notes) together with the request.

#### Response body:

```json
{'status': 0, 'msg': 'Update successful.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 5, 'msg': 'Please fill in all required fields.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 8, 'msg': 'Login timeout.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 9, 'msg': 'Error occurred, please try again later.', 'meta': {'attempted_username': 'abc'}}
```



## 10. Logout

#### GET /logout

#### Response body:

```json
{'status': 0, 'msg': 'Logout successful.'}
```



## 11. Admin - Search Filter - Tag

#### POST /searchfiltertag

#### Request body: 

```
taglist: string
```

```json
*taglist format:
#tag1#tag2#tag3
```

* A list with photos contain all tags at the same time will be returned.
* GPS should be decimal degrees. https://en.wikipedia.org/wiki/Decimal_degrees (38° 53′ 23″ N, 77° 00′ 32″ W) ==> (38.8897,-77.0089)
* All entries will be returned at once.

#### Response body:

```json
{'status': 0, 'msg': {1: {'id': 135345, 'path': '123', 'gps': '30.354, 175.945', 'date': '20211212', 'result': 13.7, 'notes': 'note here.', 'tags': '#tag1#tag2#tag3'}, 2: {{'path': '123', 'gps': '30.354, 175.945', 'date': '20211212', 'result': 13.7, 'notes': 'note here.', 'tags': '#tag1#tag2#tag3'}}, 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 5, 'msg': 'Please fill in all required fields.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 8, 'msg': 'Login timeout.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 9, 'msg': 'Error occurred, please try again later.', 'meta': {'attempted_username': 'abc'}}
```



## 12. Admin - Search Filter - Notes Global (filter photos with specific query string in their notes)
#### POST /searchfilterglobal

#### Request body: 

```
querystring: string
page: number
```

* GPS should be decimal degrees. https://en.wikipedia.org/wiki/Decimal_degrees (38° 53′ 23″ N, 77° 00′ 32″ W) ==> (38.8897,-77.0089)



* PAGE parameter can be ignored. If so, the first 100 entries will be returned.
* If PAGE parameter is provided, there will be 100 entries per page.
* For the first time to send this request, “page=1” could be passed, and the total page number will be returned in “meta” part.
* PAGE STARTS FROM 1.

#### Response body:

```json
{'status': 0, 'msg': {1: {'id': 135345, 'path': '123', 'gps': '30.354, 175.945', 'date': '20211212', 'result': 13.7, 'notes': 'note here.', 'tags': '#tag1#tag2#tag3'}, 2: {{'path': '123', 'gps': '30.354, 175.945', 'date': '20211212', 'result': 13.7, 'notes': 'note here.', 'tags': '#tag1#tag2#tag3'}}, 'meta': {'attempted_username': 'abc', 'total_page': 15, 'current_page': 1}}
```

```json
{'status': 5, 'msg': 'Please fill in all required fields.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 8, 'msg': 'Login timeout.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 9, 'msg': 'Error occurred, please try again later.', 'meta': {'attempted_username': 'abc'}}
```



## 13. Admin - Search Filter - geography
#### POST /searchfiltergeography

#### Request body: 

```
gps: string
radius: number
radiusunit: string
page: number
last_token: string
next_token: string
```

```json
gps sample: (No parenthesis, blank space. Latitude FIRST.)
38.8897,-77.0089
```

* Radiusunit should be "m" (meter), "km" or "mile".
* Radius should be an integer.
* GPS should be decimal degrees. https://en.wikipedia.org/wiki/Decimal_degrees (38° 53′ 23″ N, 77° 00′ 32″ W) ==> (38.8897,-77.0089)



* PAGE parameter can be ignored. If so, the first 100 entries will be returned.
* If PAGE parameter is provided, there will be 100 entries per page.
* For the first time to send this request, “page=1” could be passed, and the total page number will be returned in “meta” part.
* PAGE STARTS FROM 1.



* NEXT_TOKEN/LAST_TOKEN is used for turning pages, they MUST be UPPERCASE. If you received this from backend in last request, please add it in your request. 
* If NEXT_TOKEN is ‘-’ in response, this indicates the last page is being returned.
* ‘-’ is used to disable a token.
* TOKEN SAMPLES:

```
# First request:
next_token=-&last_token=-

# Moving forward:
next_token=ThisIsWhatYouGotFromResponse&last_token=-

# Moving back:
next_token=-&last_token=ThisIsWhatYouGotFromResponse
```



#### Response body:

```json
{'status': 0, 'msg': {1: {'id': 135345, 'path': '123', 'gps': '30.354, 175.945', 'date': '20211212', 'result': 13.7, 'notes': 'note here.', 'tags': '#tag1#tag2#tag3'}, 2: {{'path': '123', 'gps': '30.354, 175.945', 'date': '20211212', 'result': 13.7, 'notes': 'note here.', 'tags': '#tag1#tag2#tag3'}}, 'meta': {'attempted_username': 'abc', 'last_token': 'abc', 'next_token': 'qwe'}}
```

```json
{'status': 5, 'msg': 'Please fill in all required fields.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 6, 'msg': 'TOKENs are invalid.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 8, 'msg': 'Login timeout.', 'meta': {'attempted_username': 'abc'}}
```

```json
{'status': 9, 'msg': 'Error occurred, please try again later.', 'meta': {'attempted_username': 'abc'}}
```
