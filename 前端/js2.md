# Javascript 2

[TOC]

<hr/>

### 1、一个精简的问题

```js
// 返回的数据结构为
{
    "errorCode": "200",
    "errorMsg": null,
    "data": {
        "activedProdList": [],
        "applyingProdList": [],
        "recommendProdList": [
            {
                "tppCode": "WDPHMART",
                "tppName": "万达普惠",
                "creditAmount": 50000,
                "interestRate": "0.06%~0.10%",
                "isWaitDraw": null,
                "isOverDate": null,
                "openStatusEnum": "UN_OPEN",
                "url": null
            },
            {
                "tppCode": "MSMART",
                "tppName": "马上消金",
                "creditAmount": 50000,
                "interestRate": "0.05%~0.10%",
                "isWaitDraw": null,
                "isOverDate": null,
                "openStatusEnum": "UN_OPEN",
                "url": null
            }
        ]
    }
}
```



```js

/**
     * 是否需要显示market
     * 只有当有借贷项目时才显示
     * @param {Boolean} flag 是否需要显示market
     * @param {Object} obj market接口返回的数据
     */
    isShowMarket(flag, obj) {
        if (!flag) return false;
        const values = Object.values(obj);
        const reducer = (accumulator, item) =>
            (accumulator + Array.isArray(item) ? item.length : 0);

        const num = Object.values(obj).reduce(reducer, 0);
        console.log(values, num);
        // return num > 0;
        return num > 0;
    }
```

要求：data里面数组长度大于0的时候返回true

出现的问题：运算符的优先级、隐式类型转换、箭头函数精简代码产生的问题