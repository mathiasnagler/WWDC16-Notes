# 708 - Advanced Notifications

- User Notifications have more content (title, subtitle, ..)
- Detail View: Specialized UI (Examples: Calendar, Find my Friends, Photos, Messages)
- New API
- **Media Attachments:**
    - Service Extensions (with e.g. `NSURLSession`) to download attachments (`UINotificationAttachment`)
    - Reference (= additional, custom key) to Attachment in Push-Payload
    - Supported by Local- & Remote-Notifications
    - Content-Types: Images (incl. Gifs), Audio, Video
    - Service Extensions have limited processing time and size (use scaled down / shorter assets)
    - Files managed by the system (separate location)
- **Custom UI:**
    - `UINotificationContentExtension` Protocol
    - Limitation: No User Interaction
    - 4 Sections: System Header, Custom-Content, Default-Content (Payload Content => Pre iOS 10), Actions
    - Created by Application Extension Template -> Notification Content (3 Files in New Target)
    - Protocol: `didReceiveNotification` method to update UI
    - Configuration in `Info.plist` with `UINotificationExtensionCategory` Array (Different types possible) 
    - Additional Custom Notification Payload available in `didReceiveNotification`
    - Hide Default Content: `UINotificationExtensionDefaultContentHidden` Flag in `Info.plist`
    - Use `preferedContentSize` / constraints for content sizing
    - System needs final size for correct animation: `UINotificationExtensionContentSizeRatio` in `Info.plist` defines Height / Width Ratio (Not always possible ¯\_(ツ)_/¯)
    - Media Attachments can be used in Custom UI.
- **Actions:**
    - Intercepting Action Response: Do Work, Update Custom UI, Delay dismissal of notification
    - Text Input Action hase more Options (Placeholder Text, Custom Accessory Input View)
- [https://developer.apple.com/wwdc16/708](https://developer.apple.com/wwdc16/708)

