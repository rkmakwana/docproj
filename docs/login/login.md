---
layout: default
title: Login
nav_order: 3
has_children: true
permalink: /docs/login
---

# Login

Show the screen when :
* no user is logged in.
* first launch after app install.
* user logged out.
* user logged out because of session expiration.

#### Working

User selects their country using the country picker. We are using a cocoapod `CountryPickerView` for country picker.

User enters their mobile number and presses the submit button.

An api `GetUserRequest` is called which creates a new record in the database if it is a new user, or returns the user data if it is for an existing user.

Once the user id is available by this api call's response, a new authentication token is generated, and the token is saved and used for the subsequent api calls.



There are following scenarios in this api's response:

**1. Received complete user data:**

If the user logs in on the same device as previously logged in, no `otp` will be generated, and the user's details will be provided in the api response.

The api response will have `status = 1`, and `UsreData` field with the user's details. These details are saved in `UserDefaults` and the `UserProfile` shared instance is allocated with the received details.

The `ChatEngine`, `ContactsEngine` and `LocationEngine` are started.

Push notification device token is sent to the server by calling an api `UpdateUserNotificationId`.

A function is then called to navigate to the landing tab bar controller

     func saveUserProfileAndProceedFurther()
     func navigateAfterVerification(user: User)

*A user is said to be registered if the `email` of user is not empty. If the email is empty, the user is navigated to `SetUpProfileVC` for completing the registration*

**2. Received only `userID`:**

In any case other than above case, an `otp` is generated and sent to the provided mobile number.

The api returns the user id, which is saved locally, and the user is navigated to the `OTPVerificationVC` screen, using below function.

      func navigateToVerification()
