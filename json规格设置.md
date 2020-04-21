# API JSON 一览  

## /api/course/:course_id/ddls  
```json
// 成功查询返回
{
    "success": true,
    "message": "Success.",
    "course": {
        "cid": "BH000001",
        "course_name": "软件工程"
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
            "cid": "BH000001",
            "ddl": {
                "ddl_id": 1,
                "ddl_time": {
                    "date": "2020-04-01",
                    "time": "23:55"
                },
                "notification_time": {
                    "date": "2020-03-31",
                    "time": "12:00",
                    "repeat": null
                },
                "notification_content": "交作业啦"
            }
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
            "cid": "BH000001",
            "ddl": {
                "ddl_id": 13,
                "ddl_time": {
                    "date": "2020-04-10",
                    "time": "23:55"
                },
                "notification_time": {
                    "date": "2020-04-09",
                    "time": "23:55",
                    "repeat": null
                },
                "notification_content": "交作业啦"                
            }
        }
    ] 
}

// 自己不属于这个课程的情况
{
    "success": true,
    "message": "You have no rights to access this course."    
}
```

## /api/user/:uid/courses
```json
// 成功查询返回
{
    "success": true,
    "message": "Success.",
    "user": {
        "uid": 1,
        "student_id": "17373001",
        "name": "北小航",
        "email": "0000001@qq.com"
    },
    "data": [ //这里的data是学生选课course的集合
        {
            "cid": "BH000001",
            "course_name": "软件工程",
            "accessibility": "r"
        },
        {
            "cid": "BH000002",
            "course_name": "工科数学分析",
            "accessibility": "wr" // w表示可写，课程负责人
        },
        {
            "cid": "BH000003",
            "course_name": "高级算法分析",
            "accessibility": "r"
        }
    ]
}
```

## /api/user/:uid/task/:tid
```json
// 成功查询返回
{
    "success": true,
    "message": "Success.",
    "user": {
        "uid": 1,
        "student_id": "17373001",
        "name": "北小航",
        "email": "0000001@qq.com"
   },
    "data": { //这里的data是单个task
        "tid": 27,
        "title": "团队博客——功能规格",
        "category": "homework",
        "content": "这是一篇团队博客",
        "useful_urls": [
            "www.edu.cnblogs.com/xxxxx",
            "www.github.com/BuaaRedSun/docs"
        ],
        "cid": "BH000001",
        "course_name": "软件工程",
        "ddl": {
            "ddl_id": 13,
            "ddl_time": {
                "date": "2020-04-10",
                "time": "23:55"
            },
            "notification_time": {
                "date": "2020-04-09",
                "time": "23:55",
                "repeat": null
            },
            "notification_content": "交作业啦"                
        }
    }
} 


//不存在的task和不属于自己的task的情况
{
    "success": false, 
    "message": "Task not exists."
}
```

## /api/user/:uid/tasks
```json
// 成功查询返回
{
    "success": true,
    "message": "Success.",
    "user": {
        "uid": 1,
        "student_id": "17373001",
        "name": "北小航",
        "email": "0000001@qq.com"
   }, 
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
            "cid": "BH000001",
            "ddl": {
                "ddl_id": 13,
                "ddl_time": {
                    "date": "2020-04-10",
                    "time": "23:55"
                },
                "notification_time": {
                    "date": "2020-04-09",
                    "time": "23:55",
                    "repeat": null
                },
                "notification_content": "交作业啦"                
            }
        },
        { // exam
            "tid": 35,
            "title": "工科数学分析期中考试",
            "category": "exam",
            "useful_urls": null,
            "cid": "BH0000102",
            "ddl": {
                "ddl_id": 30,
                "ddl_time": {
                    "date": "2020-06-22",
                    "time": "14:30"
                },
                "notification_time": {
                    "date": "2020-06-15",
                    "time": "08:00",
                    "repeat": "day"
                },
                "notification_content": "淑芬考试"                
            }
        },
        { // personal
            "tid": 42,
            "title": "拿快递",
            "category": "personal",
            "useful_urls": null,
            "cid": null,
            "ddl": {
                "ddl_id": 50,
                "ddl_time": {
                    "date": "2020-04-01",
                    "time": "17:30"
                },
                "notification_time": {
                    "date": "2020-04-11",
                    "time": "17:00",
                    "repeat": null
                },
                "notification_content": "东门顺丰快递"    
            }
        },
        { // meeting
            "tid": 77,
            "title": "志愿者例会",
            "category": "meeting",
            "useful_urls": [
                "www.bv2008.cn"
            ],
            "cid": null,
            "ddl": {
                "ddl_id": 70,
                "ddl_time": {
                    "date": "2020-04-01",
                    "time": "14:30"
                },
                "notification_time": {
                    "date": "2020-04-01",
                    "time": "14:00",
                    "repeat": "week"  
                },
                "notification_content": "汇报周进展"    
            }
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
        "created_at": "2020-03-15 16:22:37"
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


