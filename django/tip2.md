---
layout: default
title: Django Fullstack Tips
description: A knowledge-sharing platform
---

# How to handle Notifications in your Django Application

_Sumit Kumar_  
_Jan 31, 2022_

## Types of Notifications

There can be three types of notifications system which might be required depending on the application type.

1. Send a notification to a user via email, SMS, or mobile push.

2. Let the user know they have unread messages or something similar, much like social media sites do with their private messages.

3. Push out data to your API users in a streaming updates fashion.

For the first one, Integrate your Django App with any of the appropriate libraries for the notification medium you want to use. [Django Anymail](https://anymail.readthedocs.io/en/stable/), [Twilio](https://www.twilio.com/), [AWS SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-email-notifications.html) etc.

The second one boils down to making an endpoint that API users can poll for updates, and storing those updates in your database. This can also be achieved via [Django messaging Framework](https://docs.djangoproject.com/en/4.0/ref/contrib/messages/) , [Django Channels](https://channels.readthedocs.io/en/stable/), [Django Signals](https://docs.djangoproject.com/en/4.0/topics/signals/) etc

The third one is slightly complex, [SSE(Server Sent Events)](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events) can be used for pushing updates in this case.

## Sending Tweet Notifications using Django Signals

Here the use case of Sending Tweet notifications to users/followers after a new blog is posted is described briefly using signals.

Django includes a signal dispatcher which helps decoupled applications get notified when actions occur elsewhere in the framework. In a nutshell, signals allow certain senders to notify a set of receivers that some action has taken place. They’re especially useful when many pieces of code may be interested in the same events.

Out of the box Django gives us several signals that are incredibly useful. We have the ability to do things pre and post save, init, delete, or even when a request is being processed. Let's say we have got a blog

```
from django.utils.translation import ugettext_lazy as _
class Post(models.Model):
    title = models.CharField(_('title'), max_length=255)
    body = models.TextField(_('body'))
    created = models.DateTimeField(auto_now_add=True)
```

We want to tweet to notify our users whenever a new post is created. With signals we have the ability to do all of this without having to add any methods to the Post class.

```
import twitter

from django.core.cache import cache
from django.db.models.signals import post_save
from django.conf import settings

def posted_blog(sender, created=None, instance=None, **kwargs):
    ''' Listens for a blog post to save and alerts some services. '''
    if (created and instance is not None):
        tweet = 'New blog post! %s' instance.title
        t = twitter.PostUpdate(settings.TWITTER_USER,
                               settings.TWITTER_PASSWD,
                               tweet)


post_save.connect(posted_blog, sender=Post)
```

The above function is executed after a blog post is saved.

Official docs - [Django Signals](https://docs.djangoproject.com/en/4.0/topics/signals/#:~:text=Django%20includes%20a%20%E2%80%9Csignal%20dispatcher,some%20action%20has%20taken%20place.)

[back](../)
