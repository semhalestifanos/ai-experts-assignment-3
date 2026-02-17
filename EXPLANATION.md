# Bug Explanation

## What was the bug?
When the OAuth2 token was stored as a dictionary instead of an `OAuth2Token` object, the client did not refresh the token even if it was expired. As a result, the Authorization header was not set, causing API requests to be sent without authentication.

## Why did it happen?
The `request()` method only checked for expiration when the token was an `OAuth2Token` instance.# Bug Explanation

## What was the bug?
When the OAuth2 token was stored as a dictionary instead of an `OAuth2Token` object, the client did not refresh the token even if it was expired. As a result, the Authorization header was not set, causing API requests to be sent without authentication.

## Why did it happen?
The `request()` method only checked for expiration when the token was an `OAuth2Token` instance. If the token was a dictionary, it skipped the expiration logic entirely, even when `expires_at` indicated the token was expired.

## Why does the fix solve it?
The fix adds a condition to treat dictionary tokens with expired `expires_at` values as invalid. This ensures the client refreshes the token and sets the correct Authorization header before making the request.

## One edge case not covered
The tests do not cover cases where the token dictionary is missing the `expires_at` field or contains invalid data types. This could cause unexpected behavior during expiration checks.
If the token was a dictionary, it skipped the expiration logic entirely, even when `expires_at` indicated the token was expired.

## Why does the fix solve it?
The fix adds a condition to treat dictionary tokens with expired `expires_at` values as invalid. This ensures the client refreshes the token and sets the correct Authorization header before making the request.

## One edge case not covered
The tests do not cover cases where the token dictionary is missing the `expires_at` field or contains invalid data types. This could cause unexpected behavior during expiration checks.
