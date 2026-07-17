# OWASP Juice Shop — Close All UI Notifications Challenge Reflection
### Investigation Process

I began by inspecting the notification UI element using browser developer tools, following the challenge hint.

My first instinct was to inspect the close button and its event listener. This showed that clicking the button triggered ```notification-closing``` behaviour, but the button itself was only the entry point.

Instead of following the button classes (```mat-mdc-button```, etc.), I traced the parent notification component and found:

```<app-challenge-solved-notification>```

This identified the Angular component responsible for the notification feature.

Searching for this component in the JavaScript led me to the component logic. Inside it, I found the notification state:

```notifications```

and the function responsible for removing notifications:

```closeNotification(e, i = !1)```

The function contained two different behaviours:

```i ? this.notifications = [] : this.notifications.splice(e, 1)```

This showed that:

- ```splice()``` removed one notification.
- Setting ```notifications = []``` cleared all notifications.

The next step was finding what controlled the second parameter ```(i)```. Tracing where the function was called revealed:

```closeNotification(s, n.shiftKey)```

This showed that the behaviour depended on the keyboard state during the click event.

```shiftKey``` is a browser event property:

- Normal click → ```shiftKey = false``` → remove one notification.
- Shift + click → ```shiftKey = true``` → clear all notifications.

Holding Shift while clicking the close button triggered the correct behaviour and completed the challenge.

### Lessons Learned

The biggest lesson was understanding how to trace functionality through a modern web application.

### The useful investigation path was:

1. Visible UI element

2. Find owning component

3. Find state/data being modified

4. Find function changing the state

5. Trace function arguments

6. Identify the user action that changes behaviour

I initially spent time looking through framework-generated code such as Angular Material classes and polyfills. These were not useful because they belonged to the framework rather than the application's logic.

For future challenges, I will first identify the component responsible for the feature and follow the application's data flow instead of getting distracted by framework internals.
