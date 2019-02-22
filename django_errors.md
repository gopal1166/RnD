#### django.core.exceptions.FieldDoesNotExist: MyUser has no field named 'username'
```
ACCOUNT_USER_MODEL_USERNAME_FIELD = None
ACCOUNT_EMAIL_REQUIRED = True
ACCOUNT_USERNAME_REQUIRED = False
ACCOUNT_AUTHENTICATION_METHOD = 'email'
```
#### django.db.utils.IntegrityError: insert or update on table "authtoken_token" violates foreign key constraint "authtoken_token_user_id_35299eff_fk_auth_user_id"
#### DETAIL:  Key (user_id)=(5) is not present in table "auth_user".
```
Do not make migrations wiht default auth_user
Try to make the migrations with custome user model as AUTH_USER_MODEL setting
we can try by creating new database and migrating to that.

We'll face this error in the below case:
  both default and customer user auth table migrated to database
    ex:
      accounts_customer_user
      auth_user
      
We should migrate to db either of these tables
```

#### Connection Refuser after testing registration api of django-rest-auth
```
solved by placing EMAIL_BACKEND setting

EMAIL_USE_TLS = True
# SERVER_EMAIL = 'pgopal1166@gmail.com'
EMAIL_HOST = 'smtp.gmail.com'
EMAIL_PORT = 587
EMAIL_HOST_USER = 'vgopal1166@gmail.com'
EMAIL_HOST_PASSWORD = 'Vgopal@1166'
DEFAULT_FROM_EMAIL = EMAIL_HOST_USER
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
```
