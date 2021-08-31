## Paywall Buster: Using headless Chrome command line within PHP to display embedded image of remote website using JavaScript.

The Paywall Buster uses headless chrome and javascript to embed an image of a remote site in the webpage one is viewing. An example is to visit [@pulpnews](http://twitter.com/pulpnews), and click on any of the tweets. This takes you to a page with a button to see the website. If the user encounters a paywall when using a link, then they can press a button and get the remote website's image embedded on the page which the can further click on to display it at maximum size.

>It looks like this: 
>![OddCrimes Crime News Item](https://oddcrimes.com/o/images/paywall_buster.jpg)

## Is this legal?
My site, [OddCrimes.Com](https://OddCrimes.Com), can be used for research. The database goes back over 10 years and I offer statistics on crime as well. Users decide whether they should click the button based on the law, 17 U.S. Code § 107 - Limitations on exclusive rights: Fair use. https://www.law.cornell.edu/uscode/text/17/107. The service is offered in good faith.

## Required Resources
Prerequisites:
  * Web server [virtual machine #1]
  * Backend server [virtual machine #2]
  * Database [this uses MySQL 5.5, but any database can be used]
  * Shared folder that both virtual machines can access.

## What the user doesn't see.
When the user presses the button, the request is placed in the database. Virtual machine #2 monitors the databases every minute. When it sees a new entry, it takes the id number and gets the url. It uses headless chrome to go to the url and take a snapshot (pdf or html file types can be used instead of an image using the switches in the chrome command line). 

The image is saved on a virtual drive accessible by the webserver and a webpage that displays the full sized image is created.  If the user clicks on the embedded image, it will take then to the full size image page. It then deletes the databases record.

## Advantages of doing it this way:
 * The process cannot be interupted by the user, meaning that they can leave the page once the button is clicked and the process will complete.
 * Using the database to establish a queue so that only one chrome process is used, keeping resources used at a minimum.
 * The image is permanent, so it is accessed quicker the second time around.
 * Only the news item people are interested in are saved, limiting storage to only those images.
