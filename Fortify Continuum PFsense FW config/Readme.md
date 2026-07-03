# Fortify Continuum Captive Portal

This folder contains the custom Fortify Continuum captive portal pages used for staff access. The pages are designed with a branded office background, translucent glass-style form panels, and responsive layouts for desktop and mobile.

## Files

- `login.html` — Login page for staff access.
- `error.html` — Error page showing login or voucher failures.
- `logout.html` — Logout/connected status page.
- `images/` — Local image assets used by the portal pages.
- `Readme.md` — This file.

## Features

- Background uses `images/FC-office-img.jpg` for a branded look.
- Transparent translucent form panel with blur effect.
- Responsive layout: pages stack for smaller screens and show side-by-side content on desktop.
- Consistent branding across login, error, and logout flows.

## Notes

- The pages currently use inline CSS inside each HTML file.
- The current file are required for each captive portal zone.
- The `login.html` form posts to the captive portal authentication endpoint.
- The `logout.html` page includes logout behavior and a reconnect flow.

## Customization

To adapt the portal for another zone or design:

1. Update the background image in `background-image: url('images/FC-office-img.jpg')`.
2. Change the brand logo path and text inside each HTML file.
3. Adjust the form action URL in `login.html` and the redirect logic in `logout.html`.
4. Update colors, spacing, or fonts in the inline `<style>` sections.

## Uploading to pfSense Captive Portal

1. Prepare the HTML and image assets locally.
2. Make sure all image references are relative paths, for example:
   - `images/FC-office-img.jpg`
   - `images/logo for FC.png`
3. Copy the image folder to pfSense. Use SCP, SFTP, or the pfSense shell to create and populate `/usr/local/captiveportal/images/`.
4. In the pfSense web GUI, go to `Services > Captive Portal`.
5. Select the captive portal zone you want to customize.
6. Under the portal page settings, paste the contents of `login.html` into the `Portal page contents` field or use the file upload button if available.
7. For custom error or logout pages, upload or paste `error.html` and `logout.html` into the corresponding page content fields.
8. Save changes and test the captive portal from a client device.

### Notes

- If pfSense does not allow direct image upload in the portal settings, uploading the image files to `/usr/local/captiveportal/images/` is the standard method.
- Use relative paths in the HTML so the pages load correctly from the captive portal directory.
- If you prefer a single file deploy, consider converting small images to base64 data URIs inside the HTML.
