---
layout: master
title: Whitney Young
---

# Hello

Greenwich is quick to set up. You'll want to download one of the compiled versions from the
downloads section of GitHub. Once you've downloaded Greenwich, there are three parts
to the setup: scripts, framework, and code.

These instructions are slightly different for <a href="#ios">iOS</a> and <a href="#mac">Mac</a>. Please
select which version of the instructions you wish to use before you begin.

<div class="switch"><a href="#ios">iOS</a><a href="#mac">Mac</a></div>
<div class="mac-specific"></div>

**You are currently viewing the Mac setup instructions.**

<div class="ios-specific"></div>

**You are currently viewing the iOS setup instructions.**

### Scripts

The Greenwich download comes with a folder called Scripts. You'll need to copy this folder
to a location where your build will be able to find the scripts. It is generally advisable
to copy the entire folder into your project directory, but you can also put the scripts
in a shared location so multiple projects can use the same installation.

Once the scripts are copied, you need to configure your Xcode project to use the scripts.
This is as simple as adding a few _Run Script_ build phases. In your Xcode project:

<div class="switch"><a href="#ios">iOS</a><a href="#mac">Mac</a></div>
<div class="mac-specific"></div>

  1. Click on your project in the project navigator
  1. Select your application target in the targets section
  1. Switch to the _Build Phases_ tab
  1. Click _Add Build Phase_
  1. Choose _Add Run Script_
  1. Move this build phase **below** the _Copy Bundle Resources_ build phase
  1. Update the script to `./Scripts/localization create -s. -r.`

<div class="ios-specific"></div>

  1. Click on your project in the project navigator
  1. Select your iOS target in the targets section
  1. Switch to the _Build Phases_ tab
  1. Click _Add Build Phase_
  1. Choose _Add Run Script_
  1. Move this build phase **below** the _Copy Bundle Resources_ build phase
  1. Update the script to `./Scripts/localization create -s. -r.`

