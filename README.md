pwsafejs
---
Browser-based viewer for Password Safe v3 files (http://passwordsafe.sourceforge.net/)

*NOTE:* This is alpha quality and hasn't been checked much for security yet, nor am I any sort of expert on security.  The password file is sent as-is (that is, an encrypted binary file) from the server to your browser, where it is decrypted by this application using the passphrase you supply.  Nobody should be able to see your passwords by sniffing the network, and your decrypted data (hopefully) won't be cached by the browser/OS, but I don't think I can forensically scrub secrets, and I could be missing something obvious... use at your own risk.

Intro and use
---
This is a Javascript reader for Password Safe V3 files.  To use it, place your Password Safe DB in the directory and name it pass.psafe3.  You can test on your hard drive (with the --allow-file-access-from-files command line argument for Chrome, or something similar for other browsers) or online.

You can see a [live demo here](http://scintill.net/pwsafejs) (password is "pass").

The interface is really clunky right now, with a pretty plain list of your accounts.  Click an account to see the username and password.  I want to make a pretty, more full-featured, and secure UI, but I also just wanted to get this out in case I never get around to that.

Compatibility
---
I've tested that it works in Google Chrome and Mozilla Firefox on Linux and Windows, Internet Explorer 8 (Windows 7), the Browser in Android 2.3 on my Nexus One, and Safari in iOS 4.2.1.

It's optimized for web worker-capable browsers but uses several setTimeout() calls when Workers aren't available.  Decryption can take 10-15 seconds on slow platforms such as my Nexus One and old iPod.

Known issues
---
- Ignores grouping of accounts
- Does not show all fields associated with your accounts -- should be pretty easy to add if you want though
- As mentioned, probably not very secure. Since my use case is logging into an account from a foreign computer I trust at least enough that I'm willing to potentially compromise that particular account, I'm interested in finding a way to not "put all my eggs in one basket." So far I can't think of a clever way to give myself access to arbitrary sets of account info without giving attakers the keys to ALL account info. Putting sensitive accounts into a separate database that you protect more carefully is probably a good idea though.

Credits
---
See libpwsafejs/COPYING.md.

Note on strange revision history
---
I rewrote the repository into two repos so that the PWSafe database logic would be more reusable, trying to preserve history _and_ not waste space (probably a bad idea.)  So, if you want to execute old revisions, you'll have to also check out a contemporaneous revision from the new [libpwsafejs](http://github.com/scintill/libpwsafejs).
