<p style="font-style: italic;">(originally posted on the Scholarly Technology Group blog at GW Libraries: <a href="https://library.gwu.edu/scholarly-technology-group/posts/drupal-hours-module">https://library.gwu.edu/scholarly-technology-group/posts/drupal-hours-module</a>)</p>

GW Libraries is a large organization with many groups and departments within it, all with their own hours and open days. Currently the site relies on each group manually updating their posted hours and a separate group/staff person maintaining a "master" hours table. None of this is automated and there is duplication both within each group but also on the master table.

To solve this we're building a module for Drupal that is able to automate the process for both the groups themselves but also the combined master table.

The module (called "Libsite Hours") grabs and calculates the relevant information for use where needed on the site pages. In its current (early) draft it is only providing hours for one group (Special Collections Research Center). The content managers for that group input their hours on a node called SCRC Hours of Operation. We've created fields for each day's open and close time. The module collects the data in those fields and sets a variable with the current day's hours that can be called on any page. The variable is a string that reads "Wednesday's Hours: 10am - 8pm" where Wednesday is the current day of the week and the hours are the open and close hours set on the SCRC Hours of Operation page.

The next draft will include a variable that outputs the hours for the full week, and provides a "closed" checkbox option with a field for more information (e.g. "Martin Luther King, Jr. Day"). 

The final draft will include tools for all Library groups and the aggregated (and sortable) master table of hours.

 

<p style="font-style: italic;">The module is on GitHub: <a href="https://github.com/gwu-libraries/Libsite-Hours">https://github.com/gwu-libraries/Libsite-Hours</a></p>
