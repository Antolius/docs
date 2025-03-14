# Publishing Requirements

We have a few requirements and suggestions for publishing your app to AppCenter. For a quick intro on writing apps for elementary OS, check out our [Getting Started](../) guide. For more developer-oriented tips, see the [Tips series on our blog](https://blog.elementary.io/tags/#developer-tips).

## Hard Requirements

The following are **hard requirements for all apps submitted to AppCenter**. Both automated and human reviews will check these requirements before each app and app update is approved and released to users.

### Technical Requirements

Your app must be hosted in a [GitHub repository](https://docs.elementary.io/develop/writing-apps/hello-world#pushing-to-github). AppCenter Dashboard works by importing source code from a GitHub repository and building it in a clean environment. To ensure reproducible builds, transparency, and auditability, binaries cannot be uploaded or included alongside the source code to be installed on users' devices.

Your app may be written in any language, but the front-end must be a native Gtk3 app. Web, Electron, Qt, Java, and other non-native app front-ends will be rejected during the review process. A game may be excepted from this requirement so long as it uses native window decorations and is generally usable on both loDPI and HiDPI displays.

Your app must not attempt to modify, replace, or append software sources on the target system.

Your app must not attempt to modify other apps or system programs.

#### Packaging

Your app must come with [a Flatpak manifest](https://docs.elementary.io/develop/writing-apps/our-first-app/packaging). elementary OS uses Flatpak packages to manage software installation and updates. Your app cannot be downloaded without it.

#### Extensions & Plugins

AppCenter supports publishing apps that meet these requirements; extensions or plugins (eg. to the Panel, System Settings, or other apps) are not currently supported.

### Metadata Requirements

In general, your app's metadata should not refer to "elementary" or "elementary OS" in user-facing strings—it is assumed that all apps submitted to AppCenter are designed for elementary OS, and users don't need to be reminded of this. If there is a rare, legitimate reason for mentioning elementary, it must abide by the [elementary Brand Guidelines](https://elementary.io/brand).

#### MetaInfo and OARS

Your app must install an [metainfo.xml file](../writing-apps/our-first-app/metadata.md#metainfo) to `/usr/share/metainfo`. AppCenter uses this metadata to create a listing for your app. It cannot be displayed in AppCenter without it.

Your metainfo.xml file must contain a `screenshot` tag that references a screenshot of your app with elementary OS default settings including the GTK stylesheet, icons, window button position, etc. Screenshots referenced in your MetaInfo should not contain marketing copy, illustrations, or other elements aside from a full-window screenshot of your app in use.

Your metainfo.xml file must contain a `developer_name` tag that references your name or the name of your organization.

Your metainfo.xml must include accurate [Open Age Rating Service (OARS)](https://hughsie.github.io/oars/) data. OARS uses a short, self-reported survey that only takes a few moments to output the required XML. Reviewers will check this data for accuracy in order for your app to be published.

For more information about the metainfo.xml format see, see the [appstream specification](https://www.freedesktop.org/software/appstream/docs/chap-Quickstart.html#sect-Quickstart-DesktopApps).

#### Desktop File

Your app must install [a .desktop file](../writing-apps/our-first-app/metadata.md#desktop-entry) to `/usr/share/applications`. elementary OS uses a .desktop file to display your app in the applications launcher and the dock. Without this file, your app will not be visible to users.

Your .desktop file must not contain `NoDisplay=true` or anything else that prevents it from showing up in the applications launcher.

#### Icons

Your app must install icons to `/usr/share/icons/hicolor` in 32px, 48px, 64px, and 128px. These are the icon sizes that will be displayed in the Applications menu's search, grid, and category views, Multitasking View, the dock, and in AppCenter.

### Legal Requirements

You must have permission to redistribute any software you attempt to publish through AppCenter. If you are not the copyright holder or the source code is not openly licensed, you likely do not have permission to redistribute the software.

You must have permission to use any trademarks in your software or its metadata. You may not publish your app using trademarks reserved by others.

Your app must comply with all applicable laws as well as the terms of any services your app utilizes.

### Other Publishing Requirements

#### Naming

To protect both users and developers, your app's name must not be the same as or confusingly similar to an existing app in AppCenter or another brand, as determined by app reviewers.

Your app should not be named generically like "Web Browser" or "File Manager".

Your app should not use "elementary", "Pantheon", or other elementary brand names in its naming scheme. It should also not be formatted with a leading lowercase "e", such as "eApp".

#### Launching

Your app should display its own graphical user interface on launch; it should not open another app or system component without user interaction inside your app UI. For example, if your app operates on a given file, it should display its own UI with an "Open File" button (or similar) before throwing an Open File dialog. If your app can request elevated permissions for certain actions, those permissions should be requested after your app's UI is shown and preferably only on-demand when actions requiring those permissions are performed.

#### App Stores

Your app cannot be an "app store," as ultimately determined by app reviewers. This includes but is not limited to apps that look and function confusingly similarly to AppCenter, provide software from other sources, link to an online app store, and/or facilitate payments for apps in the system repositories.

#### Duplicate Apps

Each app submission from a developer should be genuine and unique as determined by app reviewers. Submissions that are overly similar to existing apps from the same developer or are a a fork of an existing app with little to no changes may be rejected.

## Suggestions

For the best experience, we strongly suggest the following before you publish your app:

### Use a GitHub Organization

Once your app is submitted **you cannot change the GitHub account** that it is linked to. We recommend you use a GitHub organization as the owner of the repository so it can be transferred in the future if you so choose. This also makes it easier to manage community contributions.

Note that anyone with access to the GitHub organization will be able to manage releases and monetization.

### Repository and App ID

While AppCenter Dashboard supports repositories with dashes and underscores, it vastly simplifies things to omit them from your GitHub repository name and subsequently your app ID. Some components in the desktop require workarounds for ID matching with dashes and underscores, so it is typically simpler to stick to all lowercase with no dashes or underscores.

### Human Interface Guidelines

Apps should generally abide by the [elementary Human Interface Guidelines](https://docs.elementary.io/hig/), especially with regards to [Desktop Integration](https://docs.elementary.io/hig/desktop-integration). Guidelines around [Notifications](https://docs.elementary.io/hig/widgets/providing-feedback#notifications) may be strictly enforced, as it is important that apps behave as expected by users.

### Tips for Games

If your game UI properly scales when the window is resized, one way to support both HiDPI and loDPI (even if the engine doesn't out of the box) is to launch your game maximized. That way the UI will scale up no matter the resolution or scaling factor of the display.
