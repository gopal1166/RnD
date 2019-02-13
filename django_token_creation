#### To generate/create Token after the registration of new user we use signals
#### signals.py
```
from django.conf import settings
from django.db.models.signals import post_save
from django.dispatch import receiver
from rest_framework.authtoken.models import Token

@receiver(post_save, sender=settings.AUTH_USER_MODEL)
def create_auth_token(sender, instance=None, created=False, **kwargs):
    if created:
        Token.objects.create(user=instance)
```
#### then import these signals in models.py
```
from django.db.models import signals

/*Define custom user model here*/
import signals
```
Now in admin panel we create a new user and check the token is created or not on post new user creation.
