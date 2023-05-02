# swiftui_handle_modal_showing_error

you need to present the share sheet from the topmost view controller, not the root view controller. try this code:
```swift


 func presentShareSheet(activityItems: [Any]) {
    let activityController = UIActivityViewController(activityItems: activityItems, applicationActivities: nil)
    guard var topVC = UIApplication.shared.windows.first?.rootViewController else {
        return
    }
    // iterate til we find the topmost presented view controller
    // if you don't you'll get an error since you can't present 2 vcs from the same level
    while let presentedVC = topVC.presentedViewController {
        topVC = presentedVC
    }
    
    topVC.present(activityController, animated: true)
}
```
