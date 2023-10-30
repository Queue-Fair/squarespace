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

You can try our Cloudflare Adapter at https://github.com/queue-fair/cloudflare , but some customers have reported issues at SquareSpace if `Use "www" prefix` is enabled on your domain settings when using Cloudflare.  We therefore recommend our Cloudfront Adapter instead for Squarespace site.

