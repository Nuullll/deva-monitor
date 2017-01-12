# Interface: AndroidServer <-> Server

## Request: Server -> AndroidServer

AndroidServer与Server接口初版，根据mobile SDK与具体情况随时修改。

| Command                                                                         | Description |
|:--------------------------------------------------------------------------------|:------------|
| <a href="#user-content-getCommand">getCommand(String cmd, int index)</a>        | 获取类命令       |
| <a href="#user-content-setCommand">setCommand(String cmd, JSONObject param)</a> | 设置类命令       |

* <a id="user-content-getCommand"> </a>`getCommand(String cmd, int index)`

    - 获取`0`号无人机的当前飞行高度

        **Request** *(from Server)*
        
        ```json
        {
            "commandType" : "getCommand",
            "command" : "getCurrentAltitude",
            "index" : 0
        }
        ```

        **Response** *(from AndroidServer)*

        ```json
        {
            "aircraft" : {
                "index" : 0,
                "currentAltitude" : 50.0
            },
            "errorCode" : "", 
            "errorMsg" : ""
        }
        ```

    - 获取`2`号无人机的当前位置（经度、纬度）

        **Request**

        ```json
        {
            "commandType" : "getCommand",
            "command" : "getCurrentPosition",
            "index" : 2
        }
        ```

        **Response**

        ```json
        {
            "aircraft" : {
                "index" : 2,
                "longitude" : 38.65777,
                "latitude" : 104.08296
            }, 
            "errorCode" : "",
            "errorMsg" : ""
        }
        ```

    - 获取`3`号无人机的速度

        **Request**

        ```json
        {
            "commandType" : "getCommand",
            "command" : "getVelocity",
            "index" : 3
        }
        ```

        **Response**

        ```json
        {
            "aircraft" : {
                "index" : 3,
                "velocityX" : 2.5,
                "velocityY" : 0.0,
                "velocityZ" : 0.0
            },
            "errorCode" : "",
            "errorMsg" : ""
        }
        ```

    - 获取`0`号无人机的机头指向

        **Request**

        ```json
        {
            "commandType" : "getCommand",
            "command" : "getHeadDirection",
            "index" : 0
        }
        ```

        **Response**

        ```json
        {
            "aircraft" : {
                "index" : 0,
                "orientationMode" : "DefaultAircraftHeading",
                "headDirection" : -20
            },
            "errorCode" : "",
            "errorMsg" : ""
        }
        ```

        `headDirection`的值为相对于`orientationMode`所指定坐标轴的值，以逆时针方向为正方向

    - 获取`0`号机电池信息

        **Request**

        ```json
        {
            "commandType" : "getCommand",
            "command" : "getBatteryStatus",
            "index" : 0
        }
        ```

        **Response**

        ```json
        {
            "aircraft" : {
                "index" : 0,
                "battery1" : 76,
                "battery1Temp" : 30,
                "battery2" : 76,
                "battery2Temp" : 30,
                "battery3" : 76,
                "battery3Temp" : 30,
                "battery4" : 76,
                "battery4Temp" : 30,
                "battery5" : 76,
                "battery5Temp" : 30,
                "battery6" : 76,
                "battery6Temp" : 30
            },
            "errorCode" : "",
            "errorMsg" : ""
        }
        ```

    - 获取`2`号机云台信息

        **Request**

        ```json
        {
            "commandType" : "getCommand",
            "command" : "getGimbalStatus",
            "index" : 0
        }
        ```

        **Response**

        ```json
        {
            "aircraft" : {
                "index" : 2, 
                "gimbal" : {
                    "batteryPercentage" : 80,
                    "attitude" : ...
                }
            },
            "errorCode" : "",
            "errorMsg" : ""
        }
        ```

    - 获取`0`号机全部信息

        **Request**

        ```json
        {
            "commandType" : "getCommand",
            "command" : "getAircraftStatus",
            "index" : 0
        }
        ```

        **Response**

        ```json
        {
            "aircraft" : {
                "index" : 0,
                ...
            },
            "errorCode" : "",
            "errorMsg" : ""
        }
        ```

    - 获取全部飞机信息

        **Request**

        ```json
        {
            "commandType" : "getCommand",
            "command" : "getAllAircraftsStatus",
        }
        ```

        **Response**

        ```json
        {
            "aircrafts" : 
            [
            {
                "aircraft" : {
                    "index" : 0,
                    ...
                }
            }, {
                "aircraft" : {
                    "index" : 1,
                    ...
                }
            }, {
                "aircraft" : {
                    "index" : 2,
                    ...
                }
            }, {
                "aircraft" : {
                    "index" : 3,
                    ...
                }
            }],
            "errorCode" : "", 
            "errorMsg" : ""
        }
        ```

* <a id="user-content-setCommand"> </a>`setCommand(String cmd, JSONObject param)`

    - 无人机`2`执行移动命令

        **Request**

        ```json
        {
            "commandType" : "setCommand",
            "command" : "moveToTarget",
            "param" : {
                "index" : 2,
                "targetX" : 5.0,
                "targetY" : 3.0,
                "targetZ" : -1.0,
                "velocity" : 1.0
            }
        }
        ```

        **Response**

        ```json
        {
            "aircraft" : {
                "index" : 2,
                "response" : "ACK"
            },
            "errorCode" : "",
            "errorMsg" : ""
        }
        ```

    - 设置无人机`2`号飞控信息更新延迟（ms）

        **Request**

        ```json
        {
            "commandType" : "setCommand",
            "command" : "setUpdateDelay",
            "param" : {
                "index" : 2,
                "updateDelay" : 200
            }
        }
        ```

        **Response**

        ```json
        {
            "aircraft" : {
                "index" : 2,
                "updateDelay" : 200
            },
            "errorCode" : "",
            "errorMsg" : ""
        }
        ```
