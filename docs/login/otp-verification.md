---
layout: default
title: OTP Verification
nav_order: 1
parent: Login
<!-- permalink: /docs/login/otp-verification -->
---

# OTP Verification

Once a user submits thier mobile number on the login screen, and an `otp` is generated, the user is navigated to this screen.

The user has to input the `otp` received in the text field, and tap submit button. This triggers an api `userVerification`.

This api returns the user's details. Authentication api is called to generate a new auth token.

The `ChatEngine`, `ContactsEngine` and `LocationEngine` are started.

Push notification device token is sent to the server by calling an api `UpdateUserNotificationId`.


if the response contains complete user details, then navigated to the tab bar controller.

In all other cases, navigate to `SetUpProfileVC` for setting up the profile.

There is a counter that ticks for the time of **60 seconds**. After this time interval, the user can use the resend code button to generate a new otp.
