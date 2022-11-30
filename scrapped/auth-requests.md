# MP20 Login user request

*REF - rubyyagi.com/rails-api-authentication-devise-doorkeeper*

* [ ] make POST request to /oauth/token with:
* grant_type
* email
* password
* client_id
* client_secret

* [ ] table for client_id and secrets... model is Doorkeeper::Application
*using the desktop_client's token and secret, I get this:*
```
curl -d '{"grant_type":"password","email":"leo.ku@drifter.live","password":"Ineidu33*","client_id":"kuDIT-Kp3HNR5HtFUVwYy1f5kYn9EBFAjaWfP7a-090","client_secret":"tREOnMJSDCI6x-fAlWBL3_yaksmTrVcHMw0FZ8CyZHI"}' -H 'Content-Type: application/json' -X POST localhost:3000/oauth/token
{"access_token":"eyJraWQiOiJrdURJVC1LcDNITlI1SHRGVVZ3WXkxZjVrWW45RUJGQWphV2ZQN2EtMDkwIiwiYWxnIjoiSFM1MTIifQ.eyJpc3MiOiJEcmlmdGVyIExpdmUiLCJpYXQiOjE2NjY5ODI2MDEsImp0aSI6IjU5YzRiYmE4LTI2MWYtNDUzYi1hNDc0LTlmN2ZjZDVmY2VlYyIsInVzZXIiOnsiaWQiOjEwLCJzbHVnIjoibGVvLWt1In19.nC48_k2IElYDLOLlWVK7IjqSLGLIaBZVj9ZB_MjLXhfyp2Qjme1gYbG4jwOJamtLZv52GgFQTOp0gOPQGwOKfQ","token_type":"Bearer","expires_in":864000,"refresh_token":"yneNLb5KFqTVSHhN7n6J3wnrYUwdNPAq5h6Iq8ox214","created_at":1666982601}%
```

The problem right now is cors... CORS will block all request from a different origin than your API.  Origin in this case is the combination fo protocol, domain, and port.  If any of these three are different then CORS won't allow the front to connect.

CORS is always handled from the backend.  I'm getting errors in the console.  The first one says that there is a missing Access-Control-Allow-Origin header on the resource I requested.  My browser doesn't have anything to do with CORS.  It is only something that my browser imposes.  My browser is just suggesting that the resource I'm requesting should be configured differently.  

MP20 is to  configure the response from the server in a way that the browser identifies it as a CORS request.  There are ways to get around this from the browser, but the most reliable way is to make the response from rails cors friendly.

* [ ] add rack-cors to drifter_api
* [x] config in drifter_api with:
```
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins 'http://example.com:80'
    resource '*', headers: :any, methods: [:get, :post]
  end
end
```

* [ ] create the requests in the service and get the same login action to work
* [x] remove these and confirm that the request still works: (still works)
```
        crossDomain: true,
        withCredentials: false,

```

* [ ] pass in the login data as the form values rather than the hard coded values I'm currently using

WHEN I enter valid credentials into the form, I see the actions I want in the redux devtools and I get auth credentials back.  WHEN I put wrong email or password, I get this error:
```
Unhandled Runtime Error
InvalidStateError: Failed to read the 'responseText' property from 'XMLHttpRequest': The value is only accessible if the object's 'responseType' is '' or 'text' (was 'json').
```

That error appears that I'm getting data back into the observable, but the I should JSON.parse it so that it is no longer JSON...??
* [x] first use curl to see what the request returns with bad data
---> I get this:
```
{"error":"invalid_grant","error_description":"The provided authorization grant is invalid, expired, revoked, does not match the redirection URI used in the authorization request, or was issued to another client."}%
```
... which is JSON... and I don't see this in the rails log console.
*WHEN I type in just a string, I get the error but it doesn't cause an error in the app*

So, WHEN the part of the epic of is given that error, it causes that app error
* [ ] drill down in it so that only the error shows

I also think that it is the reducer that is causing the error and not the epic. The epic is supposed to return the action with the error and that is happening in the console.  The reducer then gets this data and is trying to proccess it but it can't since it is the mess I'm giving it...??

---> The error is everything after the payload... and it is a lot of information that doesn't do the user any good to see.  The only thing the user should see is a clear message on WHY the request was bad

* [ ] logout rout is /oauth/revoke
* [ ] make a logout epic
* [ ] first use a hardcoded token to make sure the revoke route works
* [ ] then use withLatestFrom to retrieve the token from the store and send its value with the revoke request
