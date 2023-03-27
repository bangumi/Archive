# Archive

定期导出 wiki 数据方便一些不需要实时数据的场景，顺便希望减少一些爬虫。

导出的数据为主键和原始wiki内容，即用户在/subject/1/edit或类似页面填写的原始内容。

会导出的数据包括：

条目：
- 条目 ID 
- 条目名
- 条目中文名
- 原始wiki字符串
- 条目平台，即剧场版/tv/anime等等
- 条目简介
- nsfw

人物：
- 人物 ID
- 人物名
- 人物原始wiki字符串
- 人物简介
- 人物职业

角色同人物

条目之间的关联，条目，人物，角色两两之间的关联。

章节:
- 章节 ID
- 章节名称，章节中文名
- 章节介绍
- 播出时间
- 播放时长
- 碟片数

每周三凌晨五点(GMT+8)更新。

导出的数据可以在 [releases](https://github.com/bangumi/Archive/releases/tag/archive) 下载

