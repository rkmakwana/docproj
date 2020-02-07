---
layout: default
title: Events Detail
nav_order: 2
parent: Events
<!-- permalink: /docs/events/events-detail -->
---

# Events Details

Display all the details for the given event id `eventIdentifier`.
{: .fs-6 .fw-300 }

On `viewDidLoad` event details are fetched using the given event id and api `GetEventData`. The response is then sorted an categorised into separate sections and store it in the dictionary `valueDict`. Another array `sectionKeys` holds the string values of the various sections that should be displayed for the given event.

      func prepareScreenSections()

### Event Deleted

In case an event is deleted by the user, and it's event id is used to display the details screen, `Status == 2`, then an alert is shown and navigated to the previous screen.

### Media

Check if media attachment available in the event by key `EventPhoto`. This will give the url of the media.

In case of media of video type `InvitationMediaType == 3`, the string will contain two urls separated by `|` symbol. First url will be for the media thumbnail image and second url will be of the video.

### Invitees

The invitee list is fetched by the key `EventUsersList` and is processed in following order:

* If userId of the participant is available, query local database for the user by userId

    * If found, use the fetched user.
    * If not found, create a new `GoodTimeContacts` instance with the user details found in the json object.

* If userId not available, query the local database for the user by mobile number.

    * If found, use the fetched user.
    * If not found, create a new `GoodTimeContacts` instance with the mobile number and `No Name` as the user name.

### Sort by coming status (For quick and advanced events)

The invitees are categorised into 4 categories `Coming`, `Not Coming`, `May Come`, `No Response`. This is handled by the function `func sortParticipantStatus(...)`

***Note: Past events cannot be edited.***

### Table View

The data is displayed on the screen by making use of the flexibility and dynamic abilities of a `UITableView`. The positive point of using a table is that we can :
* show/hide whole section easily
* the height of the cells can be dynamic according to the content
* code for each section can be isolated in the cell class for clarity and readability.
* the cells are reused between `EventDetailsController`, `InviteDetailsController` and `EventCreateController`, as they have similar functionality.
