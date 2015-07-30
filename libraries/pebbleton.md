---
name: Pebbleton iOS SDK
creator: Rudy Gomez
license: mit
link: https://github.com/peperodo/pebbleton-ios-sdk
language: ios
---

# Pebbleton SDK for iOS v1.0.2

A delightfully easier way to pebble.

Features:
*  Singleton convenience with no delegation needed
*  Message dispatcher via a buffer to avoid conflicts
*  Splits larger dictionaries into individual messages
*  Pre-configured toggle-able callback logs
*  Sending dictionaries of arbitrary size (Coming Soon!)

## Installation via CocoaPod

### Step 1: Add pods to Podfile

```
pod 'Pebbleton’, '~> 1.0’
```

### Step 3: Don't forget your keys

The following keys should be added to the target's .plist:

```
'Requires Background Mode' => 'App communicates with external device'
'Supported external accessory protocols' => 'com.getpebble.public'
```

## How to Use

### 1. Include framework

```
#include <Pebbleton/Pebbleton.h>
```

### 2. Initialize Singleton

```
Pebbleton *sharedPebbleton = [Pebbleton sharedInstance];
[sharedPebbleton initializeWithAppUUID:@"87c5be2a-b1dc-41bf-bc4f-b653c54ee7ae" andShowLogs:YES];
```

### 3. Call methods and callbacks

```
[sharedPebbleton printInfo];
    
// pass nil as callback if not needed
[sharedPebbleton printFirmwareInfoWithCallback:nil];

[sharedPebbleton launchAppWithCallback:^(PBWatch *watch, NSError *error){
    NSLog(@"My launch app callback");
}];

[sharedPebbleton checkCompatibilityWithCallback:^(PBWatch *watch, BOOL isAppMessagesSupported){
    NSLog(@"My compatibility callback");
}];

[sharedPebbleton setPebbleCentralWatchDidConnectCallback:^(PBPebbleCentral *central, PBWatch *watch, BOOL isNew){
    NSLog(@"My conncection callback");
}];
```

### 4. Receive message from watch

```
[sharedPebbleton setAppMessageReceiveUpdateHandler:^(PBWatch *watch, NSDictionary *update){
    NSLog(@"My received message callback");
}];
```

### 5. Send message to watch

```
// dictionary must be small enough to keep payload under 124 bytes
[[Pebbleton sharedInstance] sendMessage:@{@(KEY_TITLE_DATA): @"Title",
                                          @(KEY_DESC_DATA_1): @"Description"}
                           withCallback:nil];

// each key/value set must be small enough to keep payload under 124 bytes
NSDictionary *messages = @{@(KEY_TITLE_DATA): @"Long Title",
                           @(KEY_DESC_DATA_1): @"Long Description.",
                           @(KEY_DESC_DATA_2): @"Long Description gets cut-off",
                           @(KEY_START_DATA): @"Jan 03, 2015 2:00pm",
                           @(KEY_END_DATA): @"Jan 06, 2015 2:00pm"};

void (^callbackBlock)(PBWatch *watch, NSArray *errors) = ^(PBWatch *watch, NSArray *errors){
    if (errors.count) {
        NSLog(@"Errors sending my dictionary: %@", errors);
    } else {
        NSLog(@"Successfully my sent dictionary.");
    }
};

[[Pebbleton sharedInstance] sendDictionary:messages withCallback:callbackBlock];
```

## Overriding PBPebbleCentralDelegate (Optional)

```
- (void)pebbleCentral:(PBPebbleCentral*)central 
      watchDidConnect:(PBWatch*)watch 
                isNew:(BOOL)isNew {
    // YOUR CODE HERE
    
    [Pebbleton sharedInstance].watch = watch;
}

- (void)pebbleCentral:(PBPebbleCentral*)central 
   watchDidDisconnect:(PBWatch*)watch {
    // YOUR CODE HERE
    
    if ([Pebbleton sharedInstance].watch == watch || 
            [watch isEqual:[Pebbleton sharedInstance].watch]) {
        [Pebbleton sharedInstance].watch = nil;
    }
}
```

## Change Log

### v1.0.2
- Created new tag for new version number and CocoaPod repo

### v1.0.1
- Small log change

### v1.0.0
- Official Release

### v0.1.4
- Now using offical CocoaPod release

### v0.1.3
- Added PebbleKit dependancy to CocoaPod
- Added custom framework and debug logs

### v0.1.2

- Created api and private header files and directories
- Added public HeaderDoc comments for documentation generation
- Added missing callback arguments
- Re-factored initialization methods

### v0.1.1

- Public methods for sending dictionaries via sending each key/value pair individually
- Re-factored initialization and setter public methods
- Change the visibility of some of the class properties

