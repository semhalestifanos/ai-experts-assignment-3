# Bug Explanation

## What was the bug?
When the OAuth2 token was stored as a dictionary instead of an `OAuth2Token` object, the client did not refresh the token even if it was expired. As a result, the Authorization header was not set, causing API requests to be sent without authentication.

## Why did it happen?
The `request()` method only checked for expiration when the token was an `OAuth2Token` instance. Dictionary tokens were skipped entirely, so expired tokens were never refreshed.

## Why does the fix solve it?
The fix adds a condition to treat dictionary tokens with expired `expires_at` values as invalid. This ensures the client refreshes the token and sets the correct Authorization header before making API requests.

## One realistic edge case not covered
If the token dictionary is missing the `expires_at` key or contains invalid data types, the expiration check could fail or cause unexpected behavior. This edge case is not covered by the current tests.
