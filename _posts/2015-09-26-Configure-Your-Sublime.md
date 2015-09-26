---
layout: post
title:  "How to Configure Your Sublime Text 3 So It Looks Nicer"
date:   2015-09-26 18:22:25
categories: tech
---

[Sublime Text 3](http://www.sublimetext.com/3) is a very popular text editor due to its clean aesthetics and user-friendly interface. Underneath the attractive appearance, it is also customizable through editing your user preference file and/or various plugins. 

One nifty trick is the ability to change the font you use. In your Sublime Text window, navigate to "Sublime Text" -> "Preferences" -> "Settings - User" or simply press Ctrl + , (on a mac) to open your user preference file in a new tab. 

In the user preference file, you will be able to change display settings such as font_face and line_padding. Moreover, for fellow tabbers, you are able to specify the number of spaces tab key represents and whether or not pressing tab will be automatically converted to spaces.

I am sharing my setting below: 

{% highlight js %}
{
  "color_scheme": "Packages/User/SublimeLinter/Solarized (Dark) (SL).tmTheme",
  "font_size": 20,
  "ignored_packages":
  [
    "Vintage"
  ],
  "tab_size": 2,
  "translate_tabs_to_spaces": true,
  "font_face": "SourceCodePro-Regular",
  "line_padding_top": 1,
  "line_padding_bottom": 1
}
{% endhighlight %}


Note that "SourceCodePro-Regular" is a clean monospaced font that will surely make your Sublime experience even more pleasant. You will have to install it on your computer before using it, and you can download it from [Google Fonts](https://www.google.com/fonts/specimen/Source+Code+Pro).
