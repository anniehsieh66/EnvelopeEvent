# 紅包活動
---

# Summary

* [取得所有活動](#取得所有活動)
* [取得活動內容](#取得活動內容)
* [發送獎勵](#發送獎勵)

## 注意事項

- `需要提供 IP 讓我方加入白名單`
- `我方時區為 UTC-4`

##錯誤代碼

|Code|Description|
|--|--|
|0|成功|
|-1|未知錯誤|
|27|發放獎勵失敗|

## 取得所有活動

- `GET` `/marketing/api/events`

**Response**
```
{
    "code": 0,
    "result": [
        {
            "eventID": 1,
            "eventName": "測試活動1",
            "eventStatus": 2,
            "startTime": "2020-06-01T00:00:00",
            "endTime": "2020-08-30T00:00:00",
            "missionCondition": 5,
            "mission": 1
        },
        {
            "eventID": 1234,
            "eventName": "測試活動2",
            "eventStatus": 2,
            "startTime": "2020-06-01T09:00:00",
            "endTime": "2020-08-31T20:00:00",
            "missionCondition": 500,
            "mission": 2
        },
        {
            "eventID": 9527,
            "eventName": "測試9527",
            "eventStatus": 2,
            "startTime": "2020-06-10T12:00:00",
            "endTime": "2020-07-10T12:00:00",
            "missionCondition": 500,
            "mission": 2
        }
    ],
    "timestamp": "2020-07-15T23:55:53",
    "message": "Success"
}
```

**Result Data**

|Field|Value type|Description|
|--|--|--|
|eventID|Int|活動ID|
|eventName|String|活動名稱|
|eventStatus|Int|活動狀態 1: 開 2: 關|
|startTime|DateTime|開始時間|
|endTime|DateTime|結束時間|
|mission|Int|條件 1: 登入次數 2: 累計存款 3: 累計流水|
|missionCondition|Int|達成條件|

## 取得活動內容

- `GET` `/marketing/api/{ eventId }`

`GET` `/marketing/api/1234`

**Response**

```
{
  "code": 0,
  "result": {
    "eventID": 9527,
    "eventName": "測試9527",
    "eventStatus": 2,
    "startTime": "2020-06-10T12:00:00",
    "endTime": "2020-07-10T12:00:00",
    "missionCondition": 500,
    "mission": 2,
    "awards": [
      {
        "bonusID": 1974,
        "bonusName": "转运金_1688"
      },
      {
        "bonusID": 1987,
        "bonusName": "真人娱乐连赢_连续获胜18手_8888"
      }
    ],
    "blacklist": [
      {
        "blockType": 1,
        "blacklist": "2356"
      },
      {
        "blockType": 0,
        "blacklist": "foxtest001"
      }
    ]
  },
  "timestamp": "2020-07-16T01:27:44",
  "message": "Success"
}
```
**awards 紅利獎項**

|Field|Value type|Description|
|--|--|--|
|bonusID|Int|紅利ID|
|bonusName|String|紅利名稱|

**blacklist 排除名單**

|Field|Value type|Description|
|--|--|--|
|blockType|Int|排除類型 0: 主帳號 1: 推廣號|
|blacklist|String|排除帳號/推廣號|

## 發送獎勵

- `POST` `/marketing/api/events/award`

**Request Parameter**

|Field|Value type|Description|
|--|--|--|
|currencyId|Int|幣別，中國市場固定為2|
|mainAccountId|String|用戶主帳號|
|bonusId|String|紅利ID|

**Request**
```
{
    "currencyId": 2,
    "mainAccountId": "foxtest001",
    "bonusId": 8338
}
```

**Response**
```
// 成功時
{
  "code": 0,
  "result": "",
  "timestamp": "2020-07-16T01:36:03",
  "message": "Success"
}

// 失敗時
{
  "code": 27,
  "result": "",
  "timestamp": "2020-07-16T01:37:03",
  "message": "Backend_Bonus_SpecialBonus_Create Failed. (0.0)"
}
```
