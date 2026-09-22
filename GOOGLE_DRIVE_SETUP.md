# Google Drive backup setup

The Android app already has the only Android permission it needs: `INTERNET`.
Do **not** add storage, media, or "manage all files" permissions for this
feature. Drive access is granted by the signed-in Google account through OAuth.

## One-time Google Cloud configuration

1. Open Google Cloud Console and create or select a project.
2. In **APIs & Services → Library**, enable **Google Drive API**.
3. In **APIs & Services → OAuth consent screen**, configure the app. Add the
   Google accounts under **Test users** while the app is in testing.
4. In **Credentials**, create an **OAuth client ID → Android**.
5. Enter this project's Android package name: `com.example.india_weather_app`.
   Before publishing, change this to a package name you own and use that exact
   name here as well.
6. Add the SHA-1 certificate fingerprint for every signing key used to run the
   app. For the usual debug build, run `./gradlew signingReport` from the
   `android` folder and copy the SHA-1 shown for `debug`.
7. Reinstall the app after changing the OAuth client or signing key.

The backup uses the `drive.appdata` scope. Google stores the encrypted backup in
the app's private **Application Data** folder; it is not shown in the user's
normal My Drive files. The user approves this when Google sign-in opens.

## Fix for `Error 403: access_denied`

The message "Access blocked: [app] has not completed the Google verification
process" means the signed-in account is not a permitted tester. In the current
Google Cloud interface, open **Google Auth Platform → Audience**, click
**Add users**, add the same Gmail account used on the phone, save, wait a few
minutes, and try the backup again. This is required while the app is in
**Testing**; it is not an Android permission problem.

## If Google sign-in still fails

- **`ApiException: 10` / `DEVELOPER_ERROR`**: package name or SHA-1 does not
  exactly match the Android OAuth client.
- **`403 accessNotConfigured`**: enable Google Drive API in the same Cloud
  project that owns the OAuth client.
- **`403 appNotAuthorizedToFile`**: use the app-data folder as this project
  does; do not try to access ordinary My Drive files with this scope.
- **Access blocked / test-user error**: add the account to the OAuth consent
  screen's Test users, or publish the consent screen when ready.
