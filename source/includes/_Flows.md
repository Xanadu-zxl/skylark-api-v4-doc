# Flows

## 新建流程（1）

```http
POST /api/v4/yaw/flows/27/journeys HTTP/1.1
Authorization: your_authorization

```

```http
HTTP/1.1 200 OK
Body中传入
{
	"assignment": {
		"response_attributes": {
			"entries_attributes": [
				{
					"field_id": 545,
					"value": "7-4-406"
				},
				{
					"field_id": 496,
					"value": "123"
				}
			]
		},
		"operation": "route"
	},
	"user_id": "1",
	"webhook": {
		"payload_url": "后端触发应用的地址（url）",
		"subscribed_events": [
			"JourneyStatusEvent"
		]
	}
}

{
	"assignment": {
		"id": 693,
		"status": "stashed",
		"category": "proposed",
		"read": true,
		"current_duration_threshold": null,
		"created_at": "2020-09-07T09:52:41.927+08:00",
		"updated_at": "2020-09-07T09:52:41.959+08:00",
		"after_submit_action": "default",
		"after_submit_redirect_url": null,
		"gid": "gid://skylark/YetAnotherWorkflow::Assignment/693",
		"pretty_current_duration_threshold": null,
		"journey": {
			"id": 290,
			"sn": "2720200907095241000019",
			"status": "stashed",
			"current_duration_threshold": null,
			"created_at": "2020-09-07T09:52:41.884+08:00",
			"updated_at": "2020-09-07T09:52:41.884+08:00",
			"gid": "gid://skylark/YetAnotherWorkflow::Journey/290",
			"pretty_current_duration_threshold": null,
			"response": {
				"id": 4491,
				"created_at": "2020-09-07T09:52:41.865+08:00",
				"entries": []
			},
			"user": {
				"id": 1,
				"name": "水映汀洲",
				"nickname": "坤",
				"phone": "18980807092",
				"identifier": "123456",
				"qq": "",
				"headimgurl": "http://thirdwx.qlogo.cn/mmopen/vi_32/uJ7wdTmBn87QFExPS17iam0BxXiakvKI8rv2G49VNFGEzIC5BRGxtjvwSyExjN8ulQql4FZcY6NvVeO6xMvK3Piag",
				"openid": "ouvMN1kWhKQuOFQEoZcmiOXt4Yjs",
				"imported_alias": "水映汀洲",
				"gid": "gid://skylark/User/1"
			}
		},
		"response": {
			"id": 4492,
			"created_at": "2020-09-07T09:52:41.904+08:00",
			"entries": [
				{
					"id": 62935,
					"field_id": 529,
					"option_id": null,
					"value": "2020-08-27",
					"choice_id": null,
					"value_id": null,
					"latitude": null,
					"longitude": null,
					"group_id": null,
					"detail_id": null
				},
				{
					"id": 62934,
					"field_id": 526,
					"option_id": null,
					"value": "5675",
					"choice_id": null,
					"value_id": null,
					"latitude": null,
					"longitude": null,
					"group_id": null,
					"detail_id": null
				}
			]
		}
	},
	"next_vertices": [
		{
			"id": 82,
			"name": "工作人员",
			"type": "YetAnotherWorkflow::Vertex::Normal",
			"metadata": {
				"position": {
					"x": 395,
					"y": 224.71875
				}
			},
			"operations": {
				"route": {
					"name": "选路",
					"enabled": true
				},
				"refuse": {
					"name": "回退",
					"enabled": true
				},
				"approve": {
					"name": "通过",
					"enabled": true
				},
				"comment": {
					"name": "处理意见",
					"enabled": true
				},
				"transfer": {
					"name": "转交",
					"enabled": true
				},
				"esignature": {
					"name": "电子签字",
					"enabled": false
				}
			},
			"settings": {
				"carbon_copy": {
					"enable_manual": false
				},
				"refuse_mode": 1,
				"assign_manually": false,
				"duration_threshold": {
					"value": null,
					"enable_delay": false,
					"business_time": {
						"final": "17:00",
						"initial": "09:00",
						"workday": true
					},
					"enable_manual": false,
					"enable_business_time": false
				},
				"distributed_equally": false
			},
			"graph_id": 28,
			"created_at": "2020-08-14T15:49:39.367+08:00",
			"updated_at": "2020-08-27T14:31:43.061+08:00",
			"gid": "gid://skylark/YetAnotherWorkflow::Vertex::Normal/82",
			"fields": []
		}
	],
	"next_graphs": [
		{
			"id": 28,
			"name": "主流程",
			"ancestry": null,
			"settings": {
				"visibility": "public",
				"duration_threshold": {
					"value": null,
					"enable_delay": false,
					"business_time": {
						"final": "17:00",
						"initial": "09:00",
						"workday": true
					},
					"enable_manual": false,
					"enable_business_time": false
				}
			},
			"metadata": {},
			"created_at": "2020-08-14T15:42:29.868+08:00",
			"updated_at": "2020-08-14T15:42:29.940+08:00",
			"gid": "gid://skylark/YetAnotherWorkflow::Graph/28"
		}
	]
}
```

