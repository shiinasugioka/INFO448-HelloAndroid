# UW Homework: Hello Android
This homework is designed to force you to ensure that the tools are correctly installed on your machine, and that you can:

* run Android Studio
* create a project
* build that project
* deploy it to an emulator
* run the app on the emulator
* deploy it to a physical device
* run the app on a physical device
* take screen shots of the app on the physical device

> Notes like this are intended to explain the intent or thinking behind parts of the homework assignment, and are not necessary to read in order to accomplish the homework's goals. Consider them "flavor text" if you want to understand more of the "why" behind what we are doing here.

## Goal
Your task is simple: ***Use the Android Studio to scaffold out a new project, modify it slightly, then build it, deploy it, and run it, all to make sure the tools on your machine work correctly.***

> This assignment, and the one that follows, contains extensive instructions; future homework assignments will not, because I want to encourage you to solve problems your own way. This is just to get us started.

## Start
Begin by forking this repository, so you have your own copy of it your personal GitHub account.

> All of your homework assignments will be in GitHub repos; this is designed to get you experience with GitHub, as well as to avoid any of the potential problems that befall software development (laptop crashing, etc).

To fork the repo, look at the "Fork" button in the upper-right of the GitHub repository home page, click the down-arrow, and "Create a new fork". This will create a copy of the repository in your own GitHub account. Then, clone that account down to your machine, and work from that. Do not clone my repository; *you will not be allowed to post changes to my, original, repository.* The homework you turn in must come from your repository.

## Tools
While it's certainly possible to do Android development from a text editor like Visual Studio Code, in general most mobile development teams use a modern IDE like [Android Studio](https://developer.android.com/studio) to build applications.

> Note that while we are learning the Kotlin language (weeks 2 and 3 in the class), we will not use Android Studio. This is deliberate, because it's important to see how to build code outside of the IDE, too.

### Installation
If you haven't done so already, download Android Studio and install it to your machine. If you are having troubles understanding how to do that, the Google Android Studio home page has some links, such as [this one](https://developer.android.com/studio/install), that may help. The lab machines in MGW 430 should also have the latest version of Android Studio on them, you are always free to use those if something prevents you from doing so on your laptop.

> Android Studio is NOT a small piece of software--it requires a pretty decent laptop to run. You may also find it necessary to quit other programs while you are using it.

### Updates
Once you have Android Studio on your laptop, start it up.

Before you do any project work, let's get the emulator up and running. You will only need to do this once per laptop, at least for now.

Go to the "Tools" menu in the menubar, and click the "SDK Manager" menuitem inside of it. It will bring up a complicated "Settings" dialog box with the "Android SDK" option (in the left-hand column of the dialog) selected. In the center, you will see a long list of names like "Android 13.0 ("Tiramisu")" with either an empty checkbox next to it, or checked. These are different flavors of Android you can built your application to run on--if you want to run on an Android 9.0 (code-named "Pie") device, then you need the libraries for Android 9.0 ("Pie") on your machine. If that checkbox is not selected, select it.

Sometimes the box will have a "-" in it instead of a checkmark--that means there is an update to that version of the libraries available. (This will be indicated as well by a "Update available" text in the far-right "Status" column, under.) For our purposes, it probably own't make a difference, but you will often want to be up-to-date on the version of Android you're targeting. Click the checkbox until you see a check.

> We will be using Android 9.0 as our base target version, so that's all you need here; however, if you want to build an app that uses later features, you'll need the Android 10.0 ("Q"), or Android 11.0 ("R"), or other libraries. We'll talk about how to decide from this list later; for now, just stick with 9.0 ("Pie").

Click "OK", and you will see a new dialog box. THis will bring up a different dialog, and your machine will start downloading the libraries and tools from the central Android repository of all tools (at `dl.google.com`). This may take a few minutes, and it will soak up a bunch of your internet bandwidth, so it's highly suggested you don't do this while your roommate is watching Netflix. (Or at the very least, wait until they're watching something terrible, like "The Kardashians" or something.)

Now your Android Studio should be up to date.

### Build a Virtual Device
Let's create a virtual device for use by the Android Emulator. Select "Tools > Device Manager" from the menubar, or click nn the "Device Manager" tab along the far right side of the IDE. (It'll be a vertical tab, and slide out from the right when you select it). You close this tab by clicking the "-" in the upper right corner of the tab, but don't do that just yet. Make sure "Virtual" is selected, and you can see the "Create Device" button--push it.

This dialog ("Virtual Device Configuration") is designed to allow us to create a virtual representation of a physical Android device. There's a lot of options here, but let's keep it simple. Make sure "Category" (on the far left) is set to "Phone", and go ahead and click on "Pixel XL" in the center table. You should see a display to the right of that table show you some dimensions for a Pixel XL device. Click "Next".

