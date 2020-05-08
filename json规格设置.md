# API JSON 一览  

## /api/course/:course_id/tasks 
```json
// 成功查询返回
{
    "success": true,
    "message": "Success.",
    "course": {
        "cid": "1",
        "course_name": "软件工程",
        "teacher": "REN",
        "participant": [ //user-course表，在负责人创建课程task的时候直接call所有的participant
            "17373001",
            "17373002",
            "17373003"
        ]
    },
    "data": [ //这里的data是tasks的集合
        {
            "tid": 10,
            "title": "个人博客——热身", 
            "category": "homework", 
            "content": "这是一篇个人博客", 
            "useful_urls": [
                "www.edu.cnblogs.com/xxxxxx"
            ],
            "platform": "博客园",
            "cid": "1", //负责所属课程的唯一性，foreign key，不使用北航编号BHxxxx
            "course_name": "软件工程", //负责直接查看是什么课程
            "ddl": { //ddl现在是作为task的一个属性
                "ddl_id": 1,
                "ddl_time": "2020-04-01 23:55:00",
                "notification_alert": true, //新增提醒开关，逻辑为可以设置提醒的时间但是可以不提醒
                "notification_time": "2020-03-31 23:55:00", //创建新的事项时会根据类型category默认生成一个距离ddl_time多长时间的notification_time，同时notification_alert为true
                "notification_repeat": null,
                "notification_content": "交作业啦"
            },
            "created_at": "2020-03-20 15:33:20",
            "is_finished": false //事项的完成状态需要新开一张 user-task 表
        },
        {
            "tid": 27,
            "title": "团队博客——功能规格",
            "category": "homework",
            "content": "这是一篇团队博客",
            "useful_urls": [
                "www.edu.cnblogs.com/xxxxx",
                "www.github.com/BuaaRedSun/docs"
            ],
            "platform": "博客园",
            "cid": "1",
            "course_name": "软件工程",
            "ddl": {
                "ddl_id": 13,
                "ddl_time": "2020-04-10 23:55:00",
                "notification_alert": false,
                "notification_time": "2020-04-09 23:55:00",
                "notification_repeat": null,
                "notification_content": "交作业啦"                
            },
            "created_at": "2020-03-20 15:33:20",
            "participant": [
                "17373001",
                "17373002",
                "17373003"
            ],
            "is_finished": false
        }
    ] 
}

// 自己不属于这个课程的情况
{
    "success": false,
    "message": "You have no rights to access this course."    
}
```

## /api/user/:uid/courses
```json
// 成功查询返回
{
    "code":200,
    "success": true,
    "message": "Success.",
    "uid": 1,
    "data": [ //这里的data是学生选课course的集合
        {
            "course_name": "软件工程",
            "is_admin": false
        },
        {
            "course_name": "工科数学分析",
            "is_admin": true // 表示课程负责人
        },
        {
            "course_name": "高级算法分析",
            "is_admin": false
        }
    ]
}
```

## /api/user/:uid/task/:tid 创建和修改的传输粒度
### 查询返回json
```json
{
    "success": true,
    "message": "Success.",
    "uid": 1,
    "data": { //这里的data是单个task
        "tid": 27,
        "title": "团队博客——功能规格",
        "category": "homework",
        "content": "这是一篇团队博客",
        "useful_urls": [
            "www.edu.cnblogs.com/xxxxx",
            "www.github.com/BuaaRedSun/docs"
        ],
        "platform": "博客园",
        "cid": "1",
        "course_name": "软件工程",
        "ddl": {
            "ddl_id": 13,
            "ddl_time": "2020-04-10 23:55:00",
                "notification_alert": false,
            "notification_time": "2020-04-09 23:55:00",
            "notification_repeat": null,
            "notification_content": "交作业啦"                
        },
        "created_at": "2020-03-20 15:33:20",
        "participant": [ //单个task时内嵌到data内部
            "17373001",
            "17373002",
            "17373003"
        ],
        "is_finished": false
    }
} 
```

//不存在的task和不属于自己的task的情况
```json
{
    "success": false, 
    "message": "Task not exists."
}
```

