---
layout: default
title: Events Listing
nav_order: 1
parent: Events
<!-- permalink: /docs/events/events-listing -->
---

# Events Listing

All the events created by the logged in user will be listed here as `Upcoming` and `Past` events.
{: .fs-6 .fw-300 }

### No Events

When no events are present in the list, we display a message and a button for creating event. This is done by calling the below function and passing the required bool value.

      func displayNoEventsView(status: Bool)

The message text displayed when no events present, is decided based on user default key `NEW_USER`.       

### Skeleton Loading View

Cocoapod `SkeletonView` is used for displaying an animated loading view until events are loaded.

A bool variable `showSkeleton` is used for changing the state of loading view. The table is reloaded and in tableview cell configuration, we display the `SKELETON` cell and call below function to show animating view.

      func configureSkeleton()

Below function is used to reset the loading state.

      func resetLoadingState()


### Drafts

If any events are not posted, or are not configured, those events are stored locally in drafts. The count and message is displayed using a table cell `DRAFTS` in the `0` section of the table.

*Currently the `NoEventsView` is not shown when events list is empty but drafts are present. It is supposed to change.*


### Pagination

Cocoapod `PaginatedTableView` is used to enable pagination in the listing table view. Currently the page size is `5`.

      func loadMore(...)

The above function is invoked automatically by the tableview on reload and on table scroll.

If the page number is `1` in this function, it means that the table was pulled to refresh, so we empty the events list array and fetch events from `LocalStorageEngine`.


### Table Cells

**Drafts** : To be shown in case of draft events present. It will always be displayed on the top.

**Skeleton** : To be shown when events are being loaded. Number of rows delegate method has a constant value `3` for number of loader cells.

**Upcoming** : `Upcoming` and `Open` events are displayed using this cell. The background colour for `Open` events is provided in `cellForRowAt(indexPath)` as a shade of dark blue.

**Past** : Grayed out cards will be shown for events for which the start time is in past. Events that are currently running will also be shown in past events.

The cell will display option for leaving a review for the event venue if the user haven't already reviewed. This is decided by checking `hasreview` key in the event data.

## Process in Event Cell

* Prepare the event date :

      let dateFormatter = DateFormatter()
      dateFormatter.locale = NSLocale(localeIdentifier: "en_US_POSIX") as Locale
      let eventStartTime = event["StartTime"] as? String
      let eventEndTime = event["EndTime"] as? String
      dateFormatter.dateFormat = "yyyy/MM/dd hh:mm a"
      let eventDate = event["EventDate"] as? String
      let eventDateTime = eventDate! + " " + eventStartTime!
      let eventEndDateTime = eventDate! + " " + (eventEndTime ?? "")

      let date = dateFormatter.date(from: eventDateTime)?.toLocalTime()

* This `date` will be used for displaying date and time related fields in the event cell. Based on whether the date is in past, it is shown in `Past` cell.

* Depending on the value of `EventType`, the type of event is identified.

  `EventType == 1` means event is of type `Advanced`

  `EventType == 2` means event is of type `Quick`

  `EventType == 3` means event is of type `Open`

* Set button tags for identifying tap action.

* Set event title. For `Open` and `Advanced` events, the title is displayed using `EventName` key, while in case of `Quick` event, key name is `InvitationMessage`.

* Set date and time for event. In case of `Quick` events, the time will not be in the format `from-to`, but in the format of `Around hh:mm am/pm`

* The cell has a subview `ParticipantsView` which is used for displaying round user images. This is done using a separate function

      func arrangeParticipants(...)


### Push Notification

In case the app is launched by opening a push notification regarding event, its event id is set in the `eventIdByPushNotification` variable in the `AppDelegate` push notification handler.

In `viewWillAppear` it is checked if the `eventIdByPushNotification` has a valid value. If it has an event id, the navigation is set to Event Detail with the received event id.


### Tutorial

When user logs in for the first time, there's a check in `viewWillAppear` that checks whether the user defaults key `TUTORIAL` is set. If it is not set, then `TutorialView` is displayed. 
