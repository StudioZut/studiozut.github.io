GW Libraries has nearly 20 web properties, all of which need to be tracked. We're using Google Analytics, and we've configured it with an "aggregate" account to help us track user traffic across our sites as well as within them. We've recently moved to Google's new "Universal Analytics" (analytics.js), which required some changes to our setup (see my post from last year).

Aggregate Tracking

In addition to switching out our javascript with the new analytics.js tracking code, we created a separate "aggregate" account to collect traffic from all of our accounts. We then modified our older custom javascript snippet, using the new options available in the analytics.js code (shown in purple):

ga('create', 'UA-12345678-1', 'auto');
ga('create', 'UA-01234567-1', 'auto', {'name': 'aggregate'});  // This sets the "aggregate" Analytics account.
ga('send', 'pageview');
ga('aggregate.send', 'pageview'); // This sends the pageview to the "aggregate" Analytics account.
Line 2 sets a second account (we named it "aggregate"), and the fourth line sends a set of the site's tracking data to the second account.

Cross-Domain Tracking

One of the goals is to see how visitors move between our web properties. Since all of our sites are subdomains of the same second level domain gwu.edu, Analytics doesn't require anything more than setting the second account in order to track traffic between properties:

screenshot: google analytics cross-domain flow

If your sites have different domains, Google has excellent documentation to implement cross-domain tracking manually. 

Event Tracking and "Non-Interaction" Events

In addition to tracking page traffic, we're using "event tracking" code to tell us when visitors used certain tools or links. 

One of the behaviors we're tracking is our primary navigation menu: we set an event to trigger when someone hovers over the category menu item (which expands when hovering). To prevent this from being treated as a page interaction, we set these as non-events: {'nonInteraction': 1}. Otherwise Analytics would confuse the "mouse hover" as an event in which the user interacted with the page, impacting the Bounce Rate (as well as a few other metrics). 

The "event tracking" code is a short piece of javascript:

ga(‘send’, ‘event’, ‘primary-navigation’, ‘/primary-nav/gelman-library/research-hover’, {'nonInteraction': 1});

When added to the anchor tag looks like this:

<a onMouseOver="ga(‘send’, ‘event’, ‘primary-navigation’, ‘/primary-nav/gelman-library/research-hover’, {'nonInteraction': 1});">Research</a>

The 'hover' behavior is triggered by the onMouseOver event (vs. onClick). The last parameter {'nonInteraction': 1} sets it as a 'non-interaction' event.

Using the Drupal Analytics Module

Our Drupal sites use the analytics module (https://www.drupal.org/project/google_analytics), which has fields for custom javascript as well as a lot of helpful features. To set up aggregate tracking we dropped javascript into two of the fields in the Custom section:

Those two lines are the same as the two (in purple) we added in the first section on Aggregate Tracking.

Honoring Do Not Track

Thanks to a simple checkbox in the Privacy section, the Drupal analytics module makes it easy to honor "do not track". It also has an option for anonymization of visitor IP addresses.

For our non-Drupal sites we wrap the Analytics code in a conditional statement that checks the value of navigator.doNotTrack. Mozilla has documentation on coding for Do Not Track.

A Better Understanding of Our Visitors

With this in place we can look in one location for our combined traffic data and see how visitors move between our sites. This has been especially useful in understanding usage of our main GW Libraries website, which serves as a launchpoint for many of our other tools: we can now watch as visitors move within and across our web properties.

All of this helps us build better tools for our community and implement user centered designs that provide a better and more consistent user experience.