`POST /api/v4/yaw/flows/27/journeys`

**Parameters**

| Name               | Type    | Description          | Comments           |
| ------------------ | ------- | -------------------- | ------------------ |
| id                 | integer | 流程 id              |                    |
| entries_attributes | array   | 每一项的值组成的数组 | 格式固定           |
| field_id           | integer | 每一项值的 ID        | --                 |
| value              | string  | 每一项的值           | --                 |
| operation          | string  | 流程发起的状态       | 固定值为：route    |
| user_id            | integer | 用户 id              | --                 |
| webhook            | object  | 监听流程状态         | --                 |
| payload_url        | strings | 流程通过的回调地址   | --                 |
| subscribed_events  | strings | 固定值               | JourneyStatusEvent |

## 新建流程确认（2）

```http
POST /api/v4/yaw/flows/27/journeys HTTP/1.1
Authorization: your_authorization

```

```http
HTTP/1.1 200 OK
Body中传入
{
	"assignment": {
		"response_attributes": {
			"entries_attributes": []
		},
		"operation": "propose",
		"next_vertex_id": '下一个节点 ID'
	},
	"user_id": "1",
	"webhook": {
		"payload_url": "后端触发应用的地址（url）",
		"subscribed_events": [
			"JourneyStatusEvent"
		]
	}
}
{
	"id": 693,
	"status": "processing",
	"category": "proposed",
	"read": true,
	"current_duration_threshold": null,
	"created_at": "2020-09-07T09:53:06.796+08:00",
	"updated_at": "2020-09-07T09:53:06.833+08:00",
	"after_submit_action": "default",
	"after_submit_redirect_url": null,
	"gid": "gid://skylark/YetAnotherWorkflow::Assignment/693",
	"pretty_current_duration_threshold": null,
	"journey": {
		"id": 290,
		"sn": "2720200907095241000019",
		"status": "processing",
		"current_duration_threshold": null,
		"created_at": "2020-09-07T09:53:06.796+08:00",
		"updated_at": "2020-09-07T09:53:06.796+08:00",
		"gid": "gid://skylark/YetAnotherWorkflow::Journey/290",
		"pretty_current_duration_threshold": null,
		"response": {
			"id": 4491,
			"created_at": "2020-09-07T09:52:41.865+08:00",
			"entries": []
		},
		"user": {
			"id": 1,
			"name": "水映汀洲",
			"nickname": "坤",
			"phone": "18980807092",
			"identifier": "123456",
			"qq": "",
			"headimgurl": "http://thirdwx.qlogo.cn/mmopen/vi_32/uJ7wdTmBn87QFExPS17iam0BxXiakvKI8rv2G49VNFGEzIC5BRGxtjvwSyExjN8ulQql4FZcY6NvVeO6xMvK3Piag",
			"openid": "ouvMN1kWhKQuOFQEoZcmiOXt4Yjs",
			"imported_alias": "水映汀洲",
			"gid": "gid://skylark/User/1"
		}
	},
	"response": {
		"id": 4492,
		"created_at": "2020-09-07T09:52:41.904+08:00",
		"entries": [
			{
				"id": 62935,
				"field_id": 529,
				"option_id": null,
				"value": "2020-08-27",
				"choice_id": null,
				"value_id": null,
				"latitude": null,
				"longitude": null,
				"group_id": null,
				"detail_id": null
			},
			{
				"id": 62934,
				"field_id": 526,
				"option_id": null,
				"value": "5675",
				"choice_id": null,
				"value_id": null,
				"latitude": null,
				"longitude": null,
				"group_id": null,
				"detail_id": null
			}
		]
	}
}
```

`POST /api/v4/yaw/flows/:id/journeys`

**Parameters**

| Name               | Type    | Description          | Comments           |
| ------------------ | ------- | -------------------- | ------------------ |
| id                 | integer | 流程 id              |                    |
| entries_attributes | array   | 每一项的值组成的数组 | 空数组             |
| operation          | string  | 流程发起的状态       | 固定值为：propose  |
| next_vertex_id     | integer | 下一个节点 ID        | 上一个接口返回     |
| user_id            | integer | 用户 id              | --                 |
| webhook            | object  | 监听流程状态         | --                 |
| payload_url        | strings | 流程通过的回调地址   | --                 |
| subscribed_events  | strings | 固定值               | JourneyStatusEvent |

## 获取单条流程数据（待开发）

