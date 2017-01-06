# Interface: AndroidServer <-> Server

## Request: Server -> AndroidServer

AndroidServer与Server接口初版，根据mobile SDK与具体情况随时修改。

| Command                                                                                                                                           | Description           |
|:--------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------|
| <a href="#user-content-getCurrentAltitude">getCurrentAltitude(int index)</a>                                                                      | 获取指定无人机当前的飞行高度        |
| <a href="#user-content-getCurrentPosition">getCurrentPosition(int index)</a>                                                                      | 获取指定无人机当前的经纬度         |
| <a href="#user-content-getVelocity">getVelocity(int index)</a>                                                                                    | 获取指定无人机当前的飞行速度，需给定坐标系 |
| <a href="#user-content-getHeadDirection">getHeadDirection(int index)</a>                                                                          | 获取指定无人机当前的机头方向        |
| <a href="#user-content-getBatteryStatus">getBatteryStatus(int index)</a>                                                                          | 获取指定无人机当前的电池状态        |
| <a href="#user-content-getGimbalStatus">getGimbalStatus(int index)</a>                                                                            | 获取指定无人机当前的云台状态        |
| <a href="#user-content-getAllAircraftsStatus">getAllAircraftsStatus()</a>                                                                         | 获取所有无人机的当前状态参数        |
| <a href="#user-content-moveToTarget">moveToTarget(int index, int coordinateMode, float targetX, float targetY, float targetZ, float velocity)</a> | 控制指定无人机飞向目标           |

* <a id="user-content-getCurrentAltitude"> </a>`getCurrentAltitude(int index)`

    获取`0`号无人机的当前飞行高度

    **Request** *(from Server)*
    
    ```json
    {
        "getCurrentAltitude" : {
            "index" : 0
        }
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

* <a id="user-content-getCurrentPosition"> </a>`getCurrentPosition(int index)`

    获取`2`号无人机的当前位置（经度、纬度）

    **Request**

    ```json
    {
        "getCurrentPosition" : {
            "index" : 2
        }
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

* <a id="user-content-getVelocity"> </a>`getVelocity(int index)`

    **Request**

    ```json
    {
        "getVelocity" : {
            "index" : 3
        }
    }
    ```

    **Response**

    ```json
    {
        "aircraft" : {
            "index" : 3,
            "coordinateMode" : ...,
            "velocityX" : 2.5,
            "velocityY" : 0.0,
            "velocityZ" : 0.0
        },
        "errorCode" : "",
        "errorMsg" : ""
    }
    ```

    `coordinateMode`指定参考坐标系，以便显示端确定x, y, z轴指向

* <a id="user-content-getHeadDirection"> </a>`getHeadDirection(int index)`

    **Request**

    ```json
    {
        "getHeadDirection" : {
            "index" : 0
        }
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

* <a id="user-content-getBatteryStatus"> </a>`getBatteryStatus(int index)`

    **Request**

    ```json
    {
        "getBatteryStatus" : {
            "index" : 0
        }
    }
    ```

    **Response**

    ```json
    {
        "aircraft" : {
            "index" : 0,
            "batteryPercentage" : 76
        },
        "errorCode" : "",
        "errorMsg" : ""
    }
    ```

* <a id="user-content-getGimbalStatus"> </a>`getGimbalStatus(int index)`

    **Request**

    ```json
    {
        "getGimbalStatus" : {
            "index" : 2
        }
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

* <a id="user-content-getAllAircraftsStatus"> </a>`getAllAircraftsStatus()`

    **Request**

    ```json
    {
        "getAllAircraftsStatus" : true
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

* <a id="user-content-moveToTarget"> </a>`moveToTarget(int index, int coordinateMode, float targetX, float targetY, float targetZ, float velocity)`

    **Request**

    ```json
    {
        "moveToTarget" : {
            "index" : 2,
            "coordinateMode" : ...,
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
            "status" : "moving"
        },
        "errorCode" : "",
        "errorMsg" : ""
    }
    ```

* <a id="user-content-setUpdateRate"> </a>`setUpdateRate(int index, int rate)`

    **Request**

    ```json
    {
        "setUpdateRate" : {
            "index" : 2,
            "rate" : 5
        }
    }
    ```

    **Response**

    ```json
    {
        "aircraft" : {
            "index" : 2,
            "updateRate" : 5
        },
        "errorCode" : "",
        "errorMsg" : ""
    }
    ```