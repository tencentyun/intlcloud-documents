Thank you for using [Tencent Cloud Game Multimedia Engine (GME) SDK](https://cloud.tencent.com/product/tmg?idx=1). This document describes how to select sound quality in GME SDK to make it easy for developers to access GME.

## Sound Quality Type
### If high definition quality is selected for voice chat, there are different audio types as detailed in the table below:

| Type     	| Meaning | Parameter | Volume Type | Scenario |
| ------------- |------------ | ---- |---- |---- |
| ITMG_ROOM_TYPE_FLUENCY			| Fluent 	|1| Speaker for call volume; headphone for media volume 				| Fluent sound quality with ultra low latency for real-time voice chat in games like FPS and MOBA	|							
| ITMG_ROOM_TYPE_STANDARD			| Standard 	|2| Speaker for call volume; headphone for media volume 					|Good sound quality with acceptable latency for real-time voice chat in casual games like Werewolf and board games 	|												
| ITMG_ROOM_TYPE_HIGHQUALITY		| High Definition	|3| Speaker for call volume; headphone for media volume 		| Super-high sound quality with relative high latency for scenarios demanding high sound quality such as music playback and online karaoke	|


### If general quality is selected for voice chat, there is only one audio type as detailed in the table below:

| Type     	| Meaning | Parameter | Volume Type | Scenario |
| ------------- |------------ | ---- |---- |---- |
| ITMG_ROOM_TYPE_FLUENCY			| Fluent 	|1| Speaker for call volume; headphone for media volume 				| Fluent sound quality with ultra-low latency for team voice in games like FPS and MOBA	|

If you have selected the general quality in Console, even though the API type you selected is  ITMG_ROOM_TYPE_STANDARD or ITMG_ROOM_TYPE_HIGHQUALITY when entering room, the actual sound quality is equivalent to ITMG_ROOM_TYPE_FLUENCY.
