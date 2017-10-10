# Gmail Markup

**Google** allows you to interact with your email in a limited number of ways.

One way is to *Click a button* for example you want to confirm whether an email from a potential client needs attention.

And *Creating and showing this button*, is what we are going to walk through in write up.

# Scenario
We want the user to click a button specified on our **application/ld+json** script.

```json
{
    "@context": "http://schema.org",
    "@type": "EmailMessage",
    "thumbnailUrl": "http://example.com/assets/image.png",
    "headline": "Response from mark@example.com",
    "text": "Mark from Google responded to your email in Inbox (jon@comapny.com)",
    "discussionUrl": "https://mail.google.com/mail/u/1/#inbox/xyz789",
    "potentialAction": [{
    "@type": "SaveAction",
    "name": "Ignore Person",
    "handler": {
        "@type": "HttpActionHandler",
        "url": "https://example.com/ignore/person?messageId=xyz789",
        "method": "HttpRequestMethod.GET"
    }
    },{
    "@type": "SaveAction",
    "name": "Ignore Message",
    "handler": {
        "@type": "HttpActionHandler",
        "url": "https://example.com/ignore/message/?messageId=xyz789",
        "method": "HttpRequestMethod.GET"
    }
    }]
}
```

* Full email html content 
```html
<html lang="en">
    <body>
        <script type="application/ld+json">
            {
                "@context": "http://schema.org",
                "@type": "EmailMessage",
                "thumbnailUrl": "http://example.com/assets/image.png",
                "headline": "Response from mark@example.com",
                "text": "Mark from Google responded to your email in Inbox (jon@comapny.com)",
                "discussionUrl": "https://mail.google.com/mail/u/1/#inbox/xyz789",
                "potentialAction": [{
                "@type": "SaveAction",
                "name": "Ignore Person",
                "handler": {
                    "@type": "HttpActionHandler",
                    "url": "https://example.com/ignore/person?messageId=xyz789",
                    "method": "HttpRequestMethod.GET"
                }
                },{
                "@type": "SaveAction",
                "name": "Ignore Message",
                "handler": {
                    "@type": "HttpActionHandler",
                    "url": "https://example.com/ignore/message/?messageId=xyz789",
                    "method": "HttpRequestMethod.GET"
                }
                }]
            }
        </script>
        <p>
            Dear John, Mark from Google responded to your email in Inbox (john@comapny.com)
        </p>
        <p>
            MESSAGE DETAILS<br/>
            Hi John<br/>
            Your product looks great<br/>
            but it more expensive than what we use now<br/>
            and we do not plan to switch.<br/>
            Sincerely
        </p>
    </body>
</html>
```

# End Goal

TODO put picture of the button in Gmail

# Step by Step

* Go to Google's [Email markup site](https://developers.google.com/gmail/markup/) and complete their [apps-script-tutorial](https://developers.google.com/gmail/markup/apps-script-tutorial) walkthrough.

NOTE that the tutorial relies on **Google Apps Script** technology to send email.

* Replace the html code you used in the [apps-script-tutorial](https://developers.google.com/gmail/markup/apps-script-tutorial), with the one below

NOTE that we are using **SaveAction** instead of **ViewAction**

```html
<html lang="en">
    <body>
        <script type="application/ld+json">
            {
                "@context": "http://schema.org",
                "@type": "EmailMessage",
                "thumbnailUrl": "http://example.com/assets/image.png",
                "headline": "Response from mark@example.com",
                "text": "Mark from Google responded to your email in Inbox (jon@comapny.com)",
                "discussionUrl": "https://mail.google.com/mail/u/1/#inbox/xyz789",
                "potentialAction": [{
                "@type": "SaveAction",
                "name": "Ignore Person",
                "handler": {
                    "@type": "HttpActionHandler",
                    "url": "https://example.com/ignore/person?messageId=xyz789",
                    "method": "HttpRequestMethod.GET"
                }
                },{
                "@type": "SaveAction",
                "name": "Ignore Message",
                "handler": {
                    "@type": "HttpActionHandler",
                    "url": "https://example.com/ignore/message/?messageId=xyz789",
                    "method": "HttpRequestMethod.GET"
                }
                }]
            }
        </script>
        <p>
            Dear John, Mark from Google responded to your email in Inbox (john@comapny.com)
        </p>
        <p>
            MESSAGE DETAILS<br/>
            Hi John<br/>
            Your product looks great<br/>
            but it more expensive than what we use now<br/>
            and we do not plan to switch.<br/>
            Sincerely
        </p>
    </body>
</html>
```

* Save the html and then resend the email as you did in the [apps-script-tutorial](https://developers.google.com/gmail/markup/apps-script-tutorial)
