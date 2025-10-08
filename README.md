# Explanation

## 📌 Concept Check

1. Route vs Deep Link

A Flutter route works only inside the app, managed by the `Navigator` (e.g., `/details`). A deep link, on the other hand, starts outside the app — it’s a URL (e.g., `myapp://details 42`) that Android recognizes and uses to launch your app at a specific entry point.

2. Why Android Needs an Intent Filter

The intent filter tells Android when and how your app should respond to certain links or actions. Without it, Android simply won’t know that your app can handle `myapp://` URLs.

## 🧰 Technical Understanding

3. Role of `uni_links`

`uni_links` acts as the bridge between Android’s deep link intent and Flutter’s navigation system.
- `getInitialUri()` handles links when the app is launched.
- `uriLinkStream` handles links received while the app is already open.

4. Deep Link While App Is Running

If a deep link is triggered while the app is running, the new intent is delivered immediately. The `uriLinkStream` listener reacts and navigates the user to the correct page without a restart.

## 🐞 Debugging Insight

5. adb Opens App but Doesn’t Navigate

The first things to check are:
- The intent filter in `AndroidManifest.xml` — the scheme and host must match the link exactly.
- The link handling code — make sure `_handleIncomingLink` parses the URI correctly and calls `Navigator.push`.

If either part is off, the app may open but won’t navigate to the detail page.