---
layout: default
title: Set Up Profile
nav_order: 2
parent: Login
<!-- permalink: /docs/login/setup-profile -->
---

# Set Up Profile

User is required to setup their profile when they register for the first time. This screen will be shown based on the value of `emailID` field. If email id is not provided, user will be displayed this screen
{: .fs-6 .fw-300 }

### Social Accounts

Users can use `Facebook`, `Twitter` and `LinkedIn` to fetch their respective profile. The received data - name, email, picture and gender (if provided), are filled in the user's profile.

### Fields

Profile picture is converted into `base64encoded` string for saving in database.

`Name` and `EmailId` fields are mandatory. Other fields are optional and can be left blank.

### Submission

On `Next` button press, the data is validated and api `UserPersonalData_v1` is called to save the user's profile data.

On api call success, the user's data is saved locally and `UserProfile` shared instance is allocated. `ChatEngine`, `ContactsEngine` are started, and user is navigated to `SetUpInterestVC`.

### Set Up Interests

This screen is showed just after the user submits the profile details.

Currently, these interests are not used anywhere in the app.

The user is then navigated to the Tab bar screen by using the `SideDrawerController` singleton.

***Both these screens will be showed only once, i.e on the first login.***
