---
name: Hello
creator: James Mattis
link: https://github.com/jamesmattis/Hello
tags:
  - watchapp
  - ios
  - messaging
---

# Overview

_**Hello**_ demonstrates a fairly complete Pebble watch app appMessage implementation including error handling. It outputs a vareity of statistics, and provides convenient settings switches to control some of the app parameters and settings.

The basic appMessage demo apps provided by Pebble demonstrate the key features of the App Message system, but don't illustrate all of the potential errors, warning, and errata that you might encounter on a production app trying to send high rates of data to the Pebble Watch via App Message. The first issue is that you can't push an update dictionary to the watch until the previous appMessagePushUpdate method call has executed its callback block. If you attempt to do so, you will get a Code 9 "Watch rejected the pushed update error."

```Objective-C
[self.watch appMessagesPushUpdate:updateDictionary withUUID:self.appUUID onSent:^(PBWatch *watch, NSDictionary *update, NSError *error)
{
    if (error)
    {
        // There should be no error here.
    }
}];

[self.watch appMessagesPushUpdate:updateDictionary withUUID:self.appUUID onSent:^(PBWatch *watch, NSDictionary *update, NSError *error)
{
    if (error)
    {
        // There WILL be a Code 9 Error here and the update will not be sent.
    }
}];
```

Instead you have to do something like this to avoid an error:

```Objective-C
__weak __typeof__(self) weakSelf = self;

[self.watch appMessagesPushUpdate:updateDictionary withUUID:self.appUUID onSent:^(PBWatch *watch, NSDictionary *update, NSError *error)
{
    if (!error)
    {
        __strong __typeof__(self) strongSelf = weakSelf;

        [strongSelf.watch appMessagesPushUpdate:updateDictionary withUUID:strongSelf.appUUID onSent:^(PBWatch *watch, NSDictionary *update, NSError *error)
        {
            if (error)
            {
                // There should be no error here.
            }
        }];
    }
}];
```

This obviously isn't the cleanest solution, but does illustrate the key concept.

The second big issue is how to handle errors. This issue is discussed in further detail below.

Basics

_**Hello**_ uses a private dispatch queue for thread confinement. This approach is covered in many online examples elsewhere, but if you are unfamiliar with this approach, it begins by creating a private dispatch queue:

```Objective-C
dispatch_queue_t queue = dispatch_queue_create("com.jamesmattis.pebblequeue", DISPATCH_QUEUE_CONCURRENT);
dispatch_set_target_queue(queue, dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_HIGH, 0));
```

The problem that thread confinement using dispatch queues solves is that multiple threads can read from a property simultaneously safely. However, writing or updating that property isn't safe. Only one thread at a time can update a property, and while doing so, no thread can read from that propery safely. In Grand Central Dispatch, you can dispatch multiple read calls using using a dispatch_sync call on this private queue. When writing, you use a dispatch_barrier_sync call instead. The barrier keyword insures that the block submitted to the dispatch_queue is the only block in the queue . Its a simple way to implement synchronization without using locks.

Property Read:

```Objective-C
__block id valueToRead;

__weak __typeof__(self) weakSelf = self;

dispatch_sync(queue, ^{
    __strong __typeof__(self) strongSelf = weakSelf;

    valueToRead = strongSelf.value;
});
```

Property Write:

```Objective-C
__weak __typeof__(self) weakSelf = self;

dispatch_barrier_sync(queue, ^{
    __strong __typeof__(self) strongSelf = weakSelf;

    strongSelf.value = newValue;
});
```

##AppMessage PushMessage Error Handling

- When PebbleKit AppMessage pushMessage returns an error, the message has not been successfully sent to the watch. When 'Use Queue' is set to yes, it will attempt to resend the previous dictionary.

- On the Pebble Watch App, an AppMessageOutboxFailed handler is declared, which similarly looks for NACK'd message errors, and attempts to resend the failed dictionary.

