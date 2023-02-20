# Transactions

- you can make each http request run inside a transaction by applying the option _ATOMIC_REQUIESTS_ in the database settings
- to make a view run inside a transaction you use the **atomic decorator** or the context manager

```
from django.db import transaction

@transaction.atomic
def viewfunc(request):
    # this code will run inside of a transaction
    do_stuff()

```

```
from django.db import IntegrityError, transaction

def viewfunc(request):
    # this code is executed in an autocommit fassion
    do_stuff()

    with transaction.atomic():
        transactional_stuff()
```
