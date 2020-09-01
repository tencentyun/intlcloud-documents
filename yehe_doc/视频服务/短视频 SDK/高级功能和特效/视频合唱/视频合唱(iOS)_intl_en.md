This document describes how to implement basic duet features from scratch.
 
## Process Overview

1. Place two views on the page, one for playback, and the other for shoot.
2. Place a button and progress bar for shoot and progress display, respectively.
3. Stop shoot after the video in the same duration as that of the source video has been shot.
4. Compose the shot video with the source video side by side.
5. Preview the composed video.

## UI Construction
Create a project first. Open Xcode, select "File" > "New" > "Project", and name the project to create it. The project is named "Demo" in this example. To shoot a video, the camera and mic permissions are required. Add the following items to `Info`:
```
Privacy - Microphone Usage Description
Privacy - Camera Usage Description
```

You can enter desired values for the two items, such as "Shooting Video"

Configure a simple shoot page. Open `Main.storyboard`, drag two `UIView` objects into it, configure their width to 0.5 time of the `superview`, and set their aspect ratio to 16:9.
![](https://main.qcloudimg.com/raw/757835bb36355f7e702a364d9740eb1e.png)

Add the progress bar, bind the page to `IBOutlet` in `ViewController.m`, and set the button `IBAction`. As the preview page needs to be redirected to after shoot, a navigation controller is required. Click the "VC" icon in yellow, select "Editor" > "Embed In" in the menu, and click "Navigation Controller" to add a layer of "Navigation Controller" onto the "ViewController". At this point, the basic UI has been constructed.
![](https://main.qcloudimg.com/raw/cbdc197ae0ac5856413efb956dd5893d.png)


## Sample Code

The duet feature mainly uses three other features: playback, shoot, and composition of the shot and source videos, which correspond to the `TXVideoEditer`, `TXUGCRecord`, and `TXVideoJoiner` SDK classes, respectively.

The SDK license needs to be configured before this feature can be used. Open `AppDelegate.m` and add the following code to it:

```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [TXUGCBase setLicenceURL:@"<License URL>" key:@"<License key>"];
    return YES;
}
```

Here, you need to apply for the license parameters in the [UGSV Console](https://console.cloud.tencent.com/vod/license). Once submitted, your application will be generally approved very soon, and the relevant information will be displayed on the page.

1. First, implement the declaration and initialization.
    Open `ViewContorller.m`, import the SDK, and declare the instances of the three classes above. As video playback, shoot, and composition are all async operations here, you need to listen on their events by adding the declaration for implementing the three protocols: `TXVideoJoinerListener`, `TXUGCRecordListener`, and `TXVideoPreviewListener`. After the declaration is added, the code will be as follows:
    ```objective-c
    #import "ViewController.h"
    @import TXLiteAVSDK_UGC;

    @interface ViewController () <TXVideoJoinerListener, TXUGCRecordListener, TXVideoPreviewListener>
    {
        TXVideoEditer *_editor;
        TXUGCRecord   *_recorder;
        TXVideoJoiner *_joiner;

        TXVideoInfo    *_videoInfo;
        
        NSString       *_recordPath;
        NSString       *_resultPath;
    }

    @property (weak, nonatomic) IBOutlet UIView *cameraView;
    @property (weak, nonatomic) IBOutlet UIView *movieView;
    @property (weak, nonatomic) IBOutlet UIButton *recordButton;
    @property (weak, nonatomic) IBOutlet UIProgressView *progressView;

    - (IBAction)onTapButton:(UIButton *)sender;
    @end
    ```
    After preparing the member variables and API implementation declaration, initialize the member variables above in `viewDidLoad`.
    ```objective-c
    - (void)viewDidLoad {
        [super viewDidLoad];
        // Here, place a .mp4 video file or a .mov video shot on the phone in the project
        NSString *mp4Path = [[NSBundle mainBundle] pathForResource:@"demo" ofType:@"mp4"];
        _videoInfo = [TXVideoInfoReader getVideoInfo:mp4Path];
        TXAudioSampleRate audioSampleRate = AUDIO_SAMPLERATE_48000;
        if (_videoInfo.audioSampleRate == 8000) {
            audioSampleRate = AUDIO_SAMPLERATE_8000;
        }else if (_videoInfo.audioSampleRate == 16000){
            audioSampleRate = AUDIO_SAMPLERATE_16000;
        }else if (_videoInfo.audioSampleRate == 32000){
            audioSampleRate = AUDIO_SAMPLERATE_32000;
        }else if (_videoInfo.audioSampleRate == 44100){
            audioSampleRate = AUDIO_SAMPLERATE_44100;
        }else if (_videoInfo.audioSampleRate == 48000){
            audioSampleRate = AUDIO_SAMPLERATE_48000;
        }
        
        // Set the video storage path
        _recordPath = [NSTemporaryDirectory() stringByAppendingPathComponent:@"record.mp4"];
        _resultPath = [NSTemporaryDirectory() stringByAppendingPathComponent:@"result.mp4"];
         
       // Initialize the player
        TXPreviewParam *param = [[TXPreviewParam alloc] init];
        param.videoView = self.movieView;
        param.renderMode = RENDER_MODE_FILL_EDGE;
        _editor = [[TXVideoEditer alloc] initWithPreview:param];
        [_editor setVideoPath:mp4Path];
        _editor.previewDelegate = self;
        
        // Initialize the shoot parameters
        _recorder = [TXUGCRecord shareInstance];
        TXUGCCustomConfig *recordConfig = [[TXUGCCustomConfig alloc] init];
        recordConfig.videoResolution = VIDEO_RESOLUTION_720_1280;
        // The frame rates of the shot video and source video must be the same; otherwise, the audio and video may be out of sync
        // Note: the frame rate of the duet video obtained here is the average frame rate and may be a decimal, which needs to be rounded
        recordConfig.videoFPS = (int)(_videoInfo.fps + 0.5);
        // The audio sample rates of the shot video and source video must be the same; otherwise, the audio and video may be out of sync
        recordConfig.audioSampleRate = audioSampleRate;
        recordConfig.videoBitratePIN = 9600;
        recordConfig.maxDuration = _videoInfo.duration;
        _recorder.recordDelegate = self;
        
        // Enable camera preview
        [_recorder startCameraCustom:recordConfig preview:self.cameraView];
        
        // Compose videos
        _joiner = [[TXVideoJoiner alloc] initWithPreview:nil];
        _joiner.joinerDelegate = self;
        [_joiner setVideoPathList:@[_recordPath, mp4Path]];
    }
    ```
    
2. Next, implement the shoot feature. You only need to respond to the user click of the button to call the SDK method. For the sake of convenience, the button is reused here to display the current status, and the logic of displaying the progress is added to the progress bar.
    ```objective-c
    - (IBAction)onTapButton:(UIButton *)sender {
        [_editor startPlayFromTime:0 toTime:_videoInfo.duration];
        if ([_recorder startRecord:_recordPath coverPath:[_recordPath stringByAppendingString:@".png"]] != 0) {
            NSLog(@"Failed to start the camera");
        }
        [sender setTitle:@"Shooting" forState:UIControlStateNormal];
        sender.enabled = NO;
    }

    #pragma mark TXVideoPreviewListener
    -(void) onPreviewProgress:(CGFloat)time
    {
        self.progressView.progress = time / _videoInfo.duration;    
    }
    ```

3. After shoot, implement the composition. You need to specify the positions of the two videos in the output video. Here, the left and right positions are set.
    ```objective-c
    -(void)onRecordComplete:(TXUGCRecordResult*)result;
    {
        NSLog(@"Shoot is completed and composition is started");
        [self.recordButton setTitle:@"Composing..." forState:UIControlStateNormal];
        
        // Get the width and height of the shot video
        TXVideoInfo *videoInfo = [TXVideoInfoReader getVideoInfo:_recordPath];
        CGFloat width = videoInfo.width;
        CGFloat height = videoInfo.height;
        
        // Place the shot and source videos on the left and right, respectively
        CGRect recordScreen = CGRectMake(0, 0, width, height);
        CGRect playScreen = CGRectMake(width, 0, width, height);
        [_joiner setSplitScreenList:@[[NSValue valueWithCGRect:recordScreen],[NSValue valueWithCGRect:playScreen]] canvasWidth:width * 2 canvasHeight:height];
        [_joiner splitJoinVideo:VIDEO_COMPRESSED_720P videoOutputPath:_resultPath];
    }
    ```

4. Implement the delegation method of the composition progress to display the progress on the progress bar.   
    ```objective-c
    -(void) onJoinProgress:(float)progress
    {
        NSLog(@"Composing videos %d%%",(int)(progress * 100));
        self.progressView.progress = progress;
    }
    ```

5. Implement the delegation method of the composition completion and switch to the preview page.
    ```objective-c
    #pragma mark TXVideoJoinerListener
    -(void) onJoinComplete:(TXJoinerResult *)result
    {
        NSLog(@"Video composition completed");
        VideoPreviewController *controller = [[VideoPreviewController alloc] initWithVideoPath:_resultPath];
        [self.navigationController pushViewController:controller animated:YES];
    }
    ```

At this point, the implementation is completed. The code of the video preview `VideoPreviewController` mentioned above is as follows:
- `VideoPreviewController.h`

    ```objective-c
    #import <UIKit/UIKit.h>

    @interface VideoPreviewController : UIViewController
    - (instancetype)initWithVideoPath:(NSString *)path;
    @end
    ```

- `VideoPreviewController.m:`

    ```objective-c
    @import TXLiteAVSDK_UGC;

    @interface VideoPreviewController () <TXVideoPreviewListener>
    {
        TXVideoEditer *_editor;
    }
    @property (strong, nonatomic) NSString *videoPath;
    @end

    @implementation VideoPreviewController

    - (instancetype)initWithVideoPath:(NSString *)path {
        if (self = [super initWithNibName:nil bundle:nil]) {
            self.videoPath = path;
        }
        return self;
    }

    - (void)viewDidLoad {
        [super viewDidLoad];
        TXPreviewParam *param = [[TXPreviewParam alloc] init];
        param.videoView = self.view;
        param.renderMode = RENDER_MODE_FILL_EDGE;

        _editor = [[TXVideoEditer alloc] initWithPreview:param];
        _editor.previewDelegate = self;
        [_editor setVideoPath:self.videoPath];
        [_editor startPlayFromTime:0 toTime:[TXVideoInfoReader getVideoInfo:self.videoPath].duration];
    }

    -(void) onPreviewFinished
    {
        [_editor startPlayFromTime:0 toTime:[TXVideoInfoReader getVideoInfo:self.videoPath].duration];
    }
    @end
    ```

At this point, all basic duet features have been implemented. For the demo with more features, please see [Source Code of Full-Featured UGSV Application Demo](https://intl.cloud.tencent.com/document/product/1069/37914#.E5.85.A8.E5.8A.9F.E8.83.BD.E5.B0.8F.E8.A7.86.E9.A2.91-app.EF.BC.88demo.EF.BC.89.E6.BA.90.E4.BB.A3.E7.A0.81).
