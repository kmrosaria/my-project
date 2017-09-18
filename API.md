Dealcha API
=======

Dealcha is Thailand’s #1 Cashback Website

*Current version: [v0.9.0][dist]*

[![Build Status](https://travis-ci.org/rstacruz/flatdoc.svg?branch=gh-pages)](https://dealcha.com)

How to create an App
---------------

1. [Log In](https://dealcha.com/login)
2. Go to [App Search](https://dealcha.com/developer/app/search)
3. [Create](https://dealcha.com/developer/app/create) an app

### How OAuth 2 Works

In [App Search](https://dealcha.com/developer/app/search), click the lock. This is what you redirect to get a user's permission.

### Example scope

```
https://www.dealcha.com/dialog/request?client_id=[app_token]&redirect_uri=[redirect url]&scope=user_profile
```

### Exchange code with a token

After the user approves of your app, they will be redirected back to the specified `[redirect url]` with a new URL parameter called `?code`. The last thing you need to do is exchange that code for a token. Using cURL, call the following.

POST https://dealcha.com/rest/access

Parameters

 - `client_id [app_token]`
 - `client_secret [app_secret]`
 - `code [code]`


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

POST https://dealcha.com/rest/signup

Parameters

 - `client_id`
 - `client_secret`
 - `profile_email`
 - `auth_password `
 - `confirm `
 - `promo_code [optional]`
 - `terms`

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
        "profile_image": "{\"large\": \"http://dealcha.dev/images/avatar/avatar-10.png\", \"small\": \"http://dealcha.dev/images/avatar/avatar-10.png\"}",
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

POST https://dealcha.com/rest/login

Parameters

 - `auth_slug`
 - `auth_password`
 - `client_id`
 - `client_secret`

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
            "profile_image": "{\"large\": \"http://dealcha.dev/images/avatar/avatar-10.png\", \"small\": \"http://dealcha.dev/images/avatar/avatar-10.png\"}",
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

POST https://dealcha.com/rest/forgot

Parameters

 - `auth_slug`
 - `client_id`
 - `client_secret`

```
The response should be similar to the following and the Dealcha will send the forgot password email to the user.

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
        "profile_image": "{\"large\": \"http://dealcha.dev/images/avatar/avatar-10.png\", \"small\": \"http://dealcha.dev/images/avatar/avatar-10.png\"}",
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

GET https://dealcha.com/rest/profile/detail/:profile_id?client_id=[app_token]&client_secret=[app_secret]

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
            "large": "http://dealcha.dev/images/avatar/avatar-10.png",
            "small": "http://dealcha.dev/images/avatar/avatar-10.png"
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

GET https://dealcha.com/rest/profile/search?client_id=[app_token]&client_secret=[app_secret]

Parameters

 - `order`
 - `filter`
 - `start`
 - `range`

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
                    "large": "http://dealcha.dev/images/avatar/avatar-10.png",
                    "small": "http://dealcha.dev/images/avatar/avatar-10.png"
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

POST https://dealcha.com/rest/profile/update/:profile_id?client_id=[app_token]&client_secret=[app_secret]

Change the `:profile_id` with the profile_id of the user and add the parameter you want to update. 

Parameters

 - `client_id`
 - `client_secret`
 - `profile_first`
 - `profile_last`
 - `profile_username`
 - `profile_email`
 - `profile_image`
 - `profile_phone`
 - `profile_gender`
 - `profile_birthday`
 - `profile_address`
    - `postal`
    - `country`
    - `street1`
    - `street2`
    - `district`
    - `province`

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
        "profile_image": "{\"large\":\"http:\\/\\/dealcha.dev\\/images\\/avatar\\/avatar-2.png\",\"small\":\"http:\\/\\/dealcha.dev\\/images\\/avatar\\/avatar-2.png\"}",
        "profile_updated": "2017-09-18 13:52:06",
        "original": {
            "client_id": "300aaf826a59b87b2d5a4ebb6e3d336c",
            "client_secret": "5ae9782cdddd1994c6d91da7ad22d593",
            "profile_last": "John",
            "profile_first": "Doe",
            "profile_id": "57093",
            "profile_image": "{\"large\":\"http:\\/\\/dealcha.dev\\/images\\/avatar\\/avatar-2.png\",\"small\":\"http:\\/\\/dealcha.dev\\/images\\/avatar\\/avatar-2.png\"}",
            "profile_updated": "2017-09-18 13:52:06"
        }
    }
}

```

Settings
------------

### Cashback Summary

Get cashback summaries and list of cashback according to status

GET https://dealcha.com/rest/settings/cashback-summary**/:profile_id?client_id=[app_token]&client_secret=[app_secret]&status=[status]

Change the `:profile_id` with the profile_id of the user. 

Parameters

 - `client_id`
 - `client_secret`
 - `order`
 - `filter`
 - `start`
 - `range`
 - `status` (Default Value: `pending`) 

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

GET https://dealcha.com/rest/settings/refer/:profile_id?client_id=[app_token]&client_secret=[app_secret]&status=[status]

Change the `:profile_id` with the profile_id of the user. 

Parameters

 - `client_id`
 - `client_secret`

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

POST https://dealcha.com/rest/settings/missing-cashback/:profile_id

Change the `:profile_id` with the profile_id of the user. 

Parameters

 - `client_id`
 - `client_secret`
 - `discrepancy_reference` (Shopping Trip)
 - `discrepancy_note` (Total Purchase Price)
 - `discrepancy_price` (Expected Cashback Amount)
 - `discrepancy_order_email` (Order Confirmation Email)
 - `discrepancy_images` (Order Confirmation Screenshot) (Optional)

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

GET https://dealcha.com/rest/store/search?client_id=[app_token]&client_secret=[app_secret]

Parameters

 - `order` (latest/popular/cashback/store)
 - `filter`
 - `start`
 - `range`

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
                    "large": "http://s3-ap-southeast-1.amazonaws.com/dealcha-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858",
                    "small": "http://s3-ap-southeast-1.amazonaws.com/dealcha-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858",
                    "original": "http://s3-ap-southeast-1.amazonaws.com/dealcha-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858"
                },
                "store_slug": "Lazada-s1",
                "store_link": "http://dealcha.dev/Lazada-s1/store",
                "store_root_url": "www.lazada.com.ph",
                "store_redirect": "http://dealcha.dev/redirect/store/1",
                "store_redirect_api": "http://dealcha.dev/rest/redirect/store/1?access_token=",
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

GET https://dealcha.com/rest/store/detail/:store_id?client_id=[app_token]&client_secret=[app_secret]

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
            "large": "http://s3-ap-southeast-1.amazonaws.com/dealcha-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858",
            "small": "http://s3-ap-southeast-1.amazonaws.com/dealcha-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858",
            "original": "http://s3-ap-southeast-1.amazonaws.com/dealcha-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858"
        },
        "store_slug": "Lazada-s1",
        "store_link": "http://dealcha.dev/Lazada-s1/store",
        "store_root_url": "www.lazada.com.ph",
        "store_redirect": "http://dealcha.dev/redirect/store/1",
        "store_description": "Lazada Description",
        "store_default_cashback": "0.00",
        "store_max_purchase": "100000.00",
        "store_max_cashback": "300.00"
    }
}

```

### Store Redirect

Get redirect link and shopping trips for store

GET https://dealcha.com/rest/redirect/store/:store_id/:profile_id?client_id=[app_token]&client_secret=[app_secret]

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

GET https://dealcha.com/rest/deal/search?client_id=[app_token]&client_secret=[app_secret]

Parameters

 - `order` (latest/popular/cashback/store)
 - `filter`
 - `start`
 - `range`

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
                "promotion_link": "https://dealcha.com/Lazada-Deal-Number-1-P1/deal",
                "promotion_redirect": "https://dealcha.com//redirect/promotion/1",
                "promotion_images": [
                    {
                        "large": "https://dealcha-v2.s3-ap-southeast-1.amazonaws.com/upload/6f4859c0c981c6809e60900552aee4b13.png",
                        "small": "https://dealcha-v2.s3-ap-southeast-1.amazonaws.com/upload/6f4859c0c981c6809e60900552aee4b12.png",
                        "original": "https://dealcha-v2.s3-ap-southeast-1.amazonaws.com/upload/6f4859c0c981c6809e60900552aee4b11.png"
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
                    "large": "http://s3-ap-southeast-1.amazonaws.com/dealcha-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858",
                    "small": "http://s3-ap-southeast-1.amazonaws.com/dealcha-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858",
                    "original": "http://s3-ap-southeast-1.amazonaws.com/dealcha-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858"
                },
                "store_slug": "Lazada-s1",
                "store_link": "http://dealcha.dev/Lazada-s1/store",
                "store_redirect": "http://dealcha.dev/redirect/store/1",
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

GET https://dealcha.com/rest/Deal/detail/:promotion_id?client_id=[app_token]&client_secret=[app_secret]

```
The response should be like the following.

{
    "error": false,
    "results": {
        "promotion_id": "1",
        "promotion_title": "Lazada Deal Number 1",
        "promotion_slug": "Lazada-Deal-Number-1-P1",
        "promotion_link": "https://dealcha.com/Lazada-Deal-Number-1-P1/deal",
        "promotion_redirect": "https://dealcha.com//redirect/promotion/1",
        "promotion_images": [
            {
                "large": "https://dealcha-v2.s3-ap-southeast-1.amazonaws.com/upload/6f4859c0c981c6809e60900552aee4b13.png",
                "small": "https://dealcha-v2.s3-ap-southeast-1.amazonaws.com/upload/6f4859c0c981c6809e60900552aee4b12.png",
                "original": "https://dealcha-v2.s3-ap-southeast-1.amazonaws.com/upload/6f4859c0c981c6809e60900552aee4b11.png"
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
            "large": "http://s3-ap-southeast-1.amazonaws.com/dealcha-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858",
            "small": "http://s3-ap-southeast-1.amazonaws.com/dealcha-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858",
            "original": "http://s3-ap-southeast-1.amazonaws.com/dealcha-upload/stores/thumbnail_images/000/000/001/original/Lazada_logo.png?1462513858"
        },
        "store_slug": "Lazada-s1",
        "store_link": "http://dealcha.dev/Lazada-s1/store",
        "store_redirect": "http://dealcha.dev/redirect/store/1",
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

GET https://dealcha.com/rest/redirect/promotion/:promotion/:profile_id?client_id=[app_token]&client_secret=[app_secret]

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

GET https://dealcha.com/rest/category/search?client_id=[app_token]&client_secret=[app_secret]

Parameters

 - `order`
 - `filter`
 - `start`
 - `range`

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

GET https://dealcha.com/rest/category/detail/:category_id?client_id=[app_token]&client_secret=[app_secret]

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

GET https://dealcha.com/rest/banner/search?client_id=[app_token]&client_secret=[app_secret]

Parameters

 - `order`
 - `filter`
 - `start`
 - `range`

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
                "large": "https://dealcha-v2.s3-ap-southeast-1.amazonaws.com/upload/f8153b4810a0f87122776b210db0ebbf2.png",
                "small": "https://dealcha-v2.s3-ap-southeast-1.amazonaws.com/upload/f8153b4810a0f87122776b210db0ebbf3.png",
                "original": "https://dealcha-v2.s3-ap-southeast-1.amazonaws.com/upload/f8153b4810a0f87122776b210db0ebbf1.png"
            },
            "banner_link": "https://dealcha.com/article/how-it-works",
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

GET https://dealcha.com/rest/banner/detail/:category_id?client_id=[app_token]&client_secret=[app_secret]

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
            "large": "https://dealcha-dev.s3-ap-southeast-1.amazonaws.com/upload/eb7be4d26db2a434ab6a50d588a1710e2.png",
            "small": "https://dealcha-dev.s3-ap-southeast-1.amazonaws.com/upload/eb7be4d26db2a434ab6a50d588a1710e3.png",
            "original": "https://dealcha-dev.s3-ap-southeast-1.amazonaws.com/upload/eb7be4d26db2a434ab6a50d588a1710e1.png"
        },
        "banner_link": "https://dealcha.com/article/how-it-works",
        "banner_priority": "7",
        "banner_start": "2017-02-28 00:00:00",
        "banner_end": "2018-01-01 00:00:00",
        "banner_type": null,
        "banner_flag": null
    }
}
```

How it works
------------

Flatdoc is a hosted `.js` file (along with a theme and its assets) that you can
add into any page hosted anywhere.

#### All client-side

There are no build scripts or 3rd-party services involved. Everything is done in
the browser. Worried about performance? Oh, It's pretty fast.

Flatdoc utilizes the [GitHub API] to fetch your project's Readme files. You may
also configure it to fetch any arbitrary URL via AJAX.

#### Lightning-fast parsing

Next, it uses [marked], an extremely fast Markdown parser that has support for
GitHub flavored Markdown.

Flatdoc then simply renders *menu* and *content* DOM elements to your HTML
document. Flatdoc also comes with a default theme to style your page for you, or
you may opt to create your own styles.

Markdown extras
---------------

Flatdoc offers a few harmless, unobtrusive extras that come in handy in building
documentation sites.

#### Code highlighting

You can use Markdown code fences to make syntax-highlighted text. Simply
surround your text with three backticks. This works in GitHub as well.
See [GitHub Syntax Highlighting][fences] for more info.

    ``` html
    <strong>Hola, mundo</strong>
    ```

#### Blockquotes

Blockquotes show up as side figures. This is useful for providing side
information or non-code examples.

> Blockquotes are blocks that begin with `>`.

#### Smart quotes

Single quotes, double quotes, and double-hyphens are automatically replaced to
their typographically-accurate equivalent. This, of course, does not apply to
`<code>` and `<pre>` blocks to leave code alone.

> "From a certain point onward there is no longer any turning back. That is the
> point that must be reached."  
> --Franz Kafka

#### Buttons

If your link text has a `>` at the end (for instance: `Continue >`), they show
up as buttons.

> [View in GitHub >][project]

Customizing
===========

Basic
-----

### Theme options

For the default theme (*theme-white*), You can set theme options by adding
classes to the `<body>` element. The available options are:

#### big-h3
Makes 3rd-level headings bigger.

``` html
<body class='big-h3'>
```

#### no-literate
Disables "literate" mode, where code appears on the right and content text
appear on the left.

``` html
<body class='no-literate'>
```

#### large-brief
Makes the opening paragraph large.

``` html
<body class='large-brief'>
```

### Adding more markup

You have full control over the HTML file, just add markup wherever you see fit.
As long as you leave `role='flatdoc-content'` and `role='flatdoc-menu'` empty as
they are, you'll be fine.

Here are some ideas to get you started.

 * Add a CSS file to make your own CSS adjustments.
 * Add a 'Tweet' button on top.
 * Add Google Analytics.
 * Use CSS to style the IDs in menus (`#acknowledgements + p`).

### JavaScript hooks

Flatdoc emits the events `flatdoc:loading` and `flatdoc:ready` to help you make
custom behavior when the document loads.

``` js
$(document).on('flatdoc:ready', function() {
  // I don't like this section to appear
  $("#acknowledgements").remove();
});
```

Full customization
------------------

You don't have to be restricted to the given theme. Flatdoc is just really one
`.js` file that expects 2 HTML elements (for *menu* and *content*). Start with
the blank template and customize as you see fit.

[Get blank template >][template]

Misc
====

Inspirations
------------

The following projects have inspired Flatdoc.

 * [Backbone.js] - `Jeremy's projects have always adopted this "one page`
 documentation" approach which I really love.

 * [Docco] - `Jeremy's Docco introduced me to the world of literate programming,`
 and side-by-side documentation in general.

 * [Stripe] - `Flatdoc took inspiration on the look of their API documentation.`

 * [DocumentUp] - `This service has the same idea but does a hosted readme `
 parsing approach.

Attributions
------------

[Photo](http://www.flickr.com/photos/doug88888/2953428679/) taken from Flickr,
licensed under Creative Commons.

Acknowledgements
----------------

© 2013, 2014, Rico Sta. Cruz. Released under the [MIT 
License](http://www.opensource.org/licenses/mit-license.php).

**Flatdoc** is authored and maintained by [Rico Sta. Cruz][rsc] with help from its 
[contributors][c].

 * [My website](http://ricostacruz.com) (ricostacruz.com)
 * [Github](http://github.com/rstacruz) (@rstacruz)
 * [Twitter](http://twitter.com/rstacruz) (@rstacruz)

[rsc]: http://ricostacruz.com
[c]:   http://github.com/rstacruz/flatdoc/contributors

[GitHub API]: http://github.com/api
[marked]: https://github.com/chjj/marked
[Backbone.js]: http://backbonejs.org
[dox]: https://github.com/visionmedia/dox
[Stripe]: https://stripe.com/docs/api
[Docco]: http://jashkenas.github.com/docco
[GitHub pages]: https://pages.github.com
[fences]:https://help.github.com/articles/github-flavored-markdown#syntax-highlighting
[DocumentUp]: http://documentup.com

[project]: https://github.com/rstacruz/flatdoc
[template]: https://github.com/rstacruz/flatdoc/raw/gh-pages/templates/template.html
[blank]: https://github.com/rstacruz/flatdoc/raw/gh-pages/templates/blank.html
[dist]: https://github.com/rstacruz/flatdoc/tree/gh-pages/v/0.9.0
