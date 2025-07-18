# Archive

定期导出 wiki 数据方便一些不需要实时数据的场景，顺便希望减少一些爬虫。

导出的数据为主键和原始wiki内容，即用户在/subject/1/edit或类似页面填写的原始内容。

会导出的数据包括：

- 条目（Subject）：
  
  | **Key**           | **含义**                                                                 |
  |-------------------|--------------------------------------------------------------------------|
  | `id`              | 条目 ID                                                                  |
  | `type`            | 作品类型，1表示漫画，2表示动画，3表示音乐，4表示游戏，6表示三次元             |
  | `name`            | 条目名                                                                   |
  | `name_cn`         | 条目简体中文名                                                            |
  | `infobox`         | 条目原始 **wiki** 字符串                                                   |
  | `platform`        | 条目平台，即剧场版/TV/Anime等等                                            |
  | `summary`         | 条目简介                                                                  |
  | `nsfw`            | 是否为NSFW（Not Safe For Work，是否含有成人内容）                           |
  | `date`            | 发行日期                                                                  |
  | `favorite`        | 收藏状态（想看、看过、在看、搁置、抛弃）                                     |
  | `series`          | 是否为系列作品（单行本等）                                                  |

  2023-07-27 起会额外导出以下数据

  | **Key**           | **含义**                                                                 |
  |-------------------|--------------------------------------------------------------------------|
  | `tags`            | 标签（部分）                                                              |
  | `score`           | 评分                                                                     |
  | `score_details`   | 评分细节，包含各个评分级别的分布                                            |
  | `rank`            | 类别内排名                                                                |


  2024-08-30 起会正确处理条目名，中文名和原始wiki的html转义。

  
  2025-04-18 起会额外导出以下数据

  | **Key**           | **含义**                                                                 |
  |-------------------|--------------------------------------------------------------------------|
  | `meta_tags`       | 公共标签（由维基人管理）                                                   |


  
- 人物（Person）：
  | **Key**           | **含义**                                                                 |
  |-------------------|--------------------------------------------------------------------------|
  | `id`              | 人物 ID                                                                  |
  | `name`            | 人物名                                                                   |
  | `type`            | 类型，1表示个人，2表示公司，3表示组合                                      |
  | `career`          | 人物职业                                                                  |
  | `infobox`         | 原始 **wiki** 字符串                                                      |
  | `summary`         | 人物简介                                                                  |
  | `comments`        | 评论/吐槽数                                                               |
  | `collects`        | 收藏数                                                                   |

- 角色（Character）：
  | **Key**           | **含义**                                                                 |
  |-------------------|--------------------------------------------------------------------------|
  | `id`              | 角色 ID                                                                  |
  | `role`            | 角色类型，1表示角色，2表示机体，3表示组织，4...                             |
  | `name`            | 角色名                                                                   |
  | `infobox`         | 原始 **wiki** 字符串                                                      |
  | `summary`         | 角色简介                                                                  |
  | `comments`        | 评论/吐槽数                                                               |
  | `collects`        | 收藏数                                                                    |

- 章节（Episode）:
  | **Key**           | **含义**                                                                 |
  |-------------------|--------------------------------------------------------------------------|
  | `id`            | 章节 ID                                                                    |
  | `name`          | 章节名称                                                                    |
  | `name_cn`       | 章节简体中文名                                                               |
  | `description`   | 章节介绍                                                                    |
  | `airdate`       | 播出时间                                                                    |
  | `disc`          | 该章节存在于第几张光盘                                                       |
  | `duration`      | 播放时长                                                                    |
  | `subject_id`    | 作品 ID                                                                     |
  | `sort`          | 序话，该章节是第几集                                                         |
  | `type`          | 类型，0表示正篇，1表示特别篇，2表示OP，3表示ED，4表示Trailer，5表示MAD，6表示其他|

- 条目之间的关联（Subject-relations）：
  | **Key**              | **含义**                                                                 |
  |----------------------|--------------------------------------------------------------------------|
  | `subject_id`         | 作品 ID                                                                  |
  | `relation_type`      | 关联类型                                                                 |
  | `related_subject_id` | 关联作品ID                                                               |
  | `order`              | 关联排序                                                                 |

- 条目与角色的关联（Subject-characters）：
  | **Key**              | **含义**                                                                 |
  |----------------------|--------------------------------------------------------------------------|
  | `character_id`      | 角色 ID                                                                   |
  | `subject_id`        | 作品 ID                                                                   |
  | `type`              | 角色类型：1 主角，2 配角，3 客串                                            |
  | `order`             | 作品角色列表排序：按 (`type`, `order`) 排序，不保证 `order` 连续            |

- 条目与人物的关联（Subject-persons）：
  | **Key**              | **含义**                                                                 |
  |----------------------|--------------------------------------------------------------------------|
  | `person_id`          | 人物 ID                                                                  |
  | `subject_id`         | 作品 ID                                                                  |
  | `position`           | 担任职位                                                                 |

- 人物与角色的关联（Person-characters）：
  | **Key**              | **含义**                                                                 |
  |----------------------|--------------------------------------------------------------------------|
  | `person_id`          | 人物 ID                                                                  |
  | `subject_id`         | 条目 ID                                                                  |
  | `character_id`       | 对应条目中的角色 ID                                                       |
  | `summary`            | 概要                                                                     |

每周三凌晨五点(GMT+8)更新。

导出的数据可以在 [releases](https://github.com/bangumi/Archive/releases/tag/archive) 下载

relation, platform, staff 等常量对应关系的 yaml 文件见 [`bangumi/common`](https://github.com/bangumi/common)。

**wiki** 原始字符串的语法与解析方式，可参照 [`bangumi/wiki-parser-go`](https://github.com/bangumi/wiki-parser-go) [`bangumi/wiki-parser`](https://github.com/bangumi/wiki-parser) [`wiki-parser-py`](https://github.com/bangumi/wiki-parser-py) 与 [`bangumi/wiki-syntax-spec`](https://github.com/bangumi/wiki-syntax-spec) 。

## 获取最新的导出文件地址

请获取并解析 [./aux/latest.json](./aux/latest.json) 文件，该文件会在新数据上传之后更新。


