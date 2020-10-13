Referring to: https://github.com/xamarin/AndroidSupportComponents/issues/140

I can reproduce this as well on latest version, Microsoft Visual Studio Community 2019 Version 16.5.2 on a new Project from template, these are the steps:

Create new project
Android App (Xamarin)
Tabbed App

Build Solution

Browse the solution Explorer under Resources- Layout - Activity_Main.xml
The designer is working.

Go to Application Properties, change Target Framework to Android 10
Open Manage nuGet Packages for the App, Perform all the updates
Save and exit Visual Studio
Re-Open visual Studio and open the project.

Build - Clean Solution
Build - Rebuild App
This one is failing with error
Severity Code Description Project File Line Source Suppression State
Error Could not find 9 Android X assemblies, make sure to install the following NuGet packages:

Xamarin.AndroidX.Lifecycle.LiveData
Xamarin.Google.Android.Material
You can also copy-and-paste the following snippet into your .csproj file:

NewApp Build
So I closed visual Studio, opening the .csproj with notepad added the two PackageReference I copied from the error message.

Open Visual studio, use the nuget Dependencies manager on the App to Perform the updates
Build - Rebuild Solution
Failing with this error

Severity Code Description Project File Line Source Suppression State
Warning Could not find 1 Android X assemblies, make sure to install the following NuGet packages:

Xamarin.AndroidX.AppCompat.Resources
You can also copy-and-paste the following snippet into your .csproj file:
NewApp Build
Again close visual Studio, edit .csproj with notepad to add the PackageReference
Open Visual studio, use the nuget Dependencies manager on the App to Perform the updates
Build - Clean Solution
Build - Clean App
Build - Build App

Build Succeeded, Anyway whenever I try to open the editor on Resources\Layout\activity_main.xml I am seeing the message
"Could not load control from the Android Support Library. performing a NuGet restore may fix this."
The widget at bottom is not shown as result of the error.

You can find the resulting source that will include the "broken" design at https://github.com/alessandro-lion/NewApp