### 创建和修改回传json
```json
{
    "uid": 1,
    "operation": "create / update", 
    "data": { //这里的data是单个task
        "tid": 27,
        "title": "团队博客——功能规格",
        "category": "homework",
        "content": "这是一篇团队博客",
        "useful_urls": [
            "www.edu.cnblogs.com/xxxxx",
            "www.github.com/BuaaRedSun/docs"
        ],
        "platform": "博客园",
        "cid": "1",
        "course_name": "软件工程",
        "ddl": {
            "ddl_id": 13,
            "ddl_time": "2020-04-10 23:55:00",
                "notification_alert": false,
            "notification_time": "2020-04-09 23:55:00",
            "notification_repeat": null,
            "notification_content": "交作业啦"                
        },
        "created_at": "2020-03-20 15:33:20",
        "participant": [ //单个task时内嵌到data内部
            "17373001",
            "17373002",
            "17373003"
        ],
        "is_finished": false
    }
} 
```



## /api/user/:uid/tasks
```json
// 成功查询返回
{
    "success": true,
    "message": "Success.",
    "uid": 1,
    "data": [ //这里的data是task集合
        { // homework
            "tid": 27,
            "title": "团队博客——功能规格",
            "category": "homework",
            "content": "这是一篇团队博客",
            "useful_urls": [
                "www.edu.cnblogs.com/xxxxx",
                "www.github.com/BuaaRedSun/docs"
            ],
            "platform": "博客园",
            "cid": "1",
            "course_name": "软件工程",
            "ddl": {
                "ddl_id": 13,
            "ddl_time": "2020-04-10 23:55:00",
                "notification_alert": false,
            "notification_time": "2020-04-09 23:55:00",
            "notification_repeat": null,
            "notification_content": "交作业啦"                
            },
            "created_at": "2020-03-20 15:33:20",
            "is_finished": false
        },
        { // exam
            "tid": 35,
            "title": "工科数学分析期中考试",
            "category": "exam",
            "useful_urls": [], //集合size=1即可，空值有点奇怪
            "platform": "教4-401",
            "cid": "3",
            "course_name": "工科数学分析",
            "ddl": {
                "ddl_id": 30,
                "ddl_time": "2020-06-12 14:30:00",
                "notification_alert": false,
                "notification_time": "2020-06-05 14:30:00",
                "notification_repeat": day,
                "notification_content": "淑芬考试",
            },
            "created_at": "2020-03-20 15:33:20",
            "is_finished": false
        },
        { // personal
            "tid": 42,
            "title": "拿快递",
            "category": "personal",
            "useful_urls": null,
            "platform": null,
            "cid": null,
            "course_name": null,
            "ddl": {
                "ddl_id": 50,
                "ddl_time": "2020-04-01 17:30:00",
                "notification_alert": true,
                "notification_time": "2020-04-11 17:00",
                "notification_repeat": null,
                "notification_content": "东门顺丰快递"    
            },
            "created_at": "2020-03-20 15:33:20",
            "is_finished": false
        },
        { // meeting
            "tid": 77,
            "title": "志愿者例会",
            "category": "meeting",
            "useful_urls": [
                "www.bv2008.cn"
            ],
            "platform": "志愿北京",
            "cid": "1",
            "course_name": null,
            "ddl": {
                "ddl_id": 70,
                "ddl_time": "2020-04-01 14:30:00",
                "notification_alert": true,
                "notification_time": "2020-04-01 14:00:00",
                "notification_repeat": "week",
                "notification_content": "汇报周进展"    
            },
            "created_at": "2020-03-20 15:33:20",
            "is_finished": false
        },
    ]
} 
```

## /api/user/:uid/info 
```json
// 成功查询返回
{
    "success": true,
    "message": "Success.",
    "user": {
        "uid": 1,
        "student_id": "17373001",
        "name": "北小航",
        "email": "0000001@qq.com",
        "created_at": "2020-03-15 16:22:37",

   }
}

{
    "success": false,
    "message": "User not exists."
}

{
    "success": false,
    "message": "You have no rights to access other user."
}
```


