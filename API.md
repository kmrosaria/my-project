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



```
POST https://dealcha.com/rest/access

 - `client_id [app_token]`
 - `client_secret [app_secret]`
 - `code [code]`


This should return a session token similar to the following.

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

Account Authentication
------------

Getting Account Information. 

### Sign Up

Signin up a user via API.

```
POST https://dealcha.com/rest/signup

 - `client_id`
 - `client_secret`
 - `profile_email`
 - `auth_password `
 - `confirm `
 - `promo_code [optional]`
 - `terms`

The response should be similar to the following and this will response the data for your session. The user will also recieve a confirmation email.

{
    "error": false,
    "results": {
        "auth_id": "56864",
        "auth_slug": "johndoe@gmail.com",
        "auth_token": "90298c3d08e1a8135aa58305de35db5c",
        "auth_facebook_token": null,
        "auth_permissions": "public_product,public_profile,personal_profile,personal_product,personal_comment,personal_review",
        "auth_type": null,
        "auth_active": "0",
        "auth_created": "2017-09-15 15:38:26",
        "auth_updated": "2017-09-15 15:38:26",
        "profile_id": "56923",
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

```
POST https://dealcha.com/rest/login

 - `auth_slug`
 - `auth_password`
 - `client_id`
 - `client_secret`

The response should be similar to the following and this will response the data for your session.

{
    "error": false,
    "results": {
        "error": false,
        "results": {
            "auth_id": "56864",
            "auth_slug": "johndoe@gmail.com",
            "auth_token": "90298c3d08e1a8135aa58305de35db5c",
            "auth_facebook_token": null,
            "auth_permissions": "public_product,public_profile,personal_profile,personal_product,personal_comment,personal_review",
            "auth_type": null,
            "auth_active": "0",
            "auth_created": "2017-09-15 15:38:26",
            "auth_updated": "2017-09-15 15:38:26",
            "profile_id": "56923",
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

```
POST https://dealcha.com/rest/forgot

 - `auth_slug`
 - `client_id`
 - `client_secret`

The response should be similar to the following and the Dealcha will send the forgot password email to the user.

{
    "error": false,
    "results": {
        "auth_id": "56864",
        "auth_slug": "johndoe@gmail.com",
        "auth_token": "90298c3d08e1a8135aa58305de35db5c",
        "auth_facebook_token": null,
        "auth_permissions": "public_product,public_profile,personal_profile,personal_product,personal_comment,personal_review",
        "auth_type": null,
        "auth_active": "0",
        "auth_created": "2017-09-15 15:38:26",
        "auth_updated": "2017-09-15 15:38:26",
        "profile_id": "56923",
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

```
GET https://dealcha.com/rest/profile/detail/:profile_id?client_id=[app_token]&client_secret=[app_secret]

Change the `:profile_id` with the profile_id of the user and the response should be profile detail for the `user`.

{
    "error": false,
    "results": {
        "profile_id": "56923",
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

```
GET https://dealcha.com/rest/profile/search?client_id=[app_token]&client_secret=[app_secret]

Parameters
 - `order`
 - `filter`
 - `start`
 - `range`

The response should be like the following.

{
    "error": false,
    "results": {
        "rows": [
            {
                "profile_id": "56923",
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

```
POST https://dealcha.com/rest/profile/update/:profile_id?client_id=[app_token]&client_secret=[app_secret]

Change the `:profile_id` with the profile_id of the user and add the parameter you want to update. 
The reponse should be like the following.

The response should be like the following.

{
    "error": false,
    "results": {
        "rows": [
            {
                "profile_id": "1",
                "profile_active": "1",
                "profile_created": "2015-09-11 00:06:24",
                "profile_updated": "2017-07-03 10:53:07",
                "profile_first": "admin",
                "profile_last": "admin",
                "profile_username": "Dealcha Admin",
                "profile_email": "admin@dealcha.com",
                "profile_image": {
                    "large": "http://dealcha.com/images/avatar/avatar-2.png",
                    "small": "http://dealcha.com/images/avatar/avatar-2.png"
                },
                "profile_phone": "0853139829",
                "profile_gender": null,
                "profile_birthdate": null,
                "profile_address": {
                    "postal": "",
                    "country": "",
                    "street1": "test",
                    "street2": "test",
                    "district": "",
                    "province": ""
                },
                "profile_channel_transfer": "bank",
                "profile_bank_name": "Kbank",
                "profile_bank_account_name": "Tanun Chalermsinsuwan",
                "profile_bank_account_number": "630215183923332",
                "profile_paypal_account_name": null,
                "profile_paypal_account_number": null,
                "profile_code": null,
                "profile_type": null,
                "profile_flag": "1"
            },
        "total": "1"
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
