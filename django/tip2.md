---
layout: default
title: Django Fullstack Tips
description: A knowledge-sharing platform
---

# How to use signals in your Django Application

_Sumit Kumar_  
_Jan 24, 2022_

Django includes a “signal dispatcher” which helps decoupled applications get notified when actions occur elsewhere in the framework. In a nutshell, signals allow certain senders to notify a set of receivers that some action has taken place. They’re especially useful when many pieces of code may be interested in the same events.

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
