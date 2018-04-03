firebase init
firebase deploy
firebase serve



 3. Generate an "anonymous" user with the following request:
    POST https://www.googleapis.com/identitytoolkit/v3/relyingparty/signupNewUser?key=[API_KEY]

 4. Login with username and password to get an OAuth token (idToken):
    POST https://www.googleapis.com/identitytoolkit/v3/relyingparty/verifyPassword?key=[API_KEY]
    Content-Type: application/json
    
    {
	    "email": "user@domain.com",
	    "password": "***",
	    "returnSecureToken": true
    }
    
    Note the idToken and the refreshToken. Also note that it expires in x (=expiresIn usually) seconds (typically 3600s = 1 hour).

 5. Your idToken (xyz***) is the token you use in the Authorization header for future requests:

     Authorization: Bearer xyz***

6. Once your token expires you can get another one by requesting it via your refreshToken:
    POST https://securetoken.googleapis.com/v1/token?key=[API_KEY]
    Content-Type: application/x-www-form-urlencoded

    grant_type=refresh_token&refresh_token=[REFRESH_TOKEN]

 7. Create a document with the API explorer: https://developers.google.com/apis-explorer/
   Choose createDocument
   parent: projects/test1-b1ff5/databases/(default)/documents
   collectionId: monitoring-dev
   documentId: [some unique number]
   {
       "fields": {
           "sys": "foo",
           "subsys": "bar"
       }
   }