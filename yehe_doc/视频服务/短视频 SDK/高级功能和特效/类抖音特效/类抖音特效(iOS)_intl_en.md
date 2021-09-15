## Special Effect Filter
You can add multiple special effect filters for your videos. Currently, 11 filters are supported, all of which allow you to set the start and end time for display in the video. If multiple filters are set at the same point in time, the SDK will display the last set one.

You can set a special effect as follows:

```
- (void) startEffect:(TXEffectType)type  startTime:(float)startTime;
- (void) stopEffect:(TXEffectType)type  endTime:(float)endTime;

// The special effect type (`type` parameter) is defined in the `TXEffectType` constant:
typedef  NS_ENUM(NSInteger,TXEffectType)
{
    TXEffectType_ROCK_LIGHT,  // Dynamic light-wave
    TXEffectType_DARK_DRAEM,  // Dark dream
    TXEffectType_SOUL_OUT,    // Soul out
    TXEffectType_SCREEN_SPLIT,// Screen split
    TXEffectType_WIN_SHADOW,  // Window blinds
    TXEffectType_GHOST_SHADOW,// Ghost shadow
    TXEffectType_PHANTOM,     // Phantom
    TXEffectType_GHOST,       // Ghost
    TXEffectType_LIGHTNING,   // Lightening
    TXEffectType_MIRROR,      // Mirror
    TXEffectType_ILLUSION,    // Illusion
};

- (void) deleteLastEffect;
- (void) deleteAllEffect;
```
You can call `deleteLastEffect()` to delete the last set special effect filter.  
You can call `deleteAllEffect()` to delete all set special effect filters:

Demo:
Use the first special effect filter between the first and second seconds, use the second special effect filter between the third and fourth seconds, and delete the special effect filter set between the third and fourth seconds:

```
// Use the first special effect filter between the first and second seconds
[_ugcEdit startEffect:TXEffectType_SOUL_OUT startTime:1.0];
[_ugcEdit stopEffect:TXEffectType_SOUL_OUT startTime:2.0)];
// Use the second special effect filter between the third and fourth seconds
[_ugcEdit startEffect:TXEffectType_SPLIT_SCREEN startTime:3.0];
[_ugcEdit stopEffect:TXEffectType_SPLIT_SCREEN startTime:4.0];
// Delete the special effect filter set between the third and fourth seconds
[_ugcEdit deleteLastEffect];
```
## Slow/Fast Motions
You can change the playback speed of multiple video segments by setting slow/fast playback as follows:

```
- (void) setSpeedList:(NSArray *)speedList;

// The `TXSpeed` parameters are as follows:
@interface TXSpeed: NSObject
@property (nonatomic, assign) CGFloat               startTime;      // Speed change start time in s
@property (nonatomic, assign) CGFloat               endTime;        // Speed change end time in s
@property (nonatomic, assign) TXSpeedLevel          speedLevel;     // Speed change level
@end

Currently, multiple speed change levels are supported, which are defined in the `TXSpeedLevel` constant:
typedef NS_ENUM(NSInteger, TXSpeedLevel) {
    SPEED_LEVEL_SLOWEST,       // Ultra-slow
    SPEED_LEVEL_SLOW,          // Slow
    SPEED_LEVEL_NOMAL,         // Normal
    SPEED_LEVEL_FAST,          // Fast
    SPEED_LEVEL_FASTEST,       // Ultra-fast
};
```
Demo:

```
// The SDK supports speed change of multiple video segments. This demo only shows slow playback of one video segment.
  TXSpeed *speed =[[TXSpeed alloc] init];
  speed.startTime = 1.0;
  speed.endTime = 3.0;
  speed.speedLevel = SPEED_LEVEL_SLOW;
  [_ugcEdit setSpeedList:@[speed]];
```
## Reverse Playback
You can reverse a video as follows:

```
- (void) setReverse:(BOOL)isReverse;
```
Demo:

```
[_ugcEdit setReverse:YES];
```

## Video Segment Loop
You can loop a video segment, but the audio will not be looped.  
Set the video segment for loop as follows: 

```
- (void) setRepeatPlay:(NSArray *)repeatList;

// The `TXRepeat` parameters are as follows:
@interface TXRepeat: NSObject
@property (nonatomic, assign) CGFloat               startTime;      // Loop start time in s
@property (nonatomic, assign) CGFloat               endTime;        // Loop end time in s
@property (nonatomic, assign) int                   repeatTimes;    // Number of repeats
@end
```

Demo:

```
TXRepeat *repeat = [[TXRepeat alloc] init];
repeat.startTime = 1.0;  
repeat.endTime = 3.0;
repeat.repeatTimes = 3;  // Number of repeats
[_ugcEdit setRepeatPlay:@[repeat]];
```
