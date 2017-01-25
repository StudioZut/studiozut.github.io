If you’re patching your Drupal installation regularly (core and module updates) you’re halfway there. 

An important disclaimer: I’m not addressing the server environment (LAMP stack) in this post, which is critical to security. If you’re using a hosting service, be sure to check on their security policies and makes sure they’re updating your server. 


<h3>Part 1: Secure Connecting</h3>

Make sure you’re configured to pass login and form submissions over a secure connection. If you’re using a hosted service, check their options for adding a certificate to your site: on some services (like Dreamhost) it’s as simple as checking some boxes.

In a future post I’ll address adding certificates to your site in detail (configuring Apache and generating certificates) so you can run connections securely over https using SSL (Secure Socket Layer).

If your site accepts both http and https requests (instead of routing all requests over https), I recommend the Secure Login module (<a href="https://www.drupal.org/project/securelogin">https://www.drupal.org/project/securelogin</a>). This will let you force login requests and form submissions over https. Why is this important? If you don’t use a secure connection for logins or forms, all the submitted information (including passwords) is sent using clear text (unencrypted plain text) and can be intercepted.

These are the settings I tend to use, which include forcing forms of any kind to submit over a secure connection:

<img src="https://github.com/StudioZut/studiozut.github.io/blob/master/_posts/Screen%20Shot%202017-01-25%20at%2010.49.03%20AM.png?raw=true" alt="screenshot of the admin settings for the Secure Login module">

Note: if you’re using the Drupal login block on a page and you’re using Secure Login, that page will load over https. By default new Drupal 7 installations include the login block on the home page.

A last point on securing your site: it’s good for SEO! Google ranks secure sites higher, so you can check off another box on your Search Engine Optimization to-do list.  


<h3>Part 2: Accessible Spam Protection</h3>

On my sites I use the aptly-named Honeypot module (<a href="https://www.drupal.org/project/honeypot">https://www.drupal.org/project/honeypot</a>), a simple and effective way to catch spam in forms (comments, contact forms, anything that allows an anonymous user to submit something). I prefer Honeypot over Captcha because (a) it’s invisible to the user and (b) it meets accessibility requirements.

Comment sections tend to be hit the most on the Drupal sites I’ve built, and with Honeypot I’ve reduced spam to very manageable crumbs. If new comments from anonymous users are set to require approval (which I highly recommend) this will keep your site “spam free” on the user side and limit the spammed comments to a trickle that are easily deleted.

Configuring Honeypot:

Once you install the module, you can adjust the settings from the configuration page:


I’d start with the default settings and then adjust from there if anything is getting through. I recommend starting with the time limit setting first, then tinkering with the element name if spam is still managing to get through. And remember to check the logs!

These two easy steps will help make your Drupal site both more secure and less of a headache. 
