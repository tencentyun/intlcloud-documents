## 简介
人脸识别基于腾讯领先的  AI 技术，帮助用户快速识别视频中的人脸信息，包括视频中的人物所在帧画面，以及人脸所在区域坐标等。用户可直接使用云点播公共人物库进行人脸识别，也支持用户管理并使用自定义人物库。云点播公共人物库涵盖电影、音乐、体育、学术等众多领域知名人物。
## 适用场景
媒体内容人脸识别已广泛应用于视频创作、检索、个性化推荐等场景，下面是一些例子。

<table>
    <tr>
        <th style="width:150px">
            场景               
        </th>
				<th>
           说明
        </th>
    </tr>
 <tr>
        <td>
            视频创作
        </td>
				<td>
            通过人脸识别技术，用户可以简单高效地从海量视频中找出自己所关注的目标人物在历史视频中出现的时间点、<br/>人脸所在画面区域以及持续时间，从而快速找出相关创作素材，提升创作效率。
        </td>
 </tr>
 <tr>
        <td>
            赛事回放
        </td>
				<td>
				体育比赛、游戏比赛视频对用户关注的人物打点，方便快速定位到相关的播放位置。也可识别出热点人物出现的位置，制作精彩时刻短片，或者将其出现的视频帧画面截取生成动图做成封面吸引点击。
        </td>
 </tr>
  <tr>
        <td>
            视频网站
        </td>
				<td>
            用户搜索人物名字，检索出相关的视频资源。也可根据用户设置的关注人物列表，自动推荐相关的视频资源。
        </td>
 </tr>
</table>



## 使用方式
人脸识别通过 [音视频内容识别](https://intl.cloud.tencent.com/document/product/266/33946) 里的**人脸识别**功能实现。具体使用步骤：
1. 准备 [音视频内容识别模板](https://intl.cloud.tencent.com/document/product/266/33946#.E9.9F.B3.E8.A7.86.E9.A2.91.E5.86.85.E5.AE.B9.E8.AF.86.E5.88.AB.E6.A8.A1.E6.9D.BF)。
您可直接使用 [预置音视频内容识别模板](https://intl.cloud.tencent.com/document/product/266/33932) 用于识别全部公共人物库的人物。
也可通过 [创建音视频内容识别模板](https://intl.cloud.tencent.com/document/product/266/37568) ，指定需要识别的指定的公共人物库标签和自定义人物库\*标签。人脸识别配置项（`FaceConfigure`），比如下面表示公共人物库只识别体育明星：
```
{
	"FaceConfigure": {
		"Switch": "ON",
		"DefaultLibraryLabelSet": ["sport"]
	}
}
```
回包得到模板 ID。
\* 自定义人物库通过 [AI 样本管理相关接口](https://intl.cloud.tencent.com/document/product/266/34110) **创建/修改/删除/获取素材样本**系列接口管理。

2. 发起人脸识别任务，使用步骤1. 的模板 ID，具体请参见 [任务发起](https://intl.cloud.tencent.com/document/product/266/33946#.E4.BB.BB.E5.8A.A1.E5.8F.91.E8.B5.B7)。
3. 获取人脸识别任务结果，具体请参见 [结果获取](https://intl.cloud.tencent.com/document/product/266/33946#.E7.BB.93.E6.9E.9C.E8.8E.B7.E5.8F.96)。
