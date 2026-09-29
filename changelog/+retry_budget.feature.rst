Added the ``retry_budget`` parameter to ``HTTPConnectionPool`` and
``HTTPSConnectionPool``. When set to an integer, the pool creates a
``urllib3.util.retry.RetryBudget`` of that size which is shared by every
thread using the pool: each retry must take a token out of the budget before
being issued, and each successful response puts one token back. This caps the
request amplification a failing origin can cause no matter how many requests
are in flight. Redirects do not consume the budget, and retries behave
exactly as before when no budget is configured.
