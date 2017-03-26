# YoutubeSourceParserKit

[![Build Status](https://img.shields.io/travis/movielala/YoutubeSourceParserKit/master.svg)](https://travis-ci.org/movielala/YoutubeSourceParserKit)
![License](https://img.shields.io/badge/license-MIT-blue.svg)
[![Dependencies](https://img.shields.io/badge/dependencies-none-brightgreen.svg)](https://github.com/mobileplayer/mobileplayer-ios)
[![Ready](https://badge.waffle.io/movielala/YoutubeSourceParserKit.png?label=Ready&title=Ready)](https://waffle.io/movielala/YoutubeSourceParserKit)
[![StackOverflow](https://img.shields.io/badge/StackOverflow-Ask%20a%20question!-blue.svg)](http://stackoverflow.com/questions/ask?tags=YoutubeSourceParserKit+ios+swift)
[![CocoaPods](https://img.shields.io/cocoapods/v/YoutubeSourceParserKit.svg)](https://img.shields.io/cocoapods/v/YoutubeSourceParserKit.svg)
[![Join the chat at https://gitter.im/mobileplayer/mobileplayer-ios](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/movielala/YoutubeSourceParserKit)


YouTube Video Link Parser for Swift. Heavily inspried from hellozimi's repo [HCYoutubeParser](https://github.com/hellozimi/HCYoutubeParser)

## Introduction

__Requires iOS 8 or later and Xcode 7.0+__<br/>
Swift support uses dynamic frameworks and is therefore only supported on iOS 8.

## Installation

To install via CocoaPods add this line to your `Podfile`.

```
use_frameworks!

pod 'YoutubeSourceParserKit', :git => 'https://github.com/AkkeyLab/YoutubeSourceParserKit.git', :tag => '0.3.0'
```

Then, run the following command: `$ pod install`

## Usage

```swift
import YoutubeSourceParserKit

let testURL = NSURL(string: "https://www.youtube.com/watch?v=swZJwZeMesk")!
Youtube.h264videosWithYoutubeURL(testURL) { (videoInfo, error) -> Void in
  if let videoURLString = videoInfo?["url"] as? String,
    videoTitle = videoInfo?["title"] as? String {
      print("\(videoTitle)")
      print("\(videoURLString)")
  }
}
```

`videoInfo` output:

```json
{
    "title": "[Video Title]",
    "isStream": 0,
    "quality": "hd720",
    "itag": 22,
    "fallback_host": "tc.v20.cache2.googlevideo.com",
    "url": "http://[Source URL]"
}
```

## MPMoviePlayerController Usage

```swift
import UIKit
import YoutubeSourceParserKit
import MediaPlayer

class ViewController: UIViewController {

  let moviePlayer = MPMoviePlayerController()

  override func viewDidLoad() {
    super.viewDidLoad()
    moviePlayer.view.frame = view.frame
    view.addSubview(moviePlayer.view)
    moviePlayer.fullscreen = true
    let youtubeURL = NSURL(string: "https://www.youtube.com/watch?v=swZJwZeMesk")!
    playVideoWithYoutubeURL(youtubeURL)
  }

  func playVideoWithYoutubeURL(url: NSURL) {
    Youtube.h264videosWithYoutubeURL(url, completion: { (videoInfo, error) -> Void in
      if let
        videoURLString = videoInfo?["url"] as? String,
        videoTitle = videoInfo?["title"] as? String {
          self.moviePlayer.contentURL = NSURL(string: videoURLString)
      }
    })
  }
}
```

Warning:  
*This repo is for educational purposes.  This is not approved by the ToC of YouTube. Use at own risk.*
