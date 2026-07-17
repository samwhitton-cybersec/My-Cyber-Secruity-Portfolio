# OWASP Juice Shop — Close All UI Notifications Challenge Reflection

I started by inspecting the notification element in the browser developer tools, following the hint provided. Initially, I looked at the close button and its event listeners, but I found that the button itself was only the trigger and not where the main logic was stored.

I then traced the parent component and found the Angular component:

```<app-challenge-solved-notification>```

This led me to the component logic where I found the notifications collection and the ```closeNotification()``` function.

The important discovery was that ```closeNotification()``` had two behaviours:

Normal use removed a single notification.
A second parameter allowed all notifications to be cleared.

By tracing where this parameter came from, I found:

```closeNotification(s, n.shiftKey)```

This showed that holding the ```Shift key``` while clicking changed the behaviour because shiftKey became true.

The challenge was solved by using ```Shift + click``` on the close button.

## Reflection

The main lesson I learned was to follow the application logic rather than getting stuck in framework code. At first I spent time looking through Angular Material classes and JavaScript bundles, but the useful path was:

```UI element → Component → Function → Parameters → Behaviour```

For future challenges, I will focus on identifying the component responsible for the feature, then trace the data flow and event handling from there.
