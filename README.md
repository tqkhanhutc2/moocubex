# MOOCCubeX Data Overview
# COURSE
## entities/course.json

Each course includes multiple [resources](#resource). The fields are shown in the table below.

| field | description |
| ----- | ----------- |
| about | Course introduction |
| id | Course ID |
| field | List of the field of the course |
| name | Course name |
| prerequisites | Prerequisite knowledge description |
| resource | List of course [Resource](#resource) |

### Resource

Each resource is either a video or a set of [exercises](#exercise). The fields are shown in the table below.

| field | description |
| ----- | ----------- |
| resource_type | Resource type: either `video` (a [video](#video)) or `exercise` (a group of [exercises](#exercise)) |
| resource_id | ID of the resource |
| chapter | Chapter number |
| titles | A list of titles, including chapter titles, video titles, etc. There are up to 3 levels of headings. |

### Video

If `resource_type` is `video`, it is the video ID starting with `V_`, which is called `video_id` in this article.

Multiple `video_ids` correspond to one `ccid`, and `ccid` uniquely determines a video. These multiple `video_id` correspond to the display of the same `ccid` video at different start times (for example, spring 2018/fall 2020, etc.).
The correspondence between `video_id` and `ccid` can be found in [`relations/video_id-ccid.txt`](#relations/video_id-ccid.txt).

The subtitles of the video can be found in `entities/video.json` through the `ccid`.

### Exercise

Each set of exercises (`exercise`) corresponds to multiple questions ([`problem`](#entitiesproblemjson)). The specific correspondence can be found in `relations/exercise-problem.json` for each `exercise`
Corresponding `problem_id`.

## entities/video.json

The content of the video, its course, chapter and order can be found in [course.json](#resource).

| field | description |
| ----- | ----------- |
| ccid | Unique id of the video |
| name | The name of the video |
| start | Array, the start time of each sentence of the video subtitle |
| end | Array, the time when each sentence of the video subtitle ends |
| text | Array, subtitles of each sentence of the video |

## entities/problem.json

The specific content of [exercise](#exercise) included in the course. Note that each group of exercises ([`exercise`](#exercise)) corresponds to multiple questions ([`problem`](#entitiesproblemjson)). The fields are shown in the table below.

| field | description |
| ----- | ----------- |
| id | Problem ID, starting with `Pm_` |
| exercise_id | Exercise ID, starting with `Ex_` |
| language | The description language of the problem, Chinese/English |
| title | Title of the exercise |
| content | Description of the problem |
| option | Problem option |
| answer | The answer to the question |
| score | The score of the question |
| type | Question options |
| typetext | Question options |
| location | Chapter location of the problem |
| context_id | Array, leaf_id related to the problem |

## entities/school.json

| field | description |
| ----- | ----------- |
| id | School ID, starting with `S_` |
| name | Chinese name of the school |
| name_en | English name of the school |
| sign | The initials of the school's English name |
| about | Introduction |
| motto | School motto |

## entities/teacher.json

| field | description |
| ----- | ----------- |
| id | Teacher ID, starting with `T_` |
| name | Chinese name of the teacher |
| name_en | English name of the teacher |
| about | Teacher profile |
| job_title | job title |
| org_name | affiliation |

## relations/course-field.json

The fields of manually marked courses come from 88 fields in the "Catalogue of Disciplines and Specialties for Granting Doctoral Degrees, Master Degrees and Training Postgraduates" issued by the Ministry of Education in 1997. Each course may belong to multiple fields.

The fields are shown in the table below.

| field | description |
| ----- | ----------- |
| course_id | Course ID |
| course_name | Course name |
| field | Manually labeled field list |

## relations/course-school.txt

[Course](#entitiescoursejson)'s start [School](#entitiesschooljson). The format is `{course ID}\t{school ID}`.

## relations/course-teacher.txt

[Course](#entitiescoursejson)'s start [Teacher](#entitiesteacherjson). The format is `{course ID}\t{teacher ID}`.

## relations/exercise-problem.txt

A set of [problems](#entitiesproblemjson) contained in [exercise](#exercise). The format is `{exercise ID}\t{question ID}`.

## relations/video_id-ccid.txt

[Video ID](#video) and [ccid](#video) correspondence table. The format is `{Video ID}\t{ccid}`.
# CONCEPT
## entities/concept.json

Course concept.

| field | description |
| ----- | ----------- |
| id | Concept ID, the format is `K_{concept name}_{field}` |
| name | Concept name, guaranteed to be the same as the concept name in ID |
| context | The context in which the concept appears in [part of Wiki/Baidu Encyclopedia, Zhihu Q&A](#entitiesotherjson) (50 characters before and after). This string is guaranteed to contain the concept name. |

Bonus file: Raw concepts extracted from video captions by NER model without refinement: [entities/all_video_ner_ccid.json](https://lfs.aminer.cn/misc/moocdata/data/mooccube2/entities/all_video_ner_ccid.json)(158M)

## entities/other.json

Related materials collected outside the course, including Wikipedia, Baidu Baike, and some Zhihu Q&A. The fields are shown in the table below.

| field | description |
| ----- | ----------- |
| id | Data ID, meaningless |
| concept | The concept on which this information was collected |
| type | Data source, the value is one of `["zhihu", "baike", "wiki"]` |
| content | Data content |

## entities/paper.json

Concept-related papers. The fields are shown in the table below.

| field | description |
| ----- | ----------- |
| id | Paper ID, meaningless |
| concept | association [concept](#entitiesconceptjson)ID |
| abstract | Abstract of the paper |
| authors | The object of the author of the paper, including the author ID and name |
| doi | [DOI logo](https://www.doi.org/) |
| lang | Paper language, `en` is English, `zh` is Chinese |
| pages | Number of paper pages |
| num_citation | Number of citations as of 2020 |
| score | The score of the relevance between the paper and the concept, the higher the more similar |
| sourcetype | The source of the paper, all of which are currently `publication` |
| title | Paper Title |
| venue | Published conferences or journals |
| urls | List of paper URLs |
| year | Paper publication year |

## relations/concept-other.txt

[Concept](#entitiesconceptjson) related to [extracurricular resources](#entitiesotherjson). The format is `{concept ID}\t{resource ID}`.

## relations/concept-paper.txt

[Concept](#entitiesconceptjson) related [thesis](#entitiespaperjson). The format is `{concept ID}\t{paper ID}`.

## relations/concept-problem.txt

[Concept](#entitiesconceptjson) related [problem](./course-cn.md#entitiesproblemjson). The format is `{Concept ID}\t{Question ID}`.

## relations/concept-video.txt

[Concept](#entitiesconceptjson) related [video](./course-cn.md#entitiesvideojson). The format is `{concept ID}\t{ccid}`.

## relations/concept-comment.txt

[Concept](#entitiesconceptjson)Related users[Comments](./user-cn.md#entitiescommentjson). The format is `{concept ID}\t{review ID}`.

## relations/concept-problem.txt

[Concept](#entitiesconceptjson)[problem](./course-cn.md#problem) in related course exercises. The format is `{Concept ID}\t{Question ID}`.

# PREREQUISITES

## prerequisites/cs.json

The annotation and prediction of concepts in the computer field have been revised successively.

| field | description |
| ----- | ----------- |
| c1 | Prerequisite Concept |
| c2 | Post-repair concept |
| ground_truth | Whether there is a sequential repair relationship, `1` means yes, `0` means none |
| text_predict | Predicted results using text features |
| graph_predict | Prediction confidence obtained using graph features |

## prerequisites/math.json

Marking and prediction of concepts in the field of mathematics. The domain and its description are the same as [Computer Domain](#prerequisites/cs.json).

## prerequisites/psy.json

Annotation and prediction of concepts in the field of psychology. The domain and its description are the same as [Computer Domain](#prerequisites/cs.json).

# USER
## entities/user.json

| field | description |
| ----- | ----------- |
| id | User ID, starting with `U_` |
| name | Name |
| gender | gender |
| school | school |
| year_of_birth | Birth year and month |
| course_order | Array, selected courses |
| enroll_time | Array, course selection time corresponds to `course_order` |

## entities/comment.json

[Comment](#comment) of course [resource](./course-cn.md#resource). Each piece of data is a [comment](#comment) of a user to a [resource](./course-cn.md#resource). The fields are shown in the table below.

| field | description |
| ----- | ----------- |
| id | Comment ID, starting with `Cm_` |
| user_id | ID of the user who made the comment, starting with `U_` |
| text | Comment content |
| create_time | Comment time |

## entities/reply.json

| field | description |
| ----- | ----------- |
| id | Reply ID, starting with `Rp_` |
| user_id | User ID, starting with `U_` |
| text | Reply content |
| create_time | Reply time |

### Comment

Each [resource](./course-cn.md#resource) can have multiple comments, each comment is a user’s comment on the resource, which can be found in `relations/resource-comment.json`. `video_id` or `Ex_` at the beginning of V_`
The `exercise_id` at the beginning finds the `comment_id` of the corresponding comment. The specific content of the comment can be found in `entities/comment.json` according to the `comment_id`.

## relations/course-comment.txt

[Course](./course-cn.md#entitiescoursejson) related [user comments](#comment). The format is `{course ID}\t{review ID}`.

## relations/user-comment.txt

[Comment](#entitiescommentjson) of [User](#entitiesuserjson). The format is `{User ID}\t{Comment ID}`.

## relations/user-reply.txt

[User](#entitiesuserjson)’s [Comment Reply](#entitiesreplyjson). The format is `{User ID}\t{Reply ID}`.

## relations/comment-reply.txt

[Concept](./concept-cn.md#entitiesconceptjson) related [comment reply](#entitiesreplyjson). The format is `{concept ID}\t{reply ID}`.

A link table of comments sent by users and comments back.

## relations/user-problem.json

| field | description |
| ----- | ----------- |
| log_id | ID of the user's question record, combined with a unique key of `user_id` and `problem_id` |
| user_id | User ID, starting with `U_` |
| problem_id | Problem ID, starting with `Pm_` |
| is_correct | Is the question correct |
| attempts | Number of attempted questions |
| score | score |
| submit_time | Question time |## relations/user-video.json

## relations/user-video.json

| field | description |
| ----- | ----------- |
| user_id | User ID, starting with `U_` |
| seq | Array, the sequence of the user watching the video, each object in the array is the time sequence of the user watching a certain video, including the time of watching the video, the start and end time of the video, and the speed of watching the video, etc. |

## relations/user-xiaomu.json

| field | description |
| ----- | ----------- |
| user_id | User ID, starting with `U_` |
| question_type | User question category |
| question | Questions asked by users |

