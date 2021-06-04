## Authors
- Robbie McElrath <rmcelrath@google.com>

## Motivation
This proposal gives web applications a way to request that they be loaded with
all storage isolated from the user’s regular browsing context. This isolation
extends not just to resources within the app’s scope, but to all resources
loaded by the app, regardless of origin. This offers the user enhanced
security, as third party cookies are siloed between the app and the user’s
normal browsing context, and any data stored by the app in localStorage,
indexedDB, cookies, etc.. will not be accessible outside of the app itself.

## Behavior
An app with isolated storage should be provided the following guarantees by the
browser:
- When launching an app, all of its persisted state is loaded from and written
  to a dedicated area of storage that is only accessible from within the app
  itself.
- All descendent frames of the isolated app must also use the app’s dedicated
  storage partition, regardless of the frame’s site.
- Resources within the app’s scope that get loaded by a page from the user’s
  regular browsing context should not have access to the app’s dedicated
  storage partition.

## Manifest Changes
Opting into isolated storage can be achieved by setting a proposed new flag in
the app’s manifest: isolated_storage.

    {
      "name": "Example App",
      "start_url": "https://example.com/",
      "isolated_storage": true
    }
