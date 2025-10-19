# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repository Is

This is a **branded app customization repository** for OwnTube.tv's "Privacy Tube" brand. It contains:
- Brand-specific assets (icons, splash screens, banners) in `/assets`
- Configuration file (`.customizations`) with environment variables
- GitHub Actions workflow that triggers builds from the upstream repo

**This repo contains NO source code.** All application code lives in the upstream repository.

## Upstream Documentation

**For architecture, development, and technical details, see:**
- **[CLAUDE.md](https://github.com/OwnTube-tv/web-client/blob/main/CLAUDE.md)** - Complete OwnTube.tv architecture, development guide, and branded app system
- **[docs/customizations.md](https://github.com/OwnTube-tv/web-client/blob/main/docs/customizations.md)** - Full list of available customization options
- **[docs/pipeline.md](https://github.com/OwnTube-tv/web-client/blob/main/docs/pipeline.md)** - Detailed CI/CD setup and secrets configuration

This CLAUDE.md contains only brand-specific information for Privacy Tube.

## Privacy Tube Brand Configuration

**Current Settings:**
- **App Name:** Privacy Tube
- **Backend:** media.privacyinternational.org
- **Bundle ID (iOS):** com.owntubetv.pitube
- **Package (Android):** com.owntubetv.pitube
- **Theme Color:** #00E1FD (bright cyan)
- **Legal Entity:** OwnTube Nordic AB
- **PostHog Analytics:** Enabled (key in `.customizations`)

**Deployment URLs:**
- Web: https://cust-app-pitube.owntube.tv/
- TestFlight: https://testflight.apple.com/join/KAAJgPss
- Google Play: https://play.google.com/store/apps/details?id=com.owntubetv.pitube

## How to Customize

### Update Brand Assets

1. Add/modify image files in `/assets` directory
2. Reference them in `.customizations` using path: `../customizations/assets/filename.png`

**Asset Requirements:** See [docs/customizations.md](https://github.com/OwnTube-tv/web-client/blob/main/docs/customizations.md) for required sizes (app icons, splash screens, TV banners, etc.)

### Update Configuration

Edit `.customizations` file in repo root. All variables must have `EXPO_PUBLIC_` prefix.

**Key Variables:**
- `EXPO_PUBLIC_APP_NAME` - Display name
- `EXPO_PUBLIC_PRIMARY_BACKEND` - PeerTube instance hostname
- `EXPO_PUBLIC_IOS_BUNDLE_IDENTIFIER` / `EXPO_PUBLIC_ANDROID_PACKAGE` - App identifiers
- `EXPO_PUBLIC_ICON`, `EXPO_PUBLIC_SPLASH_IMAGE` - Branding assets
- `EXPO_PUBLIC_POSTHOG_API_KEY` - Analytics (or set to `null` to disable)

**See [docs/customizations.md](https://github.com/OwnTube-tv/web-client/blob/main/docs/customizations.md) for complete list of options.**

## How to Deploy

### Trigger Build

1. Go to **Actions** tab in GitHub
2. Select **"Build mobile artifacts & deploy static content to Pages for a branded app"** workflow
3. Click **"Run workflow"** and configure options:
   - `upload_ios_to_testflight` - Upload to TestFlight (true/false)
   - `upload_tvos_to_testflight` - Upload tvOS to TestFlight (true/false)
   - `google_play_track` - Google Play track (none/internal/alpha/beta/production)
   - `google_play_upload_tv` - Include Android TV in Google Play upload (true/false)

### What Gets Built

**Always built:**
- Web app → GitHub Pages
- Android APK → Artifact download
- Android TV APK → Artifact download
- iOS/tvOS Simulator builds → Artifact download

**Conditionally built (based on workflow inputs):**
- iOS/tvOS apps → TestFlight
- Android/Android TV → Google Play

### Required Secrets

All code signing secrets must be configured in repository Settings > Environments > `owntube`.

**See [docs/pipeline.md](https://github.com/OwnTube-tv/web-client/blob/main/docs/pipeline.md) for detailed instructions on:**
- Generating Apple certificates and provisioning profiles
- Creating Android keystores
- Setting up App Store Connect API keys
- Configuring Google Play service accounts

## Development Workflow

**This repository has no local development or testing.** All changes are configuration + assets:

1. Update assets in `/assets` OR edit `.customizations`
2. Commit changes
3. Trigger build via GitHub Actions workflow_dispatch
4. Test builds using:
   - **iOS/tvOS:** Apple TestFlight
   - **Android/Android TV:** Google Play Internal Test track
   - **Web:** GitHub Pages deployment

**Note:** There is no support for running/testing branded apps locally. All testing must be done through the CI/CD pipeline and distribution platforms.

### Developing Features Requiring Upstream Changes

To develop new features or experiment with customizations that require changes in the upstream OwnTube-tv/web-client project:

1. Fork [OwnTube-tv/web-client](https://github.com/OwnTube-tv/web-client) to your own GitHub account
2. Make code changes in your fork
3. Update this branded app repo's workflow to point to your fork:
   - Edit `.github/workflows/build_branded_main.yml`
   - Change `owntube_source: OwnTube-tv/web-client` to `owntube_source: your-username/web-client`
4. Trigger builds and test via TestFlight/Google Play Internal Test
5. Once tested, contribute changes back to upstream via Pull Request
6. After PR is merged, revert workflow to use `OwnTube-tv/web-client`

**For standard code changes:** Contribute directly to upstream [OwnTube-tv/web-client](https://github.com/OwnTube-tv/web-client) (see [CLAUDE.md](https://github.com/OwnTube-tv/web-client/blob/main/CLAUDE.md))

## Architecture Quick Reference

### Parent-Child Relationship

- **Parent (OwnTube-tv/web-client):** Source code + CI/CD workflows
- **Child (this repo):** Customizations only

**Build Flow:**
1. Child workflow reads `.customizations`
2. Triggers parent workflows with `use_parent_repo_customizations: true`
3. Parent workflows clone parent repo (not child)
4. Parent applies customizations and fetches assets from child repo

**See upstream [CLAUDE.md](https://github.com/OwnTube-tv/web-client/blob/main/CLAUDE.md) section "Branded App Architecture" for complete explanation.**

## Key Files

- `.customizations` - Environment variables for brand configuration
- `/assets` - Brand-specific images
- `.github/workflows/build_branded_main.yml` - Orchestrator that triggers parent workflows

## Notes

- Only one build can run at a time (concurrency group: "owntube-build")
- Asset paths use `../customizations/assets/` prefix when referenced in `.customizations`
- Remote assets can use full URLs (e.g., `EXPO_PUBLIC_FOOTER_LOGO`)
- Build info (git commit, timestamp) can be hidden with `EXPO_PUBLIC_HIDE_GIT_DETAILS=1`
