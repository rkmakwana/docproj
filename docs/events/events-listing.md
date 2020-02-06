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

A bool varilable `showSkeleton` is used for changing the state of loading view. The table is reloaded and in tableview cell configuration, we display the `SKELETON` cell and call below function to show animating view.

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

Table Cells

Push Notification
