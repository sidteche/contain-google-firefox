# Google Container

**Prevent Google from tracking your visits to other websites**

This is a fork of [Facebook Container](https://github.com/mozilla/contain-facebook)

Google Container is an add-on you can install on Firefox to prevent Google from tracking your activity on other websites, so you can continue to use Google while protecting your privacy.

**Note:** To learn more about Containers in general, see [Firefox Multi-Account Containers](https://support.mozilla.org/kb/containers).

## How does Google Container work?

The Add-on keeps Google in a separate Container to prevent it from following your activity on other websites. When you first install the add-on, it signs you out of Google and deletes the cookies that Google uses to track you on other websites. 

Every time you visit Google, it will open in its own container, separate from other websites you visit.  You can login to Google within its container.  When browsing outside the container, Google won’t be able to easily collect your browsing data and connect it to your Google identity.

## How do I install Google Container?

This version is installed from a file instead of from the Firefox Add-ons website. If you have the Google Container add-on from the Add-ons website, disable or remove it first, since both use the same add-on ID.

### 1. Build the add-on file

Download this repository (**Code** > **Download ZIP**) and extract it, or clone it. Then pack the add-on files into `google-container.xpi`. The files must be at the top level of the archive, not inside a folder.

On Windows (PowerShell), from the repository folder:

```powershell
Compress-Archive -Path manifest.json, background.js, options.html, options.js, icon.png, icon@2x.png -DestinationPath google-container.zip -Force
Move-Item google-container.zip google-container.xpi -Force
```

On macOS or Linux, from the repository folder:

```bash
zip google-container.xpi manifest.json background.js options.html options.js icon.png icon@2x.png
```

### 2. Install it in Firefox

Regular Firefox only installs add-ons that Mozilla has signed, so pick one of these:

**Try it out (any Firefox, removed when Firefox restarts)**

1. Open `about:debugging#/runtime/this-firefox`.
2. Click **Load Temporary Add-on…** and select `manifest.json` (or `google-container.xpi`).

**Keep it installed (Firefox Developer Edition, Nightly or ESR)**

1. Open `about:config`, accept the warning, and set `xpinstall.signatures.required` to `false`.
2. Open `about:addons`, click the gear icon, and choose **Install Add-on From File…**.
3. Select `google-container.xpi` and click **Add**.

**Keep it installed (regular Firefox)**

1. Get the file signed by Mozilla without publishing it: on the Firefox Add-on Developer Hub, submit a new add-on, choose **On your own** and upload `google-container.xpi`. Before uploading, change `id` in `manifest.json` to your own, for example `google-container@yourname`, since `@contain-google` belongs to the original add-on.
2. Download the signed `.xpi` once it's approved (usually within minutes).
3. Open `about:addons`, click the gear icon, choose **Install Add-on From File…** and select the signed file.

## How do I use Google Container?

1. After installing, the add-on logs you out of Google in your normal tabs and deletes the cookies Google uses to track you.
2. Open Google and use it like you normally would. Firefox will automatically switch to the Google Container tab for you.
3. If you click on a link to a page outside of Google or type in another website in the address bar, Firefox will load them outside of the Google Container.
4. To change settings, open `about:addons`, click **Google Container** and go to **Preferences**.

## How does this affect Google’s features?

Google Containers prevents Google from linking your activity on other websites to your Google identity. Therefore, the following will not work:

### “Like” buttons and embedded Google comments on other websites.

Because you are logged into Google only in the Container, “Like” buttons and embedded Google comments on other websites will not work.

### Logging in or creating accounts on other websites using Google

Websites that allow you to create an account or log in using Google will generally not work properly. There are two ways to make it work:

- Turn on **Allow "Sign in with Google" on other sites** in the add-on preferences. The Google sign-in page then stays in the same tab (or popup) and container as the website that opened it, so the website receives the login. You sign in to Google there separately, and those Google cookies are cleared on the next browser start.
- Add the website to **Include additional urls in Google Container**, so the website itself opens in the Google Container.

Sign-in results that are sent back to the website with a form POST are never reopened in another container, since that would drop the login.

### Troubleshooting

Open `about:debugging#/runtime/this-firefox`, click **Inspect** next to Google Container and go to **Console**. With the **Debug** filter on, every time the add-on reopens a page in another container, or decides not to, it logs the page (without its query string) and the reason.

## Will this protect me from Google completely?

This add-on does not prevent Google from mishandling the data it already has or permitted others to obtain about you. Google still will have access to everything that you do while you are on google.com or on any Google app, including your Google comments, photo uploads, likes, and any data you share with Google connected apps, etc.  

Other ad networks may try to link your Google activities with your regular browsing. In addition to this add-on, there are other things you can do to maximize your protection, including changing your Google settings, using Private Browsing and Tracking Protection, blocking third-party cookies, and/or using [Firefox Multi-Account Containers](https://addons.mozilla.org/firefox/addon/multi-account-containers/ ) extension to further limit tracking.

## How do I use Containers for other websites?

Good news! Containers aren’t just for Google. You can use Containers to prevent websites from linking your identities across the Web by installing [Firefox Multi-Account Containers](https://addons.mozilla.org/firefox/addon/multi-account-containers/).

To learn more about how Mult-Account Containers work, see our support page at [Firefox Multi-Account Containers](https://addons.mozilla.org/firefox/addon/multi-account-containers/).
