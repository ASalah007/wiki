[<< Back](./index.md)

# Dajngo Managers in a nutshell

- To rename the default name of the manager

```py
class Model1(models.Model):
    new_name = models.Manager()
```

- two reasons to extends the default manager:
  1. to add extra functions
  2. to modify the initial query set the manager returns

```
class CustomManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().filter(author='blah blah')

# then add to the model class

class CustomModel(models.Model):
    objects = CustomManager()
```

- django consider the first manager it sees in the model as the **default manager** which is used by django in different places like data_dump
