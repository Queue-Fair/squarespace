---
## Queue-Fair Free SquareSpace Virtual Waiting Room README & Installation Guide

Queue-Fair can be added to your SquareSpace shop easily in minutes, and is a great way to get a free SquareSpace virtual waiting room, as Queue-Fair offers its own Free Tier, and the Adapter methods below are free or use AWS free tier services.  You will need a Queue-Fair account - please visit https://queue-fair.com/free-trial if you don't already have one.  You should also have received our Technical Guide.  To find out more about how a Virtual Waiting Room protects your site or app from traffic spikes, see https://queue-fair.com/virtual-waiting-room

## Client-Side JavaScript Adapter

Most of our customers prefer to use the Client-Side JavaScript Adapter, which is suitable for all sites that wish solely to protect against overload.

To add the Queue-Fair Client-Side JavaScript Adapter to your SquareSpace shop, you don't need the Network-Edge Adapter described later in this README.

Instead, add the following tag to the `<head>` section of your pages:
 
```
<script data-queue-fair-client="CLIENT_NAME" src="https://files.queue-fair.net/queue-fair-adapter.js"></script>
```

Replace CLIENT_NAME with the account system name visibile on the Account -> Your Account page of the Queue-Fair Portal

In SquareSpace, you can add this tag easily by logging into SquareSpace, selecting your website, Website from the left nav, Website Tools (in the Utilities section in the left nav), Code Injection, and then copy and paste it into the Header box, then Save at the top left.

You shoud now see the Adapter tag when you perform View Source after refreshing your pages.

And you're done!  Your queues and activation rules can now be configured in the Queue-Fair Portal.

## SquareSpace Network-Edge Adapter
Rather than use the Client-Side JavaScript Adapter, some of our SquareSpace clients prefer to take advantage of the additional security features offered by our other Adapters.  It is not possible to use a Server-Side Adapter with a SquareSpace shop as SquareSpace does not support server-side code, but you can use one of our Network-Edge Adapters to make Queue-Fair fully secure and unskippable.

You can try our Cloudflare Adapter at https://github.com/queue-fair/cloudflare , but some clients have reported issues at SquareSpace if `Use "www" prefix` is enabled on your site's Domain settings in SquareSpace when using Cloudflare.  The issue may not show up right away.  We therefore recommend our AWS CloudFront Adapter instead for Squarespace shops and sites.

So, here's how to add CloudFront to your SquareSpace site and run the Queue-Fair Network-Edge Adapter.

**1.**  Go to https://aws.amazon.com and sign up for a free AWS account.

**2.**  Log in to your AWS account.  In the search box at the top left, start typing CloudFront.   Give it a Star so it's pinned to your top nav, and click on it when it appears.  Then you want the big orange Create a CloudFront distribution.

**3.**  You can leave the default settings apart from:
*Origin*
   * Origin Domain must be set to `ext-cust.squarespace.com`
   * Protocol should be Https Only
   * Name should be `mycompany.com`, the domain you use for your SquareSpace site, without any `www.` at the front
   
*Default cache behaviour*
   * Allowed HTTP methods should be everything - GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE
   * Cache policy should be CachingDisabled - you don't need or want caching on your SquareSpace site, as SquareSpace has its own CDN.
   * Origin request policy should be AllViewer.
   
*Function associations*
   * Leave set to `No association` for now.

*Web Application Firewall (WAF)*
   * Do not enable.

*Settings*
   * Alternate domain name - add your domain both with and without the www, so both mycompany.com and www.mycompany.com, one domain per item.
   * You will probably want Amazon to create the certificate for you, so hit Request certificate.  This will open a new tab.  Request a public certificate, Next.  Add both names (with and without the `www.`) to the certificate, one domain per item,
 and perform the DNS validation.  On the page that follows, you will see Certificate status, and two CNAMEs that must be added to your DNS provider for Amazon to issue the certificate.  Once they have been added, it will take a few minutes for Amazon to create the certificate, and you can check  when it's done by refreshing the page.  Have a cup of tea.  When the Status becomes Issued with a green tick, go back to the other tab, hit the Refresh icon next to `Choose certificate` and select your newly-created certificate from the pulldown.

**4.**  Now just click Save & Deploy, and that's it you've set up Cloudfront for your SquareSpace site!  Well done you!  However, Cloudfront will not be called until you add it to your request routing.  There are two ways of doing this.

If you DO have Use "www" Prefix enabled in your SquareSpace domain settings, it's super easy - just change the CNAME record for www at your DNS provider to the Distribution Domain Name, which is a long string of letters and numbers followed by .cloudfront.net that you can see on the Distributions page, such as e2slh2uy2m89es.cloudfront.net - we recommend you set the TTL on this record to five minutes or less, so you can revert changes quickly.

If you DON'T have Use "www" Prefix enabled in your SquareSpace domain settings, it's a little more tricky - you need to create a Route 53 record for your main domain.  The instructions are at https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-to-cloudfront-distribution.html

**5.**  Once any TTL has timed out on your old records, check that Cloudfront is active on your SquareSpace site.  You can do this by right-clicking, inspect and the Network tab.  Your page requests should have additional headers in the response with the letters "cf" - once you see that, Cloudfront is in the request route and it's working.

**6.**  Now you are ready to install the Cloudfront Adapter as described at https://github.com/queue-fair/cloudfront - start at Step 1 there. 
   
 
