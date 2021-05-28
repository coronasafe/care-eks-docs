# Production Environment Variables

This section covers the environment and its required setup for running the care project in production. This involves setting up the secret keys, encryption keys, PostGIS database URLs etc. The project also employs other services such as Redis for caching and Sentry for logging.

The following list contains variables you will need during the production environment.

| Variable Key | Required | Description |
| :--- | :--- | :--- |
| `POSTGIS_URL` | **Yes** | This variable is the URL to your Postgres database with the PostGIS extension. To obtain this, simply replace `postgres://` with `postgis://` in your `DATABASE_URL` |
| `DJANGO_ADMIN_URL` | **Yes** | This variable shall be used to access your Django admin dashboard. For security purposes, it is a good idea to keep it as a short random string. |
| `DJANGO_SECRET_KEY` | **Yes** | A secret key used by Django for generating session cookies and other purposes. An online search will provide several methods for generating it. |
| `FERNET_SECRET_KEY` | **Yes** | A secret key used for encrypting patient records in the database. This can be generated in the same way as the Django secret key. A change in the fernet key will cause all data to be corrupted, please make sure this variable is always handled with care. The development version has a hardcoded fernet key to avoid issues. |
| `DJANGO_SETTINGS_MODULE` | **Yes** | This variable specifies which settings to use in the production environment. Set the value to `config.settings.production` to point it to the production settings file in the project. development builds can use `config.settings.staging` defaults to local settings |
| `USE_S3` | No | Set this variable to `True` if you want to use Amazon S3 buckets for storing your static files in production. Defaults to 'False'. The backend copies the static files on start, the Gunicorn server serving the backend does not perform well with static files so it is advised to configure S3 as a static file server. |
| `AWS_STORAGE_BUCKET_NAME` | No | This variable is used to store the bucket name to store your static files during the collectstatic step. Note that this is used only if `USE_S3` is set to `True`. |
| `AWS_ACCESS_KEY_ID` | No | The AWS Access Key of your account used to access your S3 bucket. Note that this is used only when `USE_S3` is set to `True`. |
| `AWS_SECRET_ACCESS_KEY` | No | The AWS Secret Key of your account used to access your S3 bucket. Note that this is used only when `USE_S3` is set to `True`. |
| `REDIS_URL` | **Yes** | The URL to your Redis instance for use in caching. Redis is also used as the background job management |
| `CELERY_BROKER_URL` | **Yes** | The URL to your Redis instance for use in celery worker management. |
| `SENTRY_DSN` | **Yes** | The Sentry DSN value for logging errors from your app. To get a free DSN, sign up at [https://sentry.io](https://sentry.io). |
| `GOOGLE_RECAPTCHA_SITE_KEY` | No | The configured site key for your recaptcha. Recaptcha is used to prevent brute-force attacks while logging into care. |
| `GOOGLE_RECAPTCHA_SECRET_KEY` | No | The secret key for your recaptcha. |
| `DJANGO_ALLOWED_HOSTS` | **Yes** | This is used to store a JSON type array of hosts you want to allow access to your backend API. Requests with other Host fields will not be able to complete successfully. Set it to `['*']` to allow all hosts. Defaults to `['*']`. |
| `CSRF_TRUSTED_ORIGINS` | **Yes** | Contains a JSON array of hosts that are allowed to make cross site requests to the backend API. Defaults to `[]`. |
| `DJANGO_SECURE_SSL_REDIRECT` | No | Use this option to set whether or not you want to redirect from HTTP to HTTPS automatically. Defaults to `True`. |
| `RATE_LIMIT` | No | A string value of the form requests/time to be set for rate limiting. For eg., if you want to allow not more than 5 requests from a user in 10 mins, provide `5/10m` as the value. Defaults to `5/10m`. Ratelimiting is only enforced for the login and signup endpoint to prevent brute-forcing, after the limit every request required a captcha to be present. |
| `MAINTENANCE_MODE` | No | Set this variable to 1 to put the site/API into maintenance. Defaults to 0. |
| `POSTGRES_DB` | **Yes** | Your PostGIS DB name. This is used to check if the postgres db is connected before performing db migrations |
| `POSTGRES_HOST` | **Yes** | Your Postgres host address. |
| `POSTGRES_USER` | **Yes** | Your Postgres username. |
| `POSTGRES_PASSWORD` | **Yes** | Your `POSTGRES_USER` password. |
| `POSTGRES_PORT` | **Yes** | Your Postgres instance port number. |
| `SNS_ACCESS_KEY` | **Yes** | AWS SNS access key for sending SMS messages |
| `SNS_SECRET_KEY` | **Yes** | AWS SNS Secret key for sending SMS messages |
| `VAPID_PUBLIC_KEY` | **Yes** | Vapid Public key for sending Web push notifications, Defaults to publicly visible certificates |
| `VAPID_PRIVATE_KEY` | **Yes** | Vapid Private key for sending Web push notifications, Defaults to publicly visible certificates |
| `FILE_UPLOAD_BUCKET` | **Yes** | AWS S3 bucket name with no public access to store confidential patient files  |
| `FILE_UPLOAD_KEY` | **Yes** | AWS Access key to access the File Upload Bucket |
| `FILE_UPLOAD_SECRET` | **Yes** | AWS Secret key to access the File Upload Bucket |
| `EMAIL_HOST` | **Yes** | SMTP Email Host |
| `EMAIL_USER` | **Yes** | SMTP Email User |
| `EMAIL_PASSWORD` | **Yes** | SMTP Email Password |

