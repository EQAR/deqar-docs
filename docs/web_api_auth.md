# Authentication

 DEQAR API endpoints manage authentication using API Tokens (through the so-called Bearer Authentication method). Upon registration, an API Token (which is basically a hash) is created for each user. Sending this token in the Authorization header (with type/scheme Bearer) will authenticate the user in place of a regular username and password.

To get your authentication token you can send a `POST` request to the following URL:

<{{ deqar.root }}/accounts/get_token/>

An example of obtaining a token using curl in command line:

```sh
curl -s -H "Content-Type: application/json" -XPOST {{ deqar.root }}/accounts/get_token/ --data '{"username":"testuser","password":"testpassword"}'
```

Or for those who prefer to use the more user friendly [HTTPie](https://httpie.io/) client:

```sh
http POST {{ deqar.root }}/accounts/get_token/ 'username=testuser' 'password=testpassword'
```

You should send this token, preceded by the word `Bearer`, in the Authorization header with every further request. An example of a submission using curl or HTTPie:

```
curl -s -H "Content-type: application/json" -H "Authorization: Bearer $DEQAR_TOKEN" {{ deqar.root }}/webapi/v2/browse/reports/

http {{ deqar.root }}/webapi/v2/browse/reports/ "Authorization: Bearer $DEQAR_TOKEN"
```

