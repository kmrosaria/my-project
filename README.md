## Free APIs

### Searching Deals

```
GET https://dealcha.com/rest/deal/search
```

#### Parameters

 - `order`
 - `filter`
 - `start`
 - `range`

```
GET https://dealcha.com/rest/deal/detail/:id
```

```
GET https://dealcha.com/rest/store/search
```

#### Parameters

 - `order`
 - `filter`
 - `start`
 - `range`

```
GET https://dealcha.com/rest/store/detail/:id
```

## How to create an App

1. [Log In](https://dealcha.com/login)
2. Go to [App Search](https://dealcha.com/developer/app/search)
3. [Create](https://dealcha.com/developer/app/create) an app

## How OAuth 2 Works

In [App Search](https://dealcha.com/developer/app/search), click the lock. This is what you redirect to get a user's permission.

### Example scope

```
http://www.dealcha.dev/dialog/request?client_id=[app_token]&redirect_uri=[redirect url]&scope=user_profile
```

### Exchange code with a token

After the user approves of your app, they will be redirected back to the specified `[redirect url]` with a new URL paramter called `?code`. The last thing you need to do is exchange that code for a token. Using cURL, call the following.

```
POST http://www.dealcha.dev/rest/access

client_id [app_token]
client_secret [app_secret]
code [code]
```

This should return a session token similar to the following.

```
{
    "error": false,
    "results": {
        "access_token": "123",
        "access_secret": "456",
        "profile_id": "49392",
        "profile_name": null,
        "profile_email": "johndoe@gmail.com",
    }
}
```

### Session API calls

```
GET https://dealcha.com/rest/profile/cashback/summary?access_token=[access_token]
```

```
GET https://dealcha.com/rest/profile/cashback/pending?access_token=[access_token]
```

```
GET https://dealcha.com/rest/profile/cashback/redeemed?access_token=[access_token]
```

```
GET https://dealcha.com/rest/profile/cashback/approved?access_token=[access_token]
```

```
GET https://dealcha.com/rest/profile/cashback/paid?access_token=[access_token]
```

```
GET https://dealcha.com/rest/profile/trips?access_token=[access_token]
```