[![Set Runpath Search Paths](http://fadingred.github.com/greenwich/media/images/runpaths_thumbnail.png)](http://fadingred.github.com/greenwich/media/images/runpaths.png)
[![Add Run Script](http://fadingred.github.com/greenwich/media/images/runscript_thumbnail.png)](http://fadingred.github.com/greenwich/media/images/runscript.png)
[![Define Run Script](http://fadingred.github.com/greenwich/media/images/definescript_thumbnail.png)](http://fadingred.github.com/greenwich/media/images/definescript.png)

Note that the script may need to be altered slightly depending on your configuration. The path
to the script should relative to your project's `.xcodeproj` file. If you put the scripts folder in a
folder called `External`, you would need to change the beginning of the script
to `./External/Scripts/localization`. The scripts also
take a couple of options to allow you to specify where different files are located.
If your source files and xib files are located in the same directory as your
project's `.xcodeproj` file, then the options provided
in the example above are be correct. If they're in different locations, though, you'll have to alter the
arguments that are passed to the script. For most uses, you will only need to specify `-s`, the path to your
source files, and `-r`, the path to your resources. Paths relative to your project's `.xcodeproj` file are acceptable.
For example, if your source files are in a folder called
`Implemenation`, you would need to specify `-s Implementation`, and if your xib files are in a folder called
`Interface Files`, you need to specify `-r "Interface Files"`.

Greenwich will only extract strings from unlocalized xib files. If you leave your xib files in the
lproj directories, they will not be handled by Greenwich. Simply move your master out of the lproj
directory if you want Greenwich to handle it. You won't need all those extra xibs any more, phew!

For an example of setting up the scripts using the `PATH` environment variable, check out
the example application included with the source code.

<div class="mac-specific"></div>

### Framework (Copying & Linking)

<div class="ios-specific"></div>

### Framework

{% capture framework_info %}The distribution
includes the framework which you should copy to a location where your project can access it. Again,
it is generally advisable to copy the framework into your project directory. Once in place, there
are just a few steps to getting it added into your project:{% endcapture %}

<div class="mac-specific"></div>

Linking and copying the framework is similar to other Mac OS X frameworks. {{ framework_info }}

<div class="ios-specific"></div>

Linking framework is similar to other iOS frameworks. {{ framework_info }}

{% capture framework_shared_steps %}1. Activate the project navigator in Xcode
  1. Drag `Greenwhich.framework` into the _Frameworks_ group
  1. Xcode will display a dialog for adding files
  1. Make sure your application target is checked, then click _Finish_
  1. Click on your project in the project navigator
  1. Select on your target in the targets section
  1. Switch to the _Build Settings_ tab{% endcapture %}

<div class="switch"><a href="#ios">iOS</a><a href="#mac">Mac</a></div>
<div class="mac-specific"></div>

  {{ framework_shared_steps }}
  1. Set _Runpath Search Paths_ to `@executable_path/../Frameworks`
  1. Switch to the _Build Phases_ tab
  1. Click _Add Build Phase_
  1. Choose _Add Copy Files_
  1. Change the _Destination_ to _Frameworks_
  1. Drag `Greenwich.framework` from the project navigator into the copy files list

<div class="mac-specific"></div>

[![Drag Framework](http://fadingred.github.com/greenwich/media/images/frameworkdrag_thumbnail.png)](http://fadingred.github.com/greenwich/media/images/frameworkdrag.png)
[![Add Framework](http://fadingred.github.com/greenwich/media/images/frameworkadd_thumbnail.png)](http://fadingred.github.com/greenwich/media/images/frameworkadd.png)
[![Copy Framework](http://fadingred.github.com/greenwich/media/images/frameworkcopy_thumbnail.png)](http://fadingred.github.com/greenwich/media/images/frameworkcopy.png)

<div class="ios-specific"></div>

  {{ framework_shared_steps }}
  1. Set _Other Linker Flags_ to `-ObjC`

<div class="ios-specific"></div>

[![Drag Framework](http://fadingred.github.com/greenwich/media/images/frameworkdrag_thumbnail.png)](http://fadingred.github.com/greenwich/media/images/frameworkdrag.png)
[![Add Framework](http://fadingred.github.com/greenwich/media/images/frameworkadd_thumbnail.png)](http://fadingred.github.com/greenwich/media/images/frameworkadd.png)

### Code

At this point, you still need to add a little code to your application, but this is easy:

<div class="switch"><a href="#ios">iOS</a><a href="#mac">Mac</a></div>
<div class="mac-specific"></div>

    #import <Greenwich/Greenwich.h>
    
    @interface MyAppDelegate
    
    - (void)applicationDidFinishLaunching:(NSNotification *)notification {
    	[[FRLocalizationManager defaultLocalizationManager] installExtraHelpMenu];
    }
    
    @end

<div class="ios-specific"></div>

    #import <Greenwich/Greenwich.h>
    
    @interface MyAppDelegate
    
    - (void)applicationDidFinishLaunching:(NSNotification *)notification {
    	[FRLocalizationManager defaultLocalizationManager];
    }
    
    @end

<div class="mac-specific"></div>

When you launch the application, you can bring up the translator by holding down option while
opening the _Help_ menu... easy peasy.

<div class="ios-specific"></div>

Your application now includes everything necessary to use Greenwich. Simply launch the translator
tool that comes with the Greenwich download, and it will connect to your device... easy peasy.

<script>
var active = null;
var updateTo = function(type, element) {
	if (active == type) { return; }
	else { active = type; }
	
	var hide = null;
	var show = null;
	if (type=='mac') {
		$('a[href="#mac"]').addClass('selected');
		$('a[href="#ios"]').removeClass('selected');
		hide = $('.ios-specific').next(':not(:text)');
		show = $('.mac-specific').next(':not(:text)');
	}
	else if (type=='ios') {
		$('a[href="#ios"]').addClass('selected');
		$('a[href="#mac"]').removeClass('selected');
		hide = $('.mac-specific').next(':not(:text)');
		show = $('.ios-specific').next(':not(:text)');
	}
	
	var offset = $(document).scrollTop();
	var change = 0;
	var updateChange = function(multiplier) {
		if (!element) { return false; }
		var clickedOffset = $(element).offset().top;
		var thisOffset = $(this).offset().top;
		if (thisOffset < clickedOffset) {
			change += $(this).height() * multiplier;
		}
		return true;
	};
	hide.each(function() { updateChange.call(this, -1); }).hide();
	show.show(0, function() { updateChange.call(this, 1) && $(document).scrollTop(offset+change); });
};
$('a[href="#mac"]').each(function(index, element) {
	$(element).click(function() { updateTo('mac', element); });
});
$('a[href="#ios"]').each(function(index, element) {
	$(element).click(function() { updateTo('ios', element); });
});
if (window.location.hash) { updateTo(window.location.hash.substr(1)); }
else { updateTo('ios'); }
</script>


## Usage

Once you've set everything up, you're good to go. Greenwich will work with your existing calls to
`NSLocalizedString` and will translate all your xib files as they're loaded. In certain cases,
however, you may find that you need to make a few changes to the positions of UI elements after
localization has occurred. Don't worry, we've got you covered:

    - (void)awakeFromLocalization {
        // calculate the size of ui elements & reposition things
    }

If you're using your own macro based off of `NSLocalizedString`, simply define the `GREENWICH_LOCALIZATION_SYMBOL` in
your Xcode configuration with that symbol, and Greenwich will handle it from there!

Setting the environment variable `GREENWICH_PSEUDO_LOCALIZE` will make Greenwich pseudo-localize your application.
It will swap out certain characters and extend your strings slightly while keeping them identifiable. This setting is
great for testing to make sure that everything is localized and that you've allowed enough space for strings
in other languages.


## Extras

There's also a [guide](http://fadingred.github.com/greenwich/guide/) that you can
[customize](http://fadingred.github.com/greenwich/guide/?customize=1) and send to your translators.

Greenwich includes a [proofer tool](https://github.com/fadingred/Greenwich/blob/master/Framework/Proofer/Readme.md)
that will allow you to validate user translations.
