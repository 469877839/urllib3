Added opt-in per-origin retry budgets to ``PoolManager`` via the new
``retry_budget`` parameter. When set, each origin gets a
``urllib3.util.retry.RetryBudget`` shared by all requests to that origin:
every retry spends one token and every successful response replenishes one,
so concurrent clients fail fast with ``MaxRetryError`` instead of
amplifying load against an unhealthy server.
