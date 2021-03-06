# Ironboard Greenifier

Ironboard Greenifier is a simple userscript for Flatiron School students who are irrationally annoyed that not all of their completed labs turn green on Ironboard. Or rationally annoyed because it makes it harder to tell what they have or haven't finished.

You supply a list of the labs that should rightly be green but aren't. Greenifier makes them green. It also changes the icon in the "Complete?" column from a no symbol to a check mark, and corrects the completed lab count.

Greenifier works on the Your Progress page only.

## Installation

To use Ironboard Greenifier, you'll need [Tampermonkey for Chrome](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=en) or [Greasemonkey for Firefox](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/).

Once you have one of those installed, click on the ironboard-greenifier.user.js file, and then click "Raw" to open the file directly. You should see an install page or dialog; follow its instructions to install the script.

## Setup

Greenifier won't work until you've set it up with your information. I'm too lazy to write a version with, like, an actual interface, so you'll have to do this by editing the script itself.

To edit the script:

- In Firefox, go to `Tools > Greasemonkey > Manage User Scripts...`. Choose Ironboard Greenifier, and click "Edit this user script." It will open in a text editor; when you're done editing, just save the file.
- In Chrome, click the Tampermonkey icon, and then click "Dashboard." In the new tab that opens, click on Ironboard Greenifier. When you're done editing, click the disk icon to save.

### What to edit

#### Required: Adding your broken lab list

You need to provide Greenifier with a list of the labs that are broken for you and should be green. Around line 30, you should see this:

    // List the exact names of your broken userscripts here
    var brokenLabs = [];

Just fill that array with the names of the labs in question, as strings of course. These need to be the EXACT lab names as listed on the Your Progress page in the first column. Case-sensitive.

Every time a new lab fails to turn green when you've completed it, you'll need to edit the script and add it to the array. (Yep, annoying, but if it were more annoying than the lab not being green, would you be reading this?)

#### Optional: Adjusting the completed lab count

Greenifier updates the completed lab count around line 60:

    // Adjust your completed lab count here
    var newCount = parseInt(completed) + brokenLabs.length + " / " + total;

By default, it adds the number of broken labs to the original completed lab count.

This is accurate-ish, but for me it results in the completed lab count being too high by 1, because I guess one of my broken labs is still registering as completed for purposes of the total. So in my version of the script, I subtract 1 from `brokenLabs.length` on that line. If you notice that your new completed lab count is inaccurate, just adjust this line as necessary to make it right.

#### Note for iOS

I don't know the url of the Your Progress page for iOS. You'll have change the URL in the `@match` on line 7. Or add it on a second `@match` line and open a pull request. Or let me know what it is and I'll add it. Whatever.

## That's it

Save your edits, refresh the Your Progress page and enjoy your appropriately green labs!