Now it will ask you to "Select a system image". We wanted to build our application to run on an Android 9 ("Pie") device, so select that from the list and click "Next".

> One of the things mobile developers have to deal with is versioning--getting your app to run on both newer and older devices. Make sure you keep separate the version of Android your *application* is built for, and the version of Android the *device* runs. They do not need to be (and frequently aren't) the same. We will keep them both at Android 9 for this homework, though, just to keep things simpler.

Lastly, you will be asked to "Verify Configuration". Usually the defaults are fine, so just click "Finish".

You should now see a new "device" in the table in the Device Manager tab. See the "play" button in that row, under "Actions"? Go ahead and push it--that launches the emulator. If all is well, the emulator will (eventually) fire up in another tab window underneath the Device Manager. Matter of fact, it's a little tiny! In the upper-right, next to the "Hide" ("-") and "Settings" (gear) buttons is the "Window" button--push it, and it will "pop out" of the Android Studio window and become it's own window on your desktop.

This is the emulator--it is running an actual, honest-to-goodness Android system image on your machine. You use your mouse as your virtual finger, so go ahead and click down on the dot in the bottom center and drag upwards--that is you "swiping up" from the bottom of the screen to bring up all the apps on the emulator. All the apps behave exactly as they would on a real device, because they all think they're running on a real device.

Generally, it's a good idea to start the emulator up once, and leave it running while you're doing your development--starting and stopping it over and over again is a pain.

But mobile development isn't just about emulaors, it's also about physical devices. Speaking of which....

### Configure your Physical Device
Take that Android device you have in your pocket and set it next to your laptop. Let's get Android Studio to recognize it.

First, you need to get your Android device ready to receive and do some remote debugging. Ready for some super-secret developer magic? Do the following:

1. Go to Settings > About phone.
2. Scroll down to Build number. If you don't see it there, look for "Software Information" and tap on that, and it should bring up a bunch of details about the verison of Android running on that device, including "Build number".
3. Tap "Build number" seven times. (You will probably see it do some kind of countdown to let you know that it sees you tapping on it.)
4. On the seventh tap, you will see a message that reads, "You are now a developer." Or maybe "Developer options activated". Or something. More importantly, there will be a new option below "About phone" (or "About tablet", if you're on a tablet) called "Developer Options". Tap it.

In that same Device Manager tab, click on "Physical" (right next to "Virtual"). This will bring up a list of all the physical devices currently connected to your laptop. Not surprisingly, none are listed. So let's connect your device to Android Studio. There's several ways to do this:

* ***Plug a cable from your device into your computer.*** This is the OG way to do it, and is often the most reliable. (But, even having said that, there's always been some issues with Windows laptops being able to recognize Android devices over USB. Macs are usually fine, and Linux laptops usually have to recompile the kernel or somesuch. Point being, if you run into problems with the cable approach, try the Wi-Fi approach, next.) If you connect your device to the laptop and your laptop operating system "sees" it, great, you're probably good to go. On your Android device, in the Developer Options screen, make sure "USB debugging" is turned on; if it is, and your laptop recognizes your Android device, you should see the device appear in the Device Manager tab. Yay!

* ***Pair over Wi-Fi.*** Click the "Pair using Wi-Fi" button. This will bring up a dialog containing a QR code--point your device's camera at it. But before that will work, you need to go to Developer Options, and make sure "Wireless debugging" is turned on. Once it is, tap on the "Wireless debugging" text, and it will bring up another panel, which will have buttons "Pair device with QR code" and "Pair device with pairing code" (which is intended for use when the QR code doesn't work for some reason). Assuming that QR code is still up on your computer screen, push "Pair device with QR code", point your device camera at it, and within a second or two (usually), it will flash, and your computer will show a check mark instead of the QR code. More importantly, you will see the device's model number and Android OS version show up in the Device Manager tab. Yay!

You should now have both an emulated dvice and a physical device connected to your Android Studio. Coolness. Let's build an app to run on them.

## Create the Project
Select "File > New > New Project..." from the menubar. It'll present you with a number of "templates" to use to build out the project with some placeholder code--we call that *scaffolding* the project. Make sure that "Phone and Tablet" is highlighted under "Templates" (on the left), and make sure "Empty Views Activity" is selected in the center. (Should be second from top row, center.)

> There are a *lot* of templates here. If you have the time, and you want to get a jump on Android dev, after the homework is done, try doing the homework again using a different template and see the differences. Every one of these templates is immediately buildable, so you can always just select the template, fill in some settings, and build the app.

Once "Empty Views Activity" is selected (click on it if you're not sure), click "Next". Android Studio will bring you to the "New Project" dialog, which will present you with some text fields. These are fields designed to set some names for your application.

For this homeowrk assignment, change the "Name" to "Hello Android", change the "Package Name" to be `edu.uw.ischool.`{your-NetID}`.hello`. Make sure the "Save location" is a directory inside this repository, and that "Minimum SDK" is set to "API 28 ("Pie"; Android 9.0)". Leave the "Build configuration language" as "Kotlin DSL". Click OK, and Android Studio will start working to create the project, generate out some starter source code, and get things ready for you to go.

> It is not uncommon for this to download some stuff, too. Again, do it during "The Kardashians." There is a LOT of stuff to download. You may periodically get a message across the top of the screen "Gradle project sync failed. ... Try Again  Open 'Build' View ...." Click on Try Again once or twice, it's possible a hiccup in yoor internet connection interrupted the download.

Assuming it all downloads correctly, you should be presented with an application with minimal "stuff" in it that's ready to be built and deployed. Note that it can sometimes take a while (particularly the first time) to build the application--there's a LOT of stuff to download, and it all happens in the background. Keep an eye on the status bar in the IDE--if the text "Gradle Build Running..." is there with a progress bar, it means the IDE is still putting all the pieces together.

> NOTE: You will need to modify some aspects of the code, just to make sure that you can modify them and still build! I'm just getting you past some of the setup stuff first.

## Build and run the project

OK, building the project should be pretty easy at this point--the templates are all designed to build right away, so long as you haven't changed anything inside the project. See the green triangle button that looks a lot like your standard "play" icon? If you hover the mouse over it, it'll say "Run 'app'" (which is the default name of your application's main module). Just to the left of it, however, is a dropdown that tells you *where* the IDE is going to run it. On my machine, usually the emulator device appears first. Either way, when you click the green "Run 'app'" button, you should see Android Studio churn for a bit, then the device or emulator should flash, and lo and behold, the application should come up.

If it doesn't, you'll need to diagnose this before you can complete the homework--and there's not much I can tell you ahead of time to help you diagnose this.

> Sadly, one of the constants in software development is the need to debug and diagnose installation problems on your machine yourself--very rarely can anybody else do it for you. I wish it were otherwise--I hate having to do it myself--but it's a necessary part of 

If it's running, you can leave it running, or click the big red square "stop" button in the same toolbar area as where you found the green triangle "play" button. Not surprisingly, this will stop your app (but keep the emulator running).

To run it on your physical device, assuming it is connected to Android Studio, you should be able to select it in the dropdown just to the left of the "play" button; this is called the "Targets" dropdown. If it's not there, then it means that Android Studio can't see your physical device for some reason, and you may need to do some more troubleshooting.

## Make some changes, build and run it again
Now you need to make just a few changes to the app to personalize it just a bit.

> This is mostly to get you to explore in the Android Studio IDE a bit.

Please:

* Change the "Hello World" text edit to read "Go Seahawks!" or "Go Dawgs!" or "Cougars suck!" or anything more interesting than "Hello World!"
* Change the displayed name of the app (in the Android home screen) to "Hello". (This will require you to do a little Googling, but I want you to know how to do this, just in case you mis-type the application name or need to change it once you've generated the project. Trust me, typos happen.)

Rebuild and re-deploy.

## Capture the Magic
Now, take a screen shot of your app running on the emulator. Also take a screen shot of the app running on a physical device.

> This isn't just proof that you did your homework; the Google Play Store requires screen shots of your application to display in the store when people look to download it, so knowing how to do this is important for your mobile development skills.

Put the screenshots into a subdirectory called "screenshots".

## Grading Rubric
We will clone and build it from your GitHub repo. We will not get code from any other source. ("If it's not in the source code repository, it does not exist.")

* Total 5 points:
    * it builds: 2 pts
    * it runs in the emulator: 1 pt
    * we see it runs on a device: 1 pt
    * the app name is "Hello": 1 pt
* Extra credit:
    * 1 pt: Figure out how to turn on "Show layout bounds" in Developer options, and take a video of your device with that setting turned on. (This is helpful when debugging layout issues in your apps.)
    * 1 pt: Choose another developer option from the Developer Options screen, research what it's used for, and write up a quick paragraph (in your copy of this README file) on whether you believe you will use this feature during class this quarter.

When you turn in the homework in Canvas, put in the link to your GitHub repo.

## Extra Credit
* The video can be found under the `screenshots` subdirectory
* I took a look at the `Pointer Location` developer option. This feature displayed information on the current pointer location as well as a trace of the path taken by the movement. On the top there was a bar with the exact location and other statistics. I believe I will use this feature during the course of this class. Statistics such as "coordinates of touch point", "pressure being applied", and "size of touch point" will be helpful when considering responsiveness of app and dimensions of the UI features.