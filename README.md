# OwnTube.tv "Privacy Tube" Branded App

Customized Android, AndroidTV, iOS, and tvOS builds for Privacy Tube brand of OwnTube-tv/web-client.

Web version available at: https://cust-app-pitube.owntube.tv/

App beta versions:

<a href="https://testflight.apple.com/join/KAAJgPss">
  <img height=75 alt="Get the beta on TestFlight" src="https://askyourself.app/assets/testflight.png"/>
</a>
<br/>
<a href="https://play.google.com/store/apps/details?id=com.owntubetv.pitube">
  <img height=75 alt="Get the beta on Google Play" src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/78/Google_Play_Store_badge_EN.svg/1280px-Google_Play_Store_badge_EN.svg.png"/>
</a>

## How to Use

Follow the steps below to customize and deploy your branded OwnTube instance.

### 1. Create a `.customizations` File

In the root of the repository, create a `.customizations` file. This file will contain your app-specific customizations. Use it to define the following variables:

### 2. Restrict the App to a Primary Backend

Add the following line to your `.customizations` file:
```bash
EXPO_PUBLIC_PRIMARY_BACKEND=<your_instance_hostname>
```
This restricts the app to the specified hostname and disables instance selection in the web app. Note that users can still bypass this restriction by entering a different hostname in the URL parameters.

### 3. Configure App Customizations

#### All Platforms
Define the following variables for all platforms:

- **App Name:**
  ```bash
  EXPO_PUBLIC_APP_NAME=<your_app_name>
  ```
  The name of the app displayed throughout.

- **App Slug:**
  ```bash
  EXPO_PUBLIC_APP_SLUG=<your_app_slug>
  ```
  A unique identifier for your app.

- **App Icon:**
  ```bash
  EXPO_PUBLIC_ICON=<your_icon_url>
  ```
  The global icon used in the app. Size: arbitrary but it looks best if 512x512 is reused here.

#### Web Platform
Define the following variables for the web platform:

- **Favicon:**
  ```bash
  EXPO_PUBLIC_FAVICON_URL=<your_favicon_url>
  ```
  The URL of the favicon for your site. Size: 32x32.

- **Base URL:**
  ```bash
  EXPO_PUBLIC_BASE_URL=<your_repo_name>
  ```
  The base URL used by Expo when deploying to GitHub Pages or similar services.

#### Mobile Platform
Define the following variables for the mobile platform:

- **Splash Screen Background Color:**
  ```bash
  EXPO_PUBLIC_SPLASH_BG_COLOR=<your_splash_bg_color>
  ```
  The background color for the splash screen.

- **Splash Screen Image:**
  ```bash
  EXPO_PUBLIC_SPLASH_IMAGE=<your_splash_image_path>
  ```
  The splash screen image file. Size: 1152x1152, transparent background.

- **Android TV:**
  ```bash
  EXPO_PUBLIC_ANDROID_TV_BANNER=<your_android_tv_banner_path>
  ```
  The Android TV banner image file. Size: 320x180.

- **Apple TV Icons:**
  ```bash
  EXPO_PUBLIC_APPLE_TV_ICON=<your_apple_tv_icon_path>
  EXPO_PUBLIC_APPLE_TV_ICON_SMALL=<your_apple_tv_icon_small_path>
  EXPO_PUBLIC_APPLE_TV_ICON_SMALL_2X=<your_apple_tv_icon_small_2x_path>
  EXPO_PUBLIC_APPLE_TV_TOP_SHELF=<your_apple_tv_top_shelf_path>
  EXPO_PUBLIC_APPLE_TV_TOP_SHELF_2X=<your_apple_tv_top_shelf_2x_path>
  EXPO_PUBLIC_APPLE_TV_TOP_SHELF_WIDE=<your_apple_tv_top_shelf_wide_path>
  EXPO_PUBLIC_APPLE_TV_TOP_SHELF_WIDE_2X=<your_apple_tv_top_shelf_wide_2x_path>
  ```
  Apple TV-specific icons and top-shelf images. Sizes:
  -  icon: 1280x768
  -  iconSmall: 400x240
  -  iconSmall2x: 800x480
  -  topShelf: 1920x720
  -  topShelf2x: 3840x1440
  -  topShelfWide: 2320x720
  -  topShelfWide2x: 4640x1440

---

#### Example `.customizations` File

