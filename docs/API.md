Buzzedeal API
=======

Buzzedeal Front end API

[![Build Status](https://travis-ci.com/Openovate/buzzedeal.svg?token=usAby1dW3tLQe7YAy7Cr&branch=master)](https://buzzedeal.com)

How to create an App
---------------

1. [Log In](https://buzzedeal.com/login)
2. Go to [App Search](https://buzzedeal.com/developer/app/search)
3. [Create](https://buzzedeal.com/developer/app/create) an app

### How OAuth 2 Works

In [App Search](https://buzzedeal.com/developer/app/search), click the lock. This is what you redirect to get a user's permission.

### Example scope

```
https://www.buzzedeal.com/dialog/request?client_id=[app_token]&redirect_uri=[redirect url]&scope=user_profile
```

### Exchange code with a token

After the user approves of your app, they will be redirected back to the specified `[redirect url]` with a new URL parameter called `?code`. The last thing you need to do is exchange that code for a token. Using cURL, call the following.

```
POST : https://buzzedeal.com/rest/access
```

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required
`code [code]` | string | required

```
This should return a session token similar to the following.

{
    "error": false,
    "results": {
        "access_token": "123",
        "access_secret": "456",
        "profile_id": "57093",
        "profile_name": null,
        "profile_email": "johndoe@gmail.com",
    }
}

```

Account Authentication
------------

Getting Account Information. 

### Sign Up

Signin up a user via API.

```
POST : https://buzzedeal.com/rest/signup
```

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required
`profile_email` | email | required
`auth_password` | string | required
`confirm` | string | required
`promotion` | string | optional
`terms` | string | required

```
The response should be similar to the following and this will response the data for your session. The user will also recieve a confirmation email.

{
    "error": false,
    "results": {
        "auth_id": "57034",
        "auth_slug": "johndoe@gmail.com",
        "auth_token": "90298c3d08e1a8135aa58305de35db5c",
        "auth_facebook_token": null,
        "auth_permissions": "public_product,public_profile,personal_profile,personal_product,personal_comment,personal_review",
        "auth_type": null,
        "auth_active": "0",
        "auth_created": "2017-09-15 15:38:26",
        "auth_updated": "2017-09-15 15:38:26",
        "profile_id": "57093",
        "profile_active": "1",
        "profile_created": "2017-09-15 15:38:27",
        "profile_updated": "2017-09-15 15:38:27",
        "profile_first": null,
        "profile_last": null,
        "profile_username": null,
        "profile_email": "johndoe@gmail.com",
        "profile_image": "{\"large\": \"http://buzzedeal.dev/images/avatar/avatar-10.png\", \"small\": \"http://buzzedeal.dev/images/avatar/avatar-10.png\"}",
        "profile_phone": null,
        "profile_gender": null,
        "profile_birthdate": null,
        "profile_address": null,
        "profile_channel_transfer": null,
        "profile_bank_name": null,
        "profile_bank_account_name": null,
        "profile_bank_account_number": null,
        "profile_paypal_account_name": null,
        "profile_paypal_account_number": null,
        "profile_code": null,
        "profile_type": null,
        "profile_flag": null,
        "cashback": {
            "total": 0,
            "pending": 0,
            "approved": 0,
            "redeemable": 0,
            "paid": null,
            "bonus": {
                "redeemable": "0",
                "paid": 0
            },
            "redeemable_approved": 0
        }
    },
    "message": "Sign Up Successful. Please check your email for verification process."
}

```

### Log In

Log in via API.

```
POST : https://buzzedeal.com/rest/login
```

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required
`auth_slug` | email | required
`auth_password` | string | required


```
The response should be similar to the following and this will response the data for your session.

{
    "error": false,
    "results": {
        "error": false,
        "results": {
            "auth_id": "57034",
            "auth_slug": "johndoe@gmail.com",
            "auth_token": "90298c3d08e1a8135aa58305de35db5c",
            "auth_facebook_token": null,
            "auth_permissions": "public_product,public_profile,personal_profile,personal_product,personal_comment,personal_review",
            "auth_type": null,
            "auth_active": "0",
            "auth_created": "2017-09-15 15:38:26",
            "auth_updated": "2017-09-15 15:38:26",
            "profile_id": "57093",
            "profile_active": "1",
            "profile_created": "2017-09-15 15:38:27",
            "profile_updated": "2017-09-15 15:38:27",
            "profile_first": null,
            "profile_last": null,
            "profile_username": null,
            "profile_email": "johndoe@gmail.com",
            "profile_image": "{\"large\": \"http://buzzedeal.dev/images/avatar/avatar-10.png\", \"small\": \"http://buzzedeal.dev/images/avatar/avatar-10.png\"}",
            "profile_phone": null,
            "profile_gender": null,
            "profile_birthdate": null,
            "profile_address": null,
            "profile_channel_transfer": null,
            "profile_bank_name": null,
            "profile_bank_account_name": null,
            "profile_bank_account_number": null,
            "profile_paypal_account_name": null,
            "profile_paypal_account_number": null,
            "profile_code": null,
            "profile_type": null,
            "profile_flag": null,
            "cashback": {
                "total": 0,
                "pending": 0,
                "approved": 0,
                "redeemable": 0,
                "paid": null,
                "bonus": {
                    "redeemable": "0",
                    "paid": 0
                },
                "redeemable_approved": 0
            }
        }
    }
}

```

### Forgot Password

Forgot Password via API.

```
POST : https://buzzedeal.com/rest/forgot
```

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required
`auth_slug` | email | required

```
The response should be similar to the following and the buzzedeal will send the forgot password email to the user.

{
    "error": false,
    "results": {
        "auth_id": "57034",
        "auth_slug": "johndoe@gmail.com",
        "auth_token": "90298c3d08e1a8135aa58305de35db5c",
        "auth_facebook_token": null,
        "auth_permissions": "public_product,public_profile,personal_profile,personal_product,personal_comment,personal_review",
        "auth_type": null,
        "auth_active": "0",
        "auth_created": "2017-09-15 15:38:26",
        "auth_updated": "2017-09-15 15:38:26",
        "profile_id": "57093",
        "profile_active": "1",
        "profile_created": "2017-09-15 15:38:27",
        "profile_updated": "2017-09-15 15:38:27",
        "profile_first": null,
        "profile_last": null,
        "profile_username": null,
        "profile_email": "johndoe@gmail.com",
        "profile_image": "{\"large\": \"http://buzzedeal.dev/images/avatar/avatar-10.png\", \"small\": \"http://buzzedeal.dev/images/avatar/avatar-10.png\"}",
        "profile_phone": null,
        "profile_gender": null,
        "profile_birthdate": null,
        "profile_address": null,
        "profile_channel_transfer": null,
        "profile_bank_name": null,
        "profile_bank_account_name": null,
        "profile_bank_account_number": null,
        "profile_paypal_account_name": null,
        "profile_paypal_account_number": null,
        "profile_code": null,
        "profile_type": null,
        "profile_flag": null
    },
    "message": "An email with recovery instructions will be sent in a few minutes."
}

```

Profile Informations
------------

Getting Infomation about the user.

### Profile Detail

Search for profile detail per user

```
GET : https://buzzedeal.com/rest/profile/detail/:profile_id
```

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required

```
Change the `:profile_id` with the profile_id of the user and the response should be profile detail for the `user`.

{
    "error": false,
    "results": {
        "profile_id": "57093",
        "profile_active": "1",
        "profile_created": "2017-09-15 15:38:27",
        "profile_updated": "2017-09-15 15:38:27",
        "profile_first": null,
        "profile_last": null,
        "profile_username": null,
        "profile_email": "johndoe@gmail.com",
        "profile_image": {
            "large": "http://buzzedeal.dev/images/avatar/avatar-10.png",
            "small": "http://buzzedeal.dev/images/avatar/avatar-10.png"
        },
        "profile_phone": null,
        "profile_gender": null,
        "profile_birthdate": null,
        "profile_address": [],
        "profile_channel_transfer": null,
        "profile_bank_name": null,
        "profile_bank_account_name": null,
        "profile_bank_account_number": null,
        "profile_paypal_account_name": null,
        "profile_paypal_account_number": null,
        "profile_code": null,
        "profile_type": null,
        "profile_flag": null
    }
}

```

### Profiles Search

Search for profiles

```
GET : https://buzzedeal.com/rest/profile/search/:profile_id
```

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required
`order` | string | optional
`filter` | string | optional
`start` | string | optional
`range` | string | optional

```
The response should be like the following.

{
    "error": false,
    "results": {
        "rows": [
            {
                "profile_id": "57093",
                "profile_active": "1",
                "profile_created": "2017-09-15 15:38:27",
                "profile_updated": "2017-09-15 15:38:27",
                "profile_first": null,
                "profile_last": null,
                "profile_username": null,
                "profile_email": "johndoe@gmail.com",
                "profile_image": {
                    "large": "http://buzzedeal.dev/images/avatar/avatar-10.png",
                    "small": "http://buzzedeal.dev/images/avatar/avatar-10.png"
                },
                "profile_phone": null,
                "profile_gender": null,
                "profile_birthdate": null,
                "profile_address": [],
                "profile_channel_transfer": null,
                "profile_bank_name": null,
                "profile_bank_account_name": null,
                "profile_bank_account_number": null,
                "profile_paypal_account_name": null,
                "profile_paypal_account_number": null,
                "profile_code": null,
                "profile_type": null,
                "profile_flag": null
            }
        ],
        "total": "1"
    }
}

```

### Profile Update

Update profile information per user

```
POST https://buzzedeal.com/rest/profile/update/:profile_id
```

Change the `:profile_id` with the profile_id of the user and add the parameter you want to update. 

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required
`profile_first` | string | optional
`profile_last` | string | optional
`profile_username` | string | optional
`profile_email` | string | optional
`profile_image` | string | optional
`profile_phone` | string | optional
`profile_gender` | string | optional
`profile_birthday` | string | optional
`profile_address` | string | optional

```
The response should be like the following.

{
    "error": false,
    "results": {
        "client_id": "300aaf826a59b87b2d5a4ebb6e3d336c",
        "client_secret": "5ae9782cdddd1994c6d91da7ad22d593",
        "profile_last": "John",
        "profile_first": "Doe",
        "profile_id": "57093",
        "profile_image": "{\"large\":\"http:\\/\\/buzzedeal.dev\\/images\\/avatar\\/avatar-2.png\",\"small\":\"http:\\/\\/buzzedeal.dev\\/images\\/avatar\\/avatar-2.png\"}",
        "profile_updated": "2017-09-18 13:52:06",
        "original": {
            "client_id": "300aaf826a59b87b2d5a4ebb6e3d336c",
            "client_secret": "5ae9782cdddd1994c6d91da7ad22d593",
            "profile_last": "John",
            "profile_first": "Doe",
            "profile_id": "57093",
            "profile_image": "{\"large\":\"http:\\/\\/buzzedeal.dev\\/images\\/avatar\\/avatar-2.png\",\"small\":\"http:\\/\\/buzzedeal.dev\\/images\\/avatar\\/avatar-2.png\"}",
            "profile_updated": "2017-09-18 13:52:06"
        }
    }
}

```

Settings
------------

### Cashback Summary

Get cashback summaries and list of cashback according to status

```
GET https://buzzedeal.com/rest/settings/cashback-summary/:profile_id
```

Change the `:profile_id` with the profile_id of the user. 

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required
`order` | string | optional
`filter` | string | optional
`start` | string | optional
`range` | string | optional
`status` | string | optional (Default : `pending`)

```
The response should be like the following.

{
    "error": false,
    "results": {
        "rows": [
            {
                "quote_id": "343238",
                "quote_active": "1",
                "quote_created": "2017-09-18 14:09:41",
                "quote_updated": "2017-09-18 14:09:41",
                "quote_reference": "2907902578",
                "quote_total": "1000.00",
                "quote_percentage": "1.00",
                "quote_cashback": "10.00",
                "quote_redeemable": null,
                "quote_pending": null,
                "quote_approved": null,
                "quote_rejected": null,
                "quote_paid": null,
                "quote_status": "pending",
                "quote_type": "store",
                "quote_flag": null,
                "store_name": "Lazada",
                "store_id": "1",
                "profile_id": "57093",
                "profile_first": null,
                "profile_last": null,
                "profile_email": "johndoe@gmail.com"
            }
        ],
        "total": "1",
        "totals": {
            "pending": "10.00",
            "total": 10,
            "approved": 0,
            "redeemable": 0,
            "paid": null,
            "bonus": {
                "redeemable": "0",
                "paid": 0
            },
            "redeemable_approved": 0
        },
        "status": "pending"
    }
}

```

### Referrals

Get User's referral data and list of referrals

```
GET https://buzzedeal.com/rest/settings/refer/:profile_id
```

Change the `:profile_id` with the profile_id of the user. 

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required

```
The response should be like the following.

{
    "error": false,
    "results": {
        "item": [],
        "profile_last": null,
        "profile_first": null,
        "encrypt_profile_id": "2133062",
        "total": "0",
        "total_complete": 0,
        "total_pending": 0
    }
}

```

### Missing Cashback

Report a missing cashback (`Discrepancy`)

```
POST https://buzzedeal.com/rest/settings/missing-cashback/:profile_id
```

Change the `:profile_id` with the profile_id of the user. 

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required
`discrepancy_reference` (Shopping Trip)| string | required
`discrepancy_note` (Total Purchase Price) | string | required
`discrepancy_price` (Expected Cashback Amount)| string | required
`discrepancy_order_email` (Order Confirmation Email)| string | optional
`discrepancy_images` (Order Confirmation Screenshot)| string | optional

```
The response should be like the following.

{
    "error": true,
    "results": {
        "client_id": "300aaf826a59b87b2d5a4ebb6e3d336c",
        "client_secret": "5ae9782cdddd1994c6d91da7ad22d593",
        "discrepancy_note": "1000",
        "discrepancy_reference": "2907902578",
        "discrepancy_price": "10",
        "discrepancy_order_email": "Sample Content",
        "profile_id": "57093",
        "fields": [
            "discrepancy_note",
            "discrepancy_reference",
            "discrepancy_price",
            "discrepancy_order_email",
            "discrepancy_images"
        ]
    },
    "message": "Missing Cashback succesfully reported."
}

```

Stores
------------

### Store Search

Search for Stores or list of stores

```
GET https://buzzedeal.com/rest/store/search
```

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required
`order` (latest/popular/cashback/store) | string | optional
`filter` | string | optional
`start` | string | optional
`range` | string | optional

```
The response should be like the following.

{
    "error": false,
    "results": {
        "rows": [
            {
                "promotion_id": "20000",
                "promotion_detail": "Lazada",
                "promotion_cashback_type": "fixed_percent",
                "promotion_cashback_basis": "total_purchased",
                "promotion_cashback_amount": "1",
                "promotion_priority": "20",
                "cashback_type": "fixed_percent",
                "store_id": "1",
                "store_name": "Lazada",
                "store_logo": {
                    "large": "http://buzzedeal.com/buzzedeal-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858",
                    "small": "http://buzzedeal.com/buzzedeal-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858",
                    "original": "http://buzzedeal.com/buzzedeal-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858"
                },
                "store_slug": "Lazada-s1",
                "store_link": "http://buzzedeal.dev/Lazada-s1/store",
                "store_root_url": "www.lazada.com.ph",
                "store_redirect": "http://buzzedeal.dev/redirect/store/1",
                "store_redirect_api": "http://buzzedeal.dev/rest/redirect/store/1?access_token=",
                "store_description": "Lazada Description",
                "store_default_cashback": "0.00",
                "store_max_purchase": "100000.00",
                "store_max_cashback": "300.00",
                "store_cashback": "1"
            },
        "total": "1"
    }
}

```

### Store Detail

Get Store Detail

```
GET https://buzzedeal.com/rest/store/detail/:store_id
```

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required

```
The response should be like the following.

{
    "error": false,
    "results": {
        "promotion_id": "20000",
        "promotion_detail": "Lazada",
        "promotion_cashback_type": "fixed_percent",
        "promotion_cashback_basis": "total_purchased",
        "promotion_cashback_amount": "1",
        "store_id": "1",
        "store_name": "Lazada",
        "store_logo": {
            "large": "http://buzzedeal.com/buzzedeal-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858",
            "small": "http://buzzedeal.com/buzzedeal-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858",
            "original": "http://buzzedeal.com/buzzedeal-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858"
        },
        "store_slug": "Lazada-s1",
        "store_link": "http://buzzedeal.dev/Lazada-s1/store",
        "store_root_url": "www.lazada.com.ph",
        "store_redirect": "http://buzzedeal.dev/redirect/store/1",
        "store_description": "Lazada Description",
        "store_default_cashback": "0.00",
        "store_max_purchase": "100000.00",
        "store_max_cashback": "300.00"
    }
}

```

### Store Redirect

Get redirect link and shopping trips for store

```
GET https://buzzedeal.com/rest/redirect/store/:store_id/:profile_id
```

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required

```
The response should be like the following.

{
    "error": false,
    "results": {
        "transaction_id": 1573110451,
        "url": "http://ho.lazada.co.th/SHDE4j?url=http%3A%2F%2Fwww.lazada.co.th%2Fhot-top-deals?offer_id={offer_id}&affiliate_id={affiliate_id}&offer_name={offer_name}_{offer_file_id}&affiliate_name={affiliate_name}&transaction_id=1573110451&aff_sub2=1573110451"
    }
}

```

Deals
------------


### Promotion Search

Search for Stores or list of stores

```
GET https://buzzedeal.com/rest/deal/search
```

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required
`order` (latest/popular/cashback/store) | string | optional
`filter` | string | optional
`start` | string | optional
`range` | string | optional

```
The response should be like the following.

{
    "error": false,
    "results": {
        "rows": [
            {
                "promotion_id": "1",
                "promotion_title": "Lazada Deal Number 1",
                "promotion_slug": "Lazada-Deal-Number-1-P1",
                "promotion_link": "https://buzzedeal.com/Lazada-Deal-Number-1-P1/deal",
                "promotion_redirect": "https://buzzedeal.com//redirect/promotion/1",
                "promotion_images": [
                    {
                        "large": "https://buzzedeal.com/upload/img.png",
                        "small": "https://buzzedeal.com/upload/img.png",
                        "original": "https://buzzedeal.com/upload/img.png"
                    }
                ],
                "promotion_detail": "<p>Deal Sample Descrition<br></p>",
                "promotion_orig_price": "750.00",
                "promotion_final_price": "690.00",
                "promotion_start": "2017-09-14 16:47:00",
                "promotion_end": "2017-09-30 16:47:00",
                "promotion_cashback_type": "upto_percent",
                "promotion_cashback_basis": "total_purchased",
                "promotion_cashback_amount": "6",
                "promotion_active": "1",
                "promotion_created": "2017-09-14 16:47:54",
                "promotion_updated": "2017-09-15 09:49:36",
                "cashback_type": "upto_percent",
                "store_id": "1",
                "store_name": "Lazada",
                "store_logo": {
                    "large": "http://buzzedeal.com/buzzedeal-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858",
                    "small": "http://buzzedeal.com/buzzedeal-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858",
                    "original": "http://buzzedeal.com/buzzedeal-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858"
                },
                "store_slug": "Lazada-s1",
                "store_link": "http://buzzedeal.dev/Lazada-s1/store",
                "store_redirect": "http://buzzedeal.dev/redirect/store/1",
                "store_description": "Lazada Description",
                "store_default_cashback": "0.00",
                "store_max_purchase": "100000.00",
                "store_max_cashback": "300.00",
                "store_cashback": "1"
            },
        "total": "1"
    }
}

```

### Deal Detail

Get Deal Detail

```
GET https://buzzedeal.com/rest/Deal/detail/:promotion_id
```

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required


```
The response should be like the following.

{
    "error": false,
    "results": {
        "promotion_id": "1",
        "promotion_title": "Lazada Deal Number 1",
        "promotion_slug": "Lazada-Deal-Number-1-P1",
        "promotion_link": "https://buzzedeal.com/Lazada-Deal-Number-1-P1/deal",
        "promotion_redirect": "https://buzzedeal.com//redirect/promotion/1",
        "promotion_images": [
            {
                "large": "https://buzzedeal.com/upload/img.png",
                "small": "https://buzzedeal.com/upload/img.png",
                "original": "https://buzzedeal.com/upload/img.png"
            }
        ],
        "promotion_detail": "<p>Deal Sample Descrition<br></p>",
        "promotion_orig_price": "750.00",
        "promotion_final_price": "690.00",
        "promotion_start": "2017-09-14 16:47:00",
        "promotion_end": "2017-09-30 16:47:00",
        "promotion_cashback_type": "upto_percent",
        "promotion_cashback_basis": "total_purchased",
        "promotion_cashback_amount": "6",
        "promotion_active": "1",
        "promotion_created": "2017-09-14 16:47:54",
        "promotion_updated": "2017-09-15 09:49:36",
        "cashback_type": "upto_percent",
        "store_id": "1",
        "store_name": "Lazada",
        "store_logo": {
            "large": "http://buzzedeal.com/buzzedeal-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858",
            "small": "http://buzzedeal.com/buzzedeal-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858",
            "original": "http://buzzedeal.com/buzzedeal-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858"
        },
        "store_slug": "Lazada-s1",
        "store_link": "http://buzzedeal.dev/Lazada-s1/store",
        "store_redirect": "http://buzzedeal.dev/redirect/store/1",
        "store_description": "Lazada Description",
        "store_default_cashback": "0.00",
        "store_max_purchase": "100000.00",
        "store_max_cashback": "300.00",
        "store_cashback": "1"
    }
}

```

### Deal Redirect

Get redirect link and shopping trips for store

```
GET https://buzzedeal.com/rest/redirect/promotion/:promotion/:profile_id
```

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required

```
The response should be like the following.

{
    "error": false,
    "results": {
        "transaction_id": 1573110451,
        "url": "http://ho.lazada.co.th/SHDE4j?url=http%3A%2F%2Fwww.lazada.co.th%2Fhot-top-deals?offer_id={offer_id}&affiliate_id={affiliate_id}&offer_name={offer_name}_{offer_file_id}&affiliate_name={affiliate_name}&transaction_id=1573110451&aff_sub2=1573110451"
    }
}

```

Category
------------

### Category Search

Get list of categories

```
GET https://buzzedeal.com/rest/category/search
```

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required

```
The response should be like the following.

{
    "error": false,
    "results": {
        "rows": [
            {
                "category_id": "1",
                "category_name": "Home Appliances",
                "category_type": null,
                "category_flag": null,
                "category_feature": "0",
                "category_active": "1",
                "category_created": "2017-05-23 20:59:00",
                "category_updated": "2017-05-24 15:09:43"
            },
        ],
        "total": "1"
    }
}

```
### Deal Detail

Search per category

GET https://buzzedeal.com/rest/category/detail/:category_id

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required

```
The response should be like the following.

{
    "error": false,
    "results": {
        "category_id": "1",
        "category_name": "Home Appliances",
        "category_type": null,
        "category_flag": null,
        "category_feature": "0",
        "category_active": "1",
        "category_created": "2017-05-23 20:59:00",
        "category_updated": "2017-05-24 15:09:43"
    }
}

```

Banners
------------

### Banner Search

Get list of Banners

```
GET https://buzzedeal.com/rest/banner/search
```

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required
`order` | string | optional
`filter` | string | optional
`start` | string | optional
`range` | string | optional

```
The response should be like the following.

{
    "error": false,
    "results": {
        {
            "banner_id": "4",
            "banner_active": "1",
            "banner_created": "2017-02-28 16:26:33",
            "banner_updated": "2017-08-12 09:52:25",
            "banner_image": {
                "large": "https://buzzedeal.com/upload/img.png",
                "small": "https://buzzedeal.com/upload/img.png",
                "original": "https://buzzedeal.com/upload/img.png"
            },
            "banner_link": "https://buzzedeal.com",
            "banner_priority": "7",
            "banner_start": "2017-02-28 00:00:00",
            "banner_end": "2017-08-01 00:00:00",
            "banner_type": null,
            "banner_flag": null
        },
        "total": "1"
    }
}

```
### Banner Detail

Search per banner

```
GET https://buzzedeal.com/rest/banner/detail/:category_id
```

Parameter | Type | Usage
------------ | -------------
`client_id [app_token]` | string | required
`client_secret [app_secret]` | string | required

```
The response should be like the following.

{
    "error": false,
    "results": {
        "banner_id": "1",
        "banner_active": "0",
        "banner_created": "2017-02-28 16:05:06",
        "banner_updated": "2017-06-22 23:05:46",
        "banner_image": {
            "large": "https://buzzedeal.com/upload/img.png",
            "small": "https://buzzedeal.com/upload/img.png",
            "original": "https://buzzedeal.com/upload/img.png"
        },
        "banner_link": "https://buzzedeal.com",
        "banner_priority": "7",
        "banner_start": "2017-02-28 00:00:00",
        "banner_end": "2018-01-01 00:00:00",
        "banner_type": null,
        "banner_flag": null
    }
}
```
