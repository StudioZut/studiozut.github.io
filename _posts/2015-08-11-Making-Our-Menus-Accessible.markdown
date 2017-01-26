<p style="font-style: italic;">(originally posted on the Scholarly Technology Group blog at GW Libraries: <a href="http://library.gwu.edu/scholarly-technology-group/posts/making-our-menu-accessible">http://library.gwu.edu/scholarly-technology-group/posts/making-our-menu-accessible</a>)</p>

One of the remaining challenges to accessibility in the GW LIbraries website (library.gwu.edu) was its main menu.

We use a ‘hover’ style menu that expands when you hover over the categories, providing an easy and commonly used navigation tool. It works well on desktops and laptops but faces a few challenges in smaller windows and devices (and one popular mobile operating system).

More importantly it wasn’t ‘keyboard accessible’: it required a mouse/trackpad or touchscreen to operate, leaving users who rely on keyboard navigation in the dark.

<div style="margin: 0 auto 0; width: 720px; max-width: 100%;">
<img src="https://github.com/StudioZut/studiozut.github.io/blob/master/_posts/screenshot-gw-libraries-8-6-15-720px.png?raw=true" alt="screenshot of the GW Libraries site in wide view (desktop)" />
</div>

screenshot: GW Libraries in wide view (desktop)

<h3>The Accessible Mega Menu</h3>

Our solution was to rebuild the menu with Adobe’s Accessible Mega Menu jQuery library: http://adobe-accessibility.github.io/Accessible-Mega-Menu/

It offered the simplest and most straightforward approach to keyboard and screen reader accessibility along with a well supported jQuery library.

But it's not responsive, and we had to customize the css and add some javascript to adjust it to our “mobile” view.

<h3>Designing for Mobile</h3>

<div style="float: right; padding: 0 0 1em 1em; width: calc(280px + 1em); max-width: calc(50% - 1em);">
<img src="https://github.com/StudioZut/studiozut.github.io/blob/master/_posts/screenshot-gw-libraries-8-6-15-narrow-280px.png?raw=true" alt="screenshot: GW Libraries site in narrow view (handheld)" />
</div>

Our menu collapses into buttons on the smallest screens (like phones) and each button becomes a link to the main categories. The new javascript-based code from Adobe dynamically inserts css classes, which we can override in our style sheet as needed (using media queries to target smaller screens).

But not all touch devices are the same. Apple devices running iOS treat hover behavior differently: when you tap something that has a hover behavior, it toggles that behavior, and most of the time ignores any other behaviors (like links). So when our menu transformed to buttons in handheld devices, you could tap the button a thousand times and nothing would happen on an iPhone. For iOS to let you follow the link we had to remove any "child items" in the menu structure: when our menu changes to buttons we're actually just hiding the rest of the structure with css. For iOS devices we're using javascript to rewrite the output and actually remove the hidden structure.

Checking for iOS devices with jQuery:
<pre>
if ($(window).width() <= 640 && navigator.userAgent.match(/(iPod|iPhone|iPad)/))
</pre>
This non-standard hover behavior helped us improve our design for all touch devices. In our fullscreen menu we now check for touch (using modernizr: http://modernizr.com) and add a main category link in each of our sub-menus when touch is detected.

Checking for Touchscreens with CSS (and Modernizr):
<pre>
html.touch .touch-show-nav {display: block;}
</pre>
<h3>Testing for Accessibility</h3>

We now run regular audits on our site designs using Google’s Accessibility Developer Tools (a free extension for Chrome: https://chrome.google.com/webstore/detail/accessibility-developer-t/fpkknkljclfencbdbgkenhalefipecmb). A lot of results have to be manually checked -- machine audits can only guess the context of potential issues -- but this gives us a baseline to help keep our sites accessible.

<h3>Adding an Accessibility Link</h3>

Lastly, we created a simple page on the main website (https://library.gwu.edu/accessibility) with a statement about our accessibility standards. We added a link to it in the footer, which we’ll be adding gradually to all of our web tools. This page will help our community know where we stand on accessibility, our limits (such as third party vendor tools) and who to contact if they need assistance.