Here is an example `.customizations` file for reference:

```bash
EXPO_PUBLIC_APP_NAME='<Your app name>'
EXPO_PUBLIC_APP_SLUG=<your.app.package.slug>
EXPO_PUBLIC_IOS_BUNDLE_IDENTIFIER=<com.yourcompany.app>
EXPO_PUBLIC_ANDROID_PACKAGE=<com.yourcompany.app>
EXPO_PUBLIC_PRIMARY_BACKEND=<your_instance_hostname>
EXPO_PUBLIC_FAVICON_URL=<your_favicon_path>
EXPO_PUBLIC_SPLASH_BG_COLOR='<your_splash_bg_color>'
EXPO_PUBLIC_SPLASH_IMAGE=<your_splash_image_path>
EXPO_PUBLIC_ICON=<your_app_icon_path>
EXPO_PUBLIC_APPLE_TV_ICON=<your_apple_tv_icon_path>
EXPO_PUBLIC_APPLE_TV_ICON_SMALL=<your_apple_tv_icon_small_path>
EXPO_PUBLIC_APPLE_TV_ICON_SMALL_2X=<your_apple_tv_icon_small_2x_path>
EXPO_PUBLIC_APPLE_TV_TOP_SHELF=<your_apple_tv_top_shelf_path>
EXPO_PUBLIC_APPLE_TV_TOP_SHELF_2X=<your_apple_tv_top_shelf_2x_path>
EXPO_PUBLIC_APPLE_TV_TOP_SHELF_WIDE=<your_apple_tv_top_shelf_wide_path>
EXPO_PUBLIC_APPLE_TV_TOP_SHELF_WIDE_2X=<your_apple_tv_top_shelf_wide_2x_path>
EXPO_PUBLIC_ANDROID_TV_BANNER=<your_android_tv_banner_path>
EXPO_PUBLIC_ICON_192=<your_public_icon_for_pwa_path>
EXPO_PUBLIC_ICON_512=<your_public_icon_for_pwa_path>
EXPO_PUBLIC_HIDE_VIDEO_SITE_LINKS=<1_to_enable_or_omit_for_default>
EXPO_PUBLIC_HIDE_GIT_DETAILS=<1_to_enable_or_omit_for_default>
EXPO_PUBLIC_LANGUAGE_OVERRIDE=<language_code>
EXPO_PUBLIC_FOOTER_LOGO=<your_footer_logo_path>
EXPO_PUBLIC_CUSTOM_DEPLOYMENT_URL=<your_custom_deployment_hostname>
EXPO_PUBLIC_PROVIDER_LEGAL_ENTITY="Your Company Ltd"
EXPO_PUBLIC_PROVIDER_LEGAL_EMAIL=legal@yourcompany.com
EXPO_PUBLIC_PROVIDER_CONTACT_EMAIL=info@yourcompany.com
EXPO_APP_THEME_COLOR='<theme_color_for_pwa>'
EXPO_APP_BG_COLOR='<background_color_for_pwa>'
EXPO_APP_DESCRIPTION='<App description for PWA>'
```

---

### 4. Set Up Environment Variables

TODO: Mike, please add docs on how to proceed with the next step here.


## Notes

- **Image and Custom File Paths:**
  If you want to include custom images or other files directly in this repository, place them in a `/assets` folder. When referencing these files in the `.customizations` file, use paths starting with `../customizations/`. This is the path structure that the build process expects.

  For example:
  ```bash
  EXPO_PUBLIC_SPLASH_IMAGE=../customizations/assets/splashScreen.png
  EXPO_PUBLIC_ICON=../customizations/assets/icon.png
  ```
- **Code Signing for Apple & TestFlight:**
  Setting up code signing and TestFlight for Apple devices requires additional configuration. Refer to the [OwnTube Documentation](https://github.com/OwnTube-tv/web-client/blob/main/docs/pipeline.md) for detailed instructions on configuring code signing and deploying your app to TestFlight.
- **Code Signing for Android & Google Play:**
  Refer to the [OwnTube Documentation](https://github.com/OwnTube-tv/web-client/blob/main/docs/pipeline.md) for detailed instructions on how to configure delivery to Google Play.
- Ensure all referenced files (e.g., icons and splash images) exist in the specified paths.
- Double-check the configurations before deploying to avoid runtime errors.

