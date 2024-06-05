# Integrating Google OAuth into Django Application

## Step-by-Step Guide

### 1. Setup Google OAuth Credentials

1. **Create a Project in Google Developer Console:**

   - Go to [Google Developer Console](https://console.developers.google.com/).
   - Create a new project and select it.

2. **Configure OAuth Consent Screen:**

   - Search for "OAuth consent screen" and select it.
   - Select "External" user type.
   - Fill in the app name, upload a logo (optional), and provide your email.

3. **Add Scopes:**

   - On the second window, select scopes like email and profile information.

4. **Create OAuth Credentials:**
   - Go to the "Credentials" tab.
   - Click "Create Credentials" and select "OAuth Client ID".
   - Provide a name, set `http://127.0.0.1:8000` in authorized JavaScript origins.
   - Set `http://localhost:8000/accountsgoogle/login/callback/` in authorized redirect URIs.
   - Download the `client_id` and `client_secret` in JSON format.

### 2. Setup Django Project

1. **Create a New Django Project:**

   ```bash
   django-admin startproject myproject
   cd myproject
   ```

2. **Install `django-allauth`:**

   ```bash
   pip install "django-allauth[socialaccount]"
   ```

3. **Configure `django-allauth`:**

   - Follow the [django-allauth quickstart guide](https://docs.allauth.org/en/latest/installation/quickstart.html) to update your settings.
   - Ensure `SOCIALACCOUNT_PROVIDERS` includes Google configuration.

4. **Create Users App:**

   ```bash
   python manage.py startapp users
   ```

   - Add `users` to `INSTALLED_APPS` in `settings.py`.

5. **Update URL Configurations:**

   - In `myproject/urls.py`, include URLs for `users` and `allauth`.

6. **Setup Views and Templates:**

   - Create `views.py` and `urls.py` in your `users` app.
   - In the `templates` folder, create `index.html` and add a Google login link.
   - Configure template directory in `settings.py`.

7. **Migrate Database and Create Superuser:**
   ```bash
   python manage.py migrate
   python manage.py createsuperuser
   ```

### 3. Configure Django Admin

1. **Add a Site:**

   - Start the server and go to `http://127.0.0.1:8000/admin`.
   - Add a new site with the domain `127.0.0.1:8000` and a display name.

2. **Add Social Application:**
   - Go to "Social applications" and create a new application.
   - Select provider as Google, name it Google.
   - Enter the `clientId` and `clientSecret` from Google.
   - Select the site `127.0.0.1:8000` and save.

### 4. Testing and Finalizing

- Log out of the admin and navigate to the homepage.
- Click the Google login link and complete the authentication process.
- If any error occurs, note the valid redirect URL and update it in the Google Developer Console credentials.

### 5. Login with Google

- After successfully redirecting, select an account to log in.

## Summary

Following these instructions, you can integrate Google OAuth authentication into your Django application. Ensure all configurations are correctly set in both Google Developer Console and Django admin.

For more detailed settings, refer to the [django-allauth documentation](https://docs.allauth.org/en/latest/installation/quickstart.html).
