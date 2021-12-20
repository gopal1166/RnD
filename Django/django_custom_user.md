#### creating custom user profile in djagno.
if we want to add some profile information, we can extend the AbstractUser class  
Why shoud we extend AbstractBaseUser?  
tell it what field represents the username, what fields are required, and how to manage those users, authentication
```
# -*- coding: utf-8 -*-
from __future__ import unicode_literals

from django.db import models
from django.contrib.auth.models import AbstractBaseUser
from django.contrib.auth.models import PermissionsMixin
from django.contrib.auth.models import BaseUserManager
from django.contrib.auth.models import UserManager
from datetime import datetime
from django.utils import timezone
from django.db.models import signals
from django.contrib.contenttypes import fields
from django.contrib.contenttypes.models import ContentType
from django.db import models
from django.utils.dates import MONTHS

class UserProfileManager(BaseUserManager):
    """Helps Django work with our custom model"""

    def create_user(self, email, name, password=None):
        """Creats a new user profile object"""

        if not email:
            raise ValueError('Not a valid email')
        email = self.normalize_email(email)
        user = self.model(email=email, name=name)
        user.set_password(password)
        user.save(using=self._db)
        return user

    def create_superuser(self, email, name, password):
        """Creates and save a new superuser object"""

        user = self.create_user(email, name, password)
        user.is_superuser = True
        user.is_staff = True
        user.save(using=self._db)
        return user


class UserProfile(AbstractBaseUser, PermissionsMixin):
    """Refers to user's profile """

    email = models.EmailField(max_length=255, unique=True)
    name = models.CharField(max_length=255)
    is_active = models.BooleanField(default=True)
    is_staff = models.BooleanField(default=False)

    objects = UserProfileManager()

    USERNAME_FIELD = 'email'
    REQUIRED_FIELDS = ['name']

    def get_full_name(self):
        """returns full name of the user"""
        return self.name

    def get_short_name(self):
        """returns short name of user"""
        return self.name

    def __str__(self):
        """returns a string which represents the object"""
        return self.email


import signals
```
#### Then in settins.py file configure AUTH_USER_MODEL
```
AUTH_USER_MODEL = 'accounts.UserProfile'
```
