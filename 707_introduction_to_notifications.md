## 707 - Introduction to Notifications

* `UNNotification` on iOS, tvOS and watchOS
* Single code path for remote and local notification
* option for presenting notification ui while app is open
* Notification title and subtitle now always shown on iOS
* Shared badging possible with local and remote notifications in same app
* Media attachments in notifications possible for all apps
* Easier scheduling of local notifications
* Triggers for remote notifications are: interval, date, location
* `UNUserNotificationCenterDelegate` for presenting notifications in app
* Notifications can be updated after the have been presented to aggregate informations
* Three types of actions: open, custom actions, custom dismiss action
* Custom actions can run in background or launch app and run in foreground
* Callback when user dismisses notification using custom dismiss actions
* React to notification actions in `UNUserNotificationCenterDelegate userNotification(didReceiveUpdate:)`
* Service extension: non UI extension that augments or replaces notification contents **before** displayed