- PebbleKit in general handles errors well. After some errors (particularly a series of Code 10 Timeout errors) PebbleKit will automatically reset itself. However, it doesn't seem to always reset itself as quickly as I would like. So, I manually reset the pebble session on each error in this exmaple. A reset simply calls closeSession followed by openSession. Most of the appMessage method automatically call openSession when they are called if the session isn't open. This example calls closeSession on each error, and then attempts to push an update from the closeSession callback block:

```Objective-C
[strongSelf.watch closeSession:^{

    [strongSelf pushPebbleUpdate];
}];
```

##Running the Hello Demo App

- Press any of the 'hello' buttons to start or stop a test. During the test, the app steps through the possible 'hello' strings and enqueues a new text string after a random delay. The Reduced Sniff switch toggles the Pebble Watch App sniff interval between normal and reduced mode. When Use Max Data rate is set to YES, the dictionary pushed to the Pebble watch is padded with zeroed NSData to the max dictionary size of 124 bytes. Use Queue toggles the use of a queue of dictionaries, or one single dictionary that is rewritten every time new data becomes available from the PebbleTest method. When the queue is used, you are insured that each dictionary you are trying to pass to the watch will get successfully sent and ACK'd. However, if you set a data rate faster than the watch can handle, it possible that your queue will start to fill and backup. There are situations where you don't necessarily need to have every message get successfully sent to the watch, and you might want to avoid the possibility of having the queue fill and backup. In that case, set Use Queue to no.

- The level of the random delay can be set using the #defines at the top of the ViewController.m file. The purpose of the random delay is to simulate the approximate time between CLLocationManager GPS location updates. By adjusting these values, you can find the max data rate that you can effectively send messages to the watch without filling up the queue and design your app accordingly. Setting the range to 0.0 will turn off the random part of the delay and simply dispatch message on the constant average time.

##The Logged Stats

- Run time is the total test run time.
- Number of pushes counts the total number of times that pushPebbleUpdate has been called. Successful pushes counts the number of times the queue wasn't blocked because it had yet to respond from the previous push.
- Pushed bytes gives the total bytes pushed, and the rate at which bytes have been pushed. The max rate is typically between 2.2-2.8 kB/s. This corresponds to 20-25 pushes per second, or 0.05-0.04 seconds between pushes. At fewer than 20 pushes per second, the queue typically doesn't fill. Above that, it will fill.
- Received messages are the number of messages sent from the watch to the phone.
- Blocked pushes are the number of pushPebbleUpdate attempts that could not be sent because appMessage had yet to respond from a previous push. It does not mean the message wasn't sent, but just that the system was forced to wait until an ACK was received before it was able to send the message.
- Blocked bytes are the total bytes that couldn't be pushed, including rate.
- Queued message dictionaries is the number of dictionaries currently in the queue. At 0.05 seconds between push attempts, the number in the queue is typcically small, but bounded (0-10 dictionaries in the queue). At faster push rates (< 0.05 seconds between pushes) the queue will start to fill because the messages aren't getting cleared out fast enough by the App Message System.
- Failed pushes and total errors count the number of errors returned in the appMessage callback block. It is the number of NACK'd messages.

##About the Code

- The code is split into a singleton PebbleController class that handles almost all of the interaction with the Pebble. To start the PebbleControler simply call:

```Objective-C
[[PebbleController pebble] setDelegate:self];
[[PebbleController pebble] enablePebbleHardware];
```

Dictionaries to push via App Message can then be queued using:

```Objective-C
[[PebbleController pebble] addDictionaryToQueue:dictionary];
```

- The PebbleController class has a bunch of pebble watch BOOL properties that aren't necessary in a production app, but are helpful in understanding the source and nature of various errors. Really, you just need on 'okToPushUpdate' BOOL that is set to YES whenever the appMessage system is setup, open, and has successfully returned the completion block from the previous push. There is also a lot of additional logging that isn't required in production.

- There is probably some silly bug in here somewhere. If you find something, let me know about it. Thanks!

#License

The MIT License (MIT)

Copyright (c) 2014 James Mattis. All rights reserved.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
