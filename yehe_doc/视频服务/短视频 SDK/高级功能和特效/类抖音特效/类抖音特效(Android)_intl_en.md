## Special Effect Filter 
You can add multiple special effect filters for your videos. Currently, 11 filters are supported, all of which allow you to set the start and end time for display in the video. If multiple filters are set at the same point in time, the SDK will display the last set one.

Set the special effect filter:
```
/**
  * Set the start time of the special effect filter
   * @param type   Special effect filter type 
   * @param startTime   Start time of special effect filter in ms
   */
public void startEffect(int type, long startTime);
/**
  * Set the end time of the special effect filter
  * @param type   Special effect filter type
  * @param endTime   End time of special effect filter in ms
*/
public void stopEffect(int type, long endTime);
```
Parameter description: @param type: special effect filter type, which is defined in the `TXVideoEditConstants` constant:
``` 
public static final int TXEffectType_SOUL_OUT = 0;                    // Filter 1
public static final int TXEffectType_SPLIT_SCREEN = 1;                // Filter 2
public static final int TXEffectType_DARK_DRAEM = 2;                  // Filter 3
public static final int TXEffectType_ROCK_LIGHT = 3;                  // Filter 4
public static final int TXEffectType_WIN_SHADDOW = 4;                 // Filter 5
public static final int TXEffectType_GHOST_SHADDOW = 5;               // Filter 6
public static final int TXEffectType_PHANTOM_SHADDOW = 6;             // Filter 7
public static final int TXEffectType_GHOST = 7;                       // Filter 8
public static final int TXEffectType_LIGHTNING = 8;                   // Filter 9
public static final int TXEffectType_MIRROR = 9;                      // Filter 10
public static final int TXEffectType_ILLUSION = 10;                   // Filter 11
```
Delete the last set special effect filter:
``` 
public void deleteLastEffect();
```
Delete all set special effect filters:
``` 
public void deleteAllEffect();
```

Below is a complete sample:
Use the first special effect filter between the first and second seconds, use the second special effect filter between the third and fourth seconds, and delete the special effect filter set between the third and fourth seconds:

```
// Use the first special effect filter between the first and second seconds
mTXVideoEditer.startEffect(TXVideoEditConstants.TXEffectType_SOUL_OUT, 1000);
mTXVideoEditer.stopEffect(TXVideoEditConstants.TXEffectType_SOUL_OUT, 2000);
// Use the second special effect filter between the third and fourth seconds
mTXVideoEditer.startEffect(TXVideoEditConstants.TXEffectType_SPLIT_SCREEN, 3000);
mTXVideoEditer.stopEffect(TXVideoEditConstants.TXEffectType_SPLIT_SCREEN, 4000);
// Delete the special effect filter set between the third and fourth seconds
mTXVideoEditer.deleteLastEffect();
```
## Slow/Fast Motions
You can change the playback speed of multiple video segments by setting slow/fast playback as follows:

```
public void setSpeedList(List speedList);

// The `TXSpeed` parameters are as follows:
public final static class TXSpeed {
    public int speedLevel;                                    // Speed change level
    public long startTime;                                    // Start time
    public long endTime;                                      // End time
}

// Currently, multiple speed change levels are supported, which are defined in the `TXVideoEditConstants` constant:
SPEED_LEVEL_SLOWEST   - Ultra-slow
SPEED_LEVEL_SLOW   - Slow
SPEED_LEVEL_NORMAL   - Normal
SPEED_LEVEL_FAST   - Fast
SPEED_LEVEL_FASTEST   - Ultra-fast
```

Below is a complete sample:
```
List<TXVideoEditConstants.TXSpeed> list = new ArrayList<>();
TXVideoEditConstants.TXSpeed speed1 = new TXVideoEditConstants.TXSpeed();
speed1.startTime = 0;                                               
speed1.endTime = 1000;
speed1.speedLevel = TXVideoEditConstants.SPEED_LEVEL_SLOW;                         // Slow
list.add(speed1);

TXVideoEditConstants.TXSpeed speed2 = new TXVideoEditConstants.TXSpeed();
speed2.startTime = 1000;                                           
speed2.endTime = 2000;
speed2.speedLevel = TXVideoEditConstants.SPEED_LEVEL_SLOWEST;                      // Ultra-slow
list.add(speed2);

TXVideoEditConstants.TXSpeed speed3 = new TXVideoEditConstants.TXSpeed();
speed3.startTime = 2000;                                      
speed3.endTime = 3000;
speed3.speedLevel = TXVideoEditConstants.SPEED_LEVEL_SLOW;                          // Slow
list.add(speed3);

mTXVideoEditer.setSpeedList(list);
```

## Reverse Playback
You can reverse video playback. Specifically, you can call **`setReverse(true)`**/**`setReverse(false)`** to start/stop reverse playback.
>!The legacy version of **setTXVideoReverseListener()** (below SDK 4.5) needs to be manually called for the first listening, while the new version can take effect without being called.

Demo:
```
mTXVideoEditer.setTXVideoReverseListener(mTxVideoReverseListener);
mTXVideoEditer.setReverse(true);
```

## Video Segment Loop
You can loop a video segment, but the audio will not be looped. Currently, Android supports loop of only one video segment thrice.
You can call **`setRepeatPlay(null)`** to cancel the video segment loop set previously.

Set the video segment for loop as follows:
```
public void setRepeatPlay(List repeatList);

// The `TXRepeat` parameters are as follows:
public final static class TXRepeat {
    public long startTime;              // Loop start time in ms
    public long endTime;                // Loop end time in ms
    public int  repeatTimes;            // Number of repeats
}
```

Demo:
```
long currentPts = mVideoProgressController.getCurrentTimeMs();

List repeatList = new ArrayList<>();
TXVideoEditConstants.TXRepeat repeat = new TXVideoEditConstants.TXRepeat();
repeat.startTime = currentPts;
repeat.endTime = currentPts + DEAULT_DURATION_MS;
repeat.repeatTimes = 3;  // Currently, a video segment can be repeated only for thrice.
repeatList.add(repeat);  // Currently, only one video segment can be looped.
mTXVideoEditer.setRepeatPlay(repeatList);
```