```http
GET /api/v4/yaw/flows/#{flow_id}/journeys/#{id} HTTP/1.1
Authorization: your_authorization

```

```http
HTTP/1.1 200 OK

```

`GET /v4/responses/:dataID`

**Parameters**

| Name | Type    | Description | Comments |
| ---- | ------- | ----------- | -------- |
| id   | integer | 数据 id     |          |


## 获取组织流程

```http
GET /api/v4/yaw/flows/8 HTTP/1.1
Authorization: your_authorization

```

```http
HTTP/1.1 200 OK
{
  "id":8,
  "title":"简单流程",
  "fields":[
    {
      "id":38761,
      "title":"别填",
      "description":null
    },
    {
      "id":38806,
      "title":"明细清单",
      "description":null
    }
  ],
  "vertices":[
    {
      "id":78,
      "name":"开始节点",
      "type":"YetAnotherWorkflow::Vertex::Initial"
    },
    {
      "id":80,
      "name":"流程节点3",
      "type":"YetAnotherWorkflow::Vertex::Normal"
    },
    {
      "id":79,
      "name":"结束节点",
      "type":"YetAnotherWorkflow::Vertex::Final"
    },
    {
      "id":90,
      "name":"流程节点2",
      "type":"YetAnotherWorkflow::Vertex::Normal"
    },
    {
      "id":91,
      "name":"流程节点1",
      "type":"YetAnotherWorkflow::Vertex::Normal"
    },
    {
      "id":113,
      "name":"开始节点",
      "type":"YetAnotherWorkflow::Vertex::Initial"
    },
    {
      "id":114,
      "name":"结束节点",
      "type":"YetAnotherWorkflow::Vertex::Final"
    }
  ],
  "edges":[
    {
      "id":101,
      "from_vertex_id":78,
      "to_vertex_id":91
    },
    {
      "id":92,
      "from_vertex_id":80,
      "to_vertex_id":79
    },
    {
      "id":103,
      "from_vertex_id":90,
      "to_vertex_id":80
    },
    {
      "id":102,
      "from_vertex_id":91,
      "to_vertex_id":90
    }
  ]
}

```

`GET /api/v4/yaw/flows/:id`

**Parameters**

| Name | Type    | Description | Comments |
| ---- | ------- | ----------- | -------- |
| id   | integer | 流程 id     |

## 获取发起的流程列表

```http
GET /api/v4/yaw/flows/110/journeys HTTP/1.1
Authorization: your_authorization

```

```http
HTTP/1.1 200 OK
X-SLP-Current-Page: 1
X-SLP-Total-Pages: 29
X-SLP-Total-Count: 2
[
  {
    "id":110,
    "sn":"820180503184630000029",
    "status":"processing",
    "current_duration_threshold":null,
    "created_at":"2018-06-06T15:39:10.532+08:00",
    "updated_at":"2018-06-06T15:39:10.532+08:00",
    "current_vertex_id":91,
    "reviewer_vertex_ids":[
      78
    ],
    "response":{
      "id":548288,
      "cached_values":{
        "38761":{
          "value":[
            "123123123"
          ],
          "text_value":[
            "123123123"
          ],
          "exported_value":[
            "123123123"
          ]
        }
      }
    },
    "user":{
      "id":17013,
      "name":"aaaa",
      "identifier":"12345",
      "headimgurl":"/non-digested-assets/avatars/default.png"
    }
  },
  ...
]
```

`GET /api/v4/yaw/flows/:id/journeys`

**Parameters**

| Name | Type    | Description | Comments |
| ---- | ------- | ----------- | -------- |
| id   | integer | 流程 id     |

## 获取某条流程的所有 Moment

```http
GET /api/v4/yaw/journeys/392/moments
Authorization: your_authorization

```

```http
HTTP/1.1 200 OK
[
  {
    "id": 392,
    "status": "proposed",
    "comment": null,
    "esignature": "data:image/png;base64,something",
    "created_at": "2018-06-29T15:09:31.835+08:00",
    "updated_at": "2018-06-29T15:09:31.835+08:00",
    "vertex_id": 168,
    "user": {
      "id": 127057,
      "name": "cacao",
      "identifier": null,
      "headimgurl": "/non-digested-assets/avatars/default.png"
    }
  },
  {
    "id": 393,
    "status": "approved",
    "comment": "",
    "esignature": "data:image/png;base64,something",
    "created_at": "2018-06-29T15:09:46.297+08:00",
    "updated_at": "2018-06-29T15:09:46.297+08:00",
    "vertex_id": 170,
    "user": {
      "id": 127057,
      "name": "cacao",
      "identifier": null,
      "headimgurl": "/non-digested-assets/avatars/default.png"
    }
  }
]
```

**Parameters**

| Name | Type    | Description | Comments |
| ---- | ------- | ----------- | -------- |
| id   | integer | 流程 id     |
