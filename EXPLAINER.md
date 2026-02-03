# Playto Engineering Challenge – Explainer

## The Tree

Nested comments were implemented using an adjacency list model.

Each comment contains a self-referencing `parent` field that points to another comment in the same table.  
Top-level comments have `parent = NULL`, while replies store the parent comment ID. This allows unlimited nesting while keeping the database schema simple and flexible.

To avoid the N+1 query problem, all comments related to a post are fetched in a single database query using `select_related` and `prefetch_related`.  
The comment hierarchy is then constructed in memory using a dictionary-based lookup, ensuring efficient serialization without triggering additional database queries.

This approach provides:
- Efficient retrieval of deeply nested comment threads
- Constant number of database queries
- Good performance even with large datasets

---

## The Math

The leaderboard is calculated dynamically from karma activity records instead of storing derived values on the User model.

```python
from django.utils.timezone import now
from datetime import timedelta
from django.db.models import Sum

leaderboard = (
    KarmaActivity.objects
    .filter(created_at__gte=now() - timedelta(hours=24))
    .values("user__id", "user__username")
    .annotate(total_karma=Sum("points"))
    .order_by("-total_karma")[:5]
)
