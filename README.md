# flutter_instagram_stories

Display stories just like Whatsapp & Instagram. Built-in groups (multiple stories with one icon), cache, video, gifs. For now works with Firebase only.

<p float="right">
  ![Showcase|100x100, 10%](example/lib/showcase1.gif)
</p>


This a Flutter widget to display stories just like Whatsapp and Instagram. Can also be used
inline/inside ListView or Column just like Google News app. Comes with gestures
to pause, forward and go to previous page.

# Features

🕹 Still image, GIF and video support

📍 Gesture for pause, rewind and forward

⚜️ Caption for each story item

🎈 Animated progress indicator for each story item

And useful callback to perform meta functionalities.


# Installation

To use this plugin, add `story_view` as a [dependency in your pubspec.yaml file](https://flutter.io/platform-plugins/).

## iOS

For playing video uses official video_player plugin https://pub.dev/packages/video_player

From documentation:

1.  Warning: The video_player plugin doesn’t work on iOS simulators. You must test videos on real iOS devices.

2. For iOS, add the following to the Info.plist file found at <project root>/ios/Runner/Info.plist.

	<key>NSAppTransportSecurity</key>
    <dict>
      <key>NSAllowsArbitraryLoads</key>
      <true/>
    </dict>



# Usage

Import the package into your code 

```dart
import "package:story_view/story_view.dart";
```

Look inside `examples/example.dart` on how to use this library. You can copy
and paste the code into your `main.dart` and run to have a quick look.

## Basics
Use [`StoryView`](https://pub.dev/documentation/story_view/latest/story_view/StoryView-class.html) to add stories to screen or view heirarchy. `StoryView` requires a list of [`StoryItem`](https://pub.dev/documentation/story_view/latest/story_view/StoryItem-class.html), each of which describes the view to be displayed on each story page, duration and so forth. This gives you the freedom to customize each page of the story.

There are shorthands provided to create common pages. 

`StoryItem.text` is a shorthand to create a story page that displays only text.

`StoryItem.pageImage` creates a story item to display images with a caption.

`StoryItem.inlineImage` creates a story item that is intended to be displayed in a linear view hierarchy like `List`
or `Column`

`StoryItem.inlineGif` and `StoryItem.pageGif` works same as inline and page image but supports both animated GIFs and still images. The difference is that, animated GIFs get paused when a pause gesture is made.

`StoryItem.pageVideo` creates a page story item with video media. Just provide your video url and get going.

### Story controller, loaders and GIF support
While images load, it'll be a better experience to pause the stories until it's done. To achieve this effect, create a global instance of [`StoryController`](https://pub.dev/documentation/story_view/latest/story_controller/StoryController-class.html) and use the shorthand `StoryItem.pageGif` or `StoryItem.inlineGif` while passing the controller to it.

🍭 `StoryItem.pageGif` and `StoryItem.inlineGif` can also load non-animated graphic media like PNG, JPG, etc.


```dart
...
final controller = StoryController();

@override
Widget build(context) {
  List<StoryItem> storyItems = [
    StoryItem.text(...),
    StoryItem.pageImage(...),
    StoryItem.pageImage(...),
    StoryItem.pageGif(...,
      controller: controller,
      ...),
    StoryItem.pageVideo(
      ...,
      controller: controller,
    )
  ]; // your list of stories

  return StoryView(
    storyItems,
    controller: controller, // pass controller here too
    repeat: true, // should the stories be slid forever
    onStoryShow: (s) {notifyServer(s)}
  )
}
```

🍭 Now, tell your users some stories.
