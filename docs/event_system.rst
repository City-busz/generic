Event system
============

Generic library provides ``generic.event`` module which helps you implement
event systems in your application. By event system I mean an API for
*subscribing* for some types of events and to *handle* those events so previously
subscribed *handlers* are being executed.

.. contents::
   :local:

Basic usage
-----------

First you need to describe event types you want to use in your application,
``generic.event`` dispatches events to corresponding handlers by inspecting
events' types, so it's natural to model those as classes::

    >>> class CommentAdded(object):
    ...   def __init__(self, post_id, comment):
    ...     self.post_id = post_id
    ...     self.comment = comment

Now you want to register handler for your event type::

  >>> from generic.event import Manager

  >>> manager = Manager()

  >>> @manager.subscriber(CommentAdded)
  ... def print_comment(ev):
  ...   print(f"Got new comment: {ev.comment}")

Then you just call ``generic.event.handle`` function with ``CommentAdded``
instance as its argument::

  >>> manager.handle(CommentAdded(167, "Hello!"))
  Got new comment: Hello!

This is how it works.

Event inheritance
-----------------

Using per-application event API
-------------------------------

API reference
-------------

.. autoclass:: generic.event.Manager
   :members: subscribe, subscriber, handle, unsubscribe
