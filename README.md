Keen IO OS X Client
===================

The Keen IO OS X client is based on the Keen IO [iOS client](https://github.com/keenlabs/KeenClient-iOS). You can safely use the iOS API and Client Documentation to get going with this library.

[iOS API Documentation](https://keen.io/static/iOS-reference/index.html)

[iOS Client Documentation](https://keen.io/docs/clients/iOS/usage-guide)

##### Build Settings

1. Import all the source files.
2. If you're using ARC for your project, [disable ARC](http://stackoverflow.com/questions/6646052/how-can-i-disable-arc-for-a-single-file-in-a-project) for all classes you just imported.
3. Make sure to add CoreLocation.framework to the "Link Binary with Libraries" section.
4. Under "Capabilities -> App Sandbox" of your project - (if it is a Sandboxed application)

    i. Enable the "Outgoing Connections (Client)" so data can be sent to Keen.
    
    ii. Enable "Location" if you want to send location data to Keen. 

Voila!

### Usage

To use this client with the Keen IO API, you have to configure your Keen IO Project ID and its access keys (if you need an account, [sign up here](https://keen.io/) - it's free).

##### Register Your Project ID and Access Keys

```objc
    - (void)applicationDidFinishLaunching:(NSNotification *)aNotification
    {
        [KeenClient sharedClientWithProjectId:@"your_project_id" andWriteKey:@"your_write_key" andReadKey:@"your_read_key"];
    }
```

The write key is required to send events to Keen IO. The read key is required to do analysis on Keen IO.

##### Add Events

Use the client like so:

```objc
    - (void)someMethod
    {
        NSDictionary *event = [NSDictionary dictionaryWithObjectsAndKeys:@"event_source", @"awesome source",
                               @"started_by", @"some user action", nil];
        [[KeenClient sharedClient] addEvent:event toEventCollection:@"event_name" error:nil];
    }
```

##### Upload Events to Keen IO

Adding events just stores the events locally on the device. You must explicitly upload them to Keen IO. Here's how:

```objc
    [[KeenClient sharedClient] uploadWithFinishedBlock:^(void) {
        NSLog(@"Uploaded data to Keen!");
    }];
```
You can upload data as soon as the events are added, or create an NSThread to upload it periodically.

##### Do analysis with Keen IO

    TO DO
    
That's it! After running your code, check your Keen IO Project to see the event has been added.

### Questions & Support

Report your questions, bugs or suggestions via Github issues.

### Credits
This is project is based on code originally written by David Schiefer (david.schiefer@me.com). Thank you David! 