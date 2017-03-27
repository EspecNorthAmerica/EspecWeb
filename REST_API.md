# Index Route  
Returns top level uri list

* **URL**  
    /api/v1.0/

* **Method**  
    `GET`

* **URL Params**
    * **Optional:**  
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Success Response**
    * **Code:** `200`  
    * **Content:**  
    ```JSON
    {
        "uri": [
            "http://10.30.100.151/api/v1.0/chambers", 
            "http://10.30.100.151/api/v1.0/systems"
        ]
    }
    ```

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`

<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# All Chambers Route
Returns a list of available chambers (only 1 for now)

* **URL**  
    /api/v1.0/chambers

* **Method**  
    `GET`

* **URL Params**
    * **Optional:**  
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Success Response**  
    * **Code:** `200`
    * **Content:**
    ```JSON
    {
        "chambers": [
            {
                "alarms": {
                    "list": [
                        {
                            "controller": 1, 
                            "id": 115, 
                            "name": "Sensor Failure", 
                            "number": 0, 
                            "triggered": false
                        },
                    ], 
                    "ok": true
                }, 
                "controllers": [
                    {
                    "cascade": true, 
                    "humidity": false, 
                    "indConstant": true, 
                    "model": "P300"
                    }
                ], 
                "events": [
                    {
                        "N": 1, 
                        "controller": 1, 
                        "manual": true, 
                        "name": "Time Signal #1", 
                        "status": {
                            "constant": false, 
                            "current": false
                        }, 
                        "uri": "http://10.30.100.151/api/v1.0/chambers/1/events/1", 
                        "valid": true
                    }
                ], 
                "loops": [
                    {
                        "N": 1, 
                        "controller": 1, 
                        "deviation": {
                            "negative": -10.0, 
                            "positive": 10.0
                        }, 
                        "enable": {
                            "constant": true, 
                            "current": true
                        }, 
                        "enable_cascade": {
                            "constant": false, 
                            "current": false
                        }, 
                        "mode": {
                            "constant": "On", 
                            "current": "On"
                        }, 
                        "modes": [
                            "On"
                        ], 
                        "name": "Temperature", 
                        "power": {
                            "constant": null, 
                            "current": null
                        }, 
                        "processValue": {
                            "air": 21.7, 
                            "product": 21.8
                        }, 
                        "range": {
                            "max": 190.0, 
                            "min": -80.0
                        }, 
                        "setValue": {
                            "air": -40.0, 
                            "constant": -40.0, 
                            "current": -40.0, 
                            "product": 0.0
                        }, 
                        "units": "\u00b0C", 
                        "uri": "http://10.30.100.151/api/v1.0/chambers/1/loops/1", 
                        "valid": true
                    }
                ], 
                "operations": {
                    "datetime": {
                        "strftime": "Tue Jan 31 2017 16:35:58", 
                        "uts": 1485880558.0
                    }, 
                    "mode": "Constant", 
                    "program": {
                        "editor": "/program/editor", 
                        "name": null, 
                        "number": null, 
                        "step": null, 
                        "time_end": null, 
                        "time_step": null, 
                        "time_total": null, 
                        "uri": null
                    }
                }, 
                "programs": {
                    "all": [
                        {
                            "name": "", 
                            "number": 1, 
                            "uri": "http://10.30.100.151/api/v1.0/chambers/1/programs/1"
                        },
                    ], 
                    "existing": []
                }, 
                "refrigerators": [
                    {
                    "controller": 1, 
                    "mode": "auto", 
                    "modes": [
                        {
                            "text": "Off", 
                            "value": "off"
                        }, 
                        {
                            "text": "20%", 
                            "value": "20%"
                        }, 
                        {
                            "text": "50%", 
                            "value": "50%"
                        }, 
                        {
                            "text": "100%", 
                            "value": "100%"
                        }, 
                        {
                            "text": "Auto", 
                            "value": "auto"
                        }
                    ],
                    "valid": true
                    }
                ], 
                "uri": "http://10.30.100.151/api/v1.0/chambers/1"
            }
        ]
    }
    ```

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`

<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# Chamber Route  
Get all cachable information about the chamber, This includes opration state, alarm state, control loop status, available programs, time signal status, refrigeration status.

* **URL**  
    /api/v1.0/chambers/:cid

* **Method:**  
    `GET` | `POST` | `PUT`
  
* **URL Params**  
    * **Required:**  
        * `cid=[integer]`  
        Chamber id, must be `1` (used for future expansion)
    * **Optional:**  
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Data Params**  
    All parameters asside from `"N"` & `"controller"` are optiopnal, all extra parameters will be ignored.  
    Where a parameter is `{"constant":value }` the `value` may be applied directly ie:  
    `{"loops":[{"enable":{"constant":value }}]}` == `{"loops":[{"enable":value}]}`
    ```JSON
    {
        "loops": [
            {
                "N": 1, 
                "controller": 1, 
                "deviation": {
                    "negative": -10.0, 
                    "positive": 10.0
                }, 
                "enable": { "constant": true }, 
                "enable_cascade": { "constant": false }, 
                "mode": { "constant": "On" },
                "power": { "constant": 0.0 }, 
                "range": {
                    "max": 190.0, 
                    "min": -80.0
                }, 
                "setValue": { "constant": -40.0 }
            }
        ],
        "events": [
            {
                "N": 1, 
                "controller": 1, 
                "status": { "constant": false }
            }
        ],
        "refrigerators": [
            {
                "controller": 1, 
                "mode": "auto"
            }
        ],
    }
    ```

* **Success Response:**  
    * `GET` Request:
        * **Code:** `200`  
        **Content:**  
        ```JSON
        {
            "alarms": {
                "list": [
                {
                    "controller": 1, 
                    "id": 115, 
                    "name": "Sensor Failure", 
                    "number": 0, 
                    "triggered": false
                }
                ], 
                "ok": true
            }, 
            "controllers": [
                {
                    "cascade": true, 
                    "humidity": false, 
                    "indConstant": true, 
                    "model": "P300"
                }
            ], 
            "events": [
                {
                    "N": 1, 
                    "controller": 1, 
                    "manual": true, 
                    "name": "Time Signal #1", 
                    "status": {
                        "constant": false, 
                        "current": false
                    }, 
                    "uri": "http://10.30.100.151/api/v1.0/chambers/1/events/1", 
                    "valid": true
                }
            ], 
            "loops": [
                {
                    "N": 1, 
                    "controller": 1, 
                    "deviation": {
                        "negative": -10.0, 
                        "positive": 10.0
                    }, 
                    "enable": {
                        "constant": true, 
                        "current": true
                    }, 
                    "enable_cascade": {
                        "constant": false, 
                        "current": false
                    }, 
                    "mode": {
                        "constant": "On", 
                        "current": "On"
                    }, 
                    "modes": [
                        "On"
                    ], 
                    "name": "Temperature", 
                    "power": {
                        "constant": null, 
                        "current": null
                    }, 
                    "processValue": {
                        "air": 20.8, 
                        "product": 20.9
                    }, 
                    "range": {
                        "max": 190.0, 
                        "min": -80.0
                    }, 
                    "setValue": {
                        "air": -40.0, 
                        "constant": -40.0, 
                        "current": -40.0, 
                        "product": 0.0
                    }, 
                    "units": "\u00b0C", 
                    "uri": "http://10.30.100.151/api/v1.0/chambers/1/loops/1", 
                    "valid": true
                }
            ], 
            "operations": {
                "datetime": {
                    "strftime": "Wed Feb 01 2017 08:12:44", 
                    "uts": 1485936764.0
                }, 
                "mode": "Constant", 
                "program": {
                    "editor": "/program/editor", 
                    "name": null, 
                    "number": null, 
                    "step": null, 
                    "time_end": null, 
                    "time_step": null, 
                    "time_total": null, 
                    "uri": null
                }
            }, 
            "programs": {
                "all": [
                    {
                        "name": "", 
                        "number": 1, 
                        "uri": "http://10.30.100.151/api/v1.0/chambers/1/programs/1"
                    }
                ],
                "existing": []
            }, 
            "refrigerators": [
                {
                    "controller": 1, 
                    "mode": "auto", 
                    "modes": [
                        {
                            "text": "Off", 
                            "value": "off"
                        }, 
                        {
                            "text": "20%", 
                            "value": "20%"
                        }, 
                        {
                            "text": "50%", 
                            "value": "50%"
                        }, 
                        {
                            "text": "100%", 
                            "value": "100%"
                        }, 
                        {
                            "text": "Auto", 
                            "value": "auto"
                        }
                    ], 
                    "valid": true
                }
            ], 
            "uri": "http://10.30.100.151/api/v1.0/chambers/1"
        }
        ```
    * `POST` | `PUT` Request  
        * **Code:** 200  
        **Content:**
        ```JSON
            {
                "events": [
                    {
                        "N": 1, 
                        "controller": 1, 
                        "manual": true, 
                        "name": "Time Signal #1", 
                        "status": {
                            "constant": false, 
                            "current": false
                        }, 
                        "uri": "http://10.30.100.151/api/v1.0/chambers/1/events/1", 
                        "valid": true
                    }
                ], 
                "loops": [
                    {
                        "N": 1, 
                        "controller": 1, 
                        "deviation": {
                            "negative": -10.0, 
                            "positive": 10.0
                        }, 
                        "enable": {
                            "constant": true, 
                            "current": true
                        }, 
                        "enable_cascade": {
                            "constant": false, 
                            "current": false
                        }, 
                        "mode": {
                            "constant": "On", 
                            "current": "On"
                        }, 
                        "modes": [
                            "On"
                        ], 
                        "name": "Temperature", 
                        "power": {
                            "constant": null, 
                            "current": null
                        }, 
                        "processValue": {
                            "air": 20.8, 
                            "product": 20.9
                        }, 
                        "range": {
                            "max": 190.0, 
                            "min": -80.0
                        }, 
                        "setValue": {
                            "air": -40.0, 
                            "constant": -40.0, 
                            "current": -40.0, 
                            "product": 0.0
                        }, 
                        "units": "\u00b0C", 
                        "uri": "http://10.30.100.151/api/v1.0/chambers/1/loops/1", 
                        "valid": true
                    }
                ], 
                "refrigerators": [
                    {
                        "controller": 1, 
                        "mode": "auto", 
                        "modes": [
                            {
                                "text": "Off", 
                                "value": "off"
                            }, 
                            {
                                "text": "20%", 
                                "value": "20%"
                            }, 
                            {
                                "text": "50%", 
                                "value": "50%"
                            }, 
                            {
                                "text": "100%", 
                                "value": "100%"
                            }, 
                            {
                                "text": "Auto", 
                                "value": "auto"
                            }
                        ], 
                        "valid": true
                    }
                ], 
                "uri": "http://10.30.100.151/api/v1.0/chambers/1"
            }
            ```

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`

<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# Chamber Loops Route  
Get a list of all control loops for the chamber.

* **URL**  
    /api/v1.0/chambers/:cid/loops

* **Method:**  
    `GET` | `POST` | `PUT`

* **URL Params**  
    * **Required:**  
        * `cid=[integer]`  
        Chamber id, must be `1` (used for future expansion)
    * **Optional:**
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Data Params**  
    All parameters asside from `"N"` & `"controller"` are optional, all extra parameters will be ignored.  
    Where a parameter is `{"constant":value }` the `value` may be applied directly ie:  
    `[{"enable":{"constant":value }}]` == `[{"enable":value}]`  
    ```JSON
    [
        {
            "N": 1, 
            "controller": 1, 
            "deviation": {
                "negative": -10.0, 
                "positive": 10.0
            }, 
            "enable": { "constant": true }, 
            "enable_cascade": { "constant": false }, 
            "mode": { "constant": "On" },
            "power": { "constant": 0.0 }, 
            "range": {
                "max": 190.0, 
                "min": -80.0
            }, 
            "setValue": { "constant": -40.0 }
        }
    ]
    ```

* **Success Response:**  
    **Code:** `200`  
    **Content:**  
    ```JSON
    {
        "loops": [
            {
                "N": 1, 
                "controller": 1, 
                "deviation": {
                    "negative": -10.0, 
                    "positive": 10.0
                }, 
                "enable": {
                    "constant": true, 
                    "current": true
                }, 
                "enable_cascade": {
                    "constant": false, 
                    "current": false
                }, 
                "mode": {
                    "constant": "On", 
                    "current": "On"
                }, 
                "modes": [
                    "On"
                ], 
                "name": "Temperature", 
                "power": {
                    "constant": null, 
                    "current": null
                }, 
                "processValue": {
                    "air": 20.8, 
                    "product": 20.9
                }, 
                "range": {
                    "max": 190.0, 
                    "min": -80.0
                }, 
                "setValue": {
                    "air": -40.0, 
                    "constant": -40.0, 
                    "current": -40.0, 
                    "product": 0.0
                }, 
                "units": "\u00b0C", 
                "uri": "http://10.30.100.151/api/v1.0/chambers/1/loops/1", 
                "valid": true
            }
        ]
    }
    ```

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`

* **Notes**
    * The following parameters may or may not be present on a `enable_cascade`, `deviation`, depending on if the loop/controller supports cascade control/product temperature control.
    * The `power` parameter is only really apllicable to loops running on a watlow F4T

<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# Chamber Events Route  
Get a list of all events (Time Signals) for the chamber.

* **URL**  
    /api/v1.0/chambers/:cid/events

* **Method:**  
    `GET` | `POST` | `PUT`

* **URL Params**  
    * **Required:**  
        * `cid=[integer]`  
        Chamber id, must be `1` (used for future expansion)
    * **Optional:**
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Data Params**  
    All parameters asside from `"N"` & `"controller"` are optional, all extra parameters will be ignored.  
    Where a parameter is `{"constant":value }` the `value` may be applied directly ie:  
    `[{"enable":{"constant":value }}]` == `[{"enable":value}]`  
    ```JSON
    [
        {
            "N": 1, 
            "controller": 1, 
            "status": { "constant": false }, 
        }
    ]
    ```

* **Success Response:**  
    **Code:** `200`  
    **Content:**  
    ```JSON
    {
        "events": [
            {
                "N": 1,
                "controller": 1,
                "manual": true,
                "name": "Time Signal #1",
                "status": {
                    "constant": false,
                    "current": false
                },
                "uri": "http://10.30.100.151/api/v1.0/chambers/1/events/1",
                "valid": true
            }
        ]
    }
    ```

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`

<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# Chamber Refrigerators Route  
Get a list of all refrigeration systems for the chamber.

* **URL**  
    /api/v1.0/chambers/:cid/refrigerators

* **Method:**  
    `GET` | `POST` | `PUT`

* **URL Params**  
    * **Required:**  
        * `cid=[integer]`  
        Chamber id, must be `1` (used for future expansion)
    * **Optional:**
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Data Params**  
    All parameters asside from `"controller"` are optional, all extra parameters will be ignored.  
    ```JSON
    [
        {
            "controller": 1,
            "mode": "auto"
        }
    ]
    ```

* **Success Response:**  
    **Code:** `200`  
    **Content:**  
    ```JSON
    {
        "refrigerators": [
            {
                "controller": 1,
                "mode": "auto",
                "modes": [
                    {
                        "text": "Off",
                        "value": "off"
                    },
                    {
                        "text": "20%",
                        "value": "20%"
                    },
                    {
                        "text": "50%",
                        "value": "50%"
                    },
                    {
                        "text": "100%",
                        "value": "100%"
                    },
                    {
                        "text": "Auto",
                        "value": "auto"
                    }
                ],
                "valid": true
            }
        ]
    }
    ```

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`

<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# Chamber Controllers Route  
Get a list of all process controllers on the chamber.

* **URL**
    /api/v1.0/chambers/:cid/controllers

* **Method:**  
    `GET`

* **URL Params**  
    * **Required:**  
        * `cid=[integer]`  
        Chamber id, must be `1` (used for future expansion)
    * **Optional:**
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Data Params**  
    None

* **Success Response:**  
    **Code:** `200`  
    **Content:**  
    ```JSON
    {
        "controllers": [
            {
                "cascade": true,
                "humidity": false,
                "indConstant": true,
                "model": "P300"
            }
        ]
    }
    ```

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`

<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# Chamber Operations Route  
Get the current mode of operation for the chamber.

* **URL**  
    /api/v1.0/chambers/:cid/operations

* **Method:**  
    `GET`

* **URL Params**  
    * **Required:**  
        * `cid=[integer]`  
        Chamber id, must be `1` (used for future expansion)
    * **Optional:**
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Data Params**  
    None

* **Success Response:**  
    **Code:** `200`  
    **Content:**  
    ```JSON
    {
        "operations": {
            "datetime": {
                "strftime": "Wed Feb 01 2017 12:51:26",
                "uts": 1485953486
            },
            "mode": "Constant",
            "program": {
                "editor": "/program/editor",
                "name": null,
                "number": null,
                "step": null,
                "time_end": null,
                "time_step": null,
                "time_total": null,
                "uri": null
            }
        }
    }
    ```

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`

<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# Chamber Programs Route  
Get a list of all available programs for the chamber.

* **URL**  
    /api/v1.0/chambers/:cid/programs

* **Method:**  
    `GET`

* **URL Params**  
    * **Required:**  
        * `cid=[integer]`  
        Chamber id, must be `1` (used for future expansion)
    * **Optional:**
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Data Params**  
    None

* **Success Response:**  
    **Code:** `200`  
    **Content:**  
    ```JSON
    {
        "programs": {
            "all": [
                {
                    "name": "",
                    "number": 1,
                    "uri": "http://10.30.100.151/api/v1.0/chambers/1/programs/1"
                }
            ],
            "existing": []
        }
    }
    ```

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`

<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# Chamber Programs Route  
Get a list of all alarms possible alarms, there status, and if any are currently triggered.

* **URL**  
    /api/v1.0/chambers/:cid/alarms

* **Method:**  
    `GET`

* **URL Params**  
    * **Required:**  
        * `cid=[integer]`  
        Chamber id, must be `1` (used for future expansion)
    * **Optional:**
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Data Params**  
    None

* **Success Response:**  
    **Code:** `200`  
    **Content:**  
    ```JSON
    {
        "alarms": {
            "list": [
                {
                    "controller": 1,
                    "id": 115,
                    "name": "Sensor Failure",
                    "number": 0,
                    "triggered": false
                }
            ],
            "ok": true
        }
    }
    ```

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`

<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# Chamber Loops\Events\Refrigerators\Controllers\Operations\Programs\Alarms Route  
Get any combination of the individual Chamber Loops\Events\Refrigerators\Controllers\Operations\Programs\Alarms routes in one call.

* **URL**  
    /api/v1.0/chambers/:cid/:params

* **Method:**  
    `GET` | `POST` | `PUT`
  
* **URL Params**  
    * **Required:**  
        * `cid=[integer]`  
        Chamber id, must be `1` (used for future expansion)
        * `params=[list[strings]]`  
        Valid parameters: `loops`, `events`, `refrigerators`, `controllers`, `operations`, `programs`, `alarms`  
        separate desired params with a `+` ie: `/api/v1.0/chambers/1/loops+events`
    * **Optional:**
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Data Params**  
    Only params `loops`, `events`, and `refrigerators` are settable
    All parameters asside from `"N"` & `"controller"` are optional, all extra parameters will be ignored.  
    Where a parameter is `{"constant":value }` the `value` may be applied directly ie:  
    `{"loops":[{"enable":{"constant":value }}]}` == `{"loops":[{"enable":value}]}`  
    ```JSON
    {
        "loops": [...],
        "events": [...],
        "refrigerators": [...]
    }
    ```

* **Success Response:**  
    * `GET` Request:
        * **Code:** `200`  
        **Content:**  
        ```JSON
        {
            "alarms": {...}, 
            "controllers": [...], 
            "events": [...], 
            "loops": [...], 
            "operations": {...}, 
            "programs": {...}, 
            "refrigerators": [...]
        }
        ```
    * `POST` | `PUT` Request  
        * **Code:** 200  
        **Content:**
        ```JSON
        {
            "events": [...], 
            "loops": [...], 
            "refrigerators": [...]
        }
        ```

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`

* **Notes**
    * See the individual routes for an exact explination on what the "Data Params" & "Success Response" data will look like.

<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# Chamber Loop Route  
Get a specific set of loop parameters by id

* **URL**  
    /api/v1.0/chambers/:cid/loops/:lid

* **Method:**  
    `GET` | `POST` | `PUT`

* **URL Params**  
    * **Required:**  
        * `cid=[integer]`  
        Chamber id, must be `1` (used for future expansion)
        * `lid=[integer]`  
        Loop id.
    * **Optional:**
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Data Params**  
    ```JSON
    {
        "N": 1,
        "controller": 1,
        "deviation": {
            "negative": -10,
            "positive": 10
        },
        "enable": { "constant": true },
        "enable_cascade": { "constant": false },
        "mode": { "constant": "On" },
        "power": { "constant": 0.0 },
        "range": {
            "max": 190,
            "min": -80
        },
        "setValue": { "constant": -40 }
    }
    ```

* **Success Response:**  
    * `GET` Request  
    **Code:** `200`  
    **Content:**  
    ```JSON
    {
        "N": 1,
        "controller": 1,
        "deviation": {
            "negative": -10,
            "positive": 10
        },
        "enable": {
            "constant": true,
            "current": true
        },
        "enable_cascade": {
            "constant": false,
            "current": false
        },
        "mode": {
            "constant": "On",
            "current": "On"
        },
        "modes": [
            "On"
        ],
        "name": "Temperature",
        "power": {
            "constant": null,
            "current": null
        },
        "processValue": {
            "air": 21.6,
            "product": 21.6
        },
        "range": {
            "max": 190,
            "min": -80
        },
        "setValue": {
            "air": -40,
            "constant": -40,
            "current": -40,
            "product": 0
        },
        "units": "°C",
        "uri": "http://10.30.100.151/api/v1.0/chambers/1/loops/1",
        "valid": true
    }
    ```
    * `PUT` | `POST` Request  
    **Code:** `204`  
    **Content:** None  

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`

<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# Chamber Event Route  
Get a specific set of Event parameters by id

* **URL**  
    /api/v1.0/chambers/:cid/events/:eid

* **Method:**  
    `GET` | `POST` | `PUT`

* **URL Params**  
    * **Required:**  
        * `cid=[integer]`  
        Chamber id, must be `1` (used for future expansion)
        * `eid=[integer]`  
        Event id.
    * **Optional:**
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Data Params**  
    Broken in Web Controller V2.0

* **Success Response:**  
    Broken in Web Controller V2.0

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`

<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# Chamber Program Route  
Get/update/delete a specific program

* **URL**  
    /api/v1.0/chambers/:cid/events/:pid

* **Method:**  
    `GET` | `POST` | `PUT` | `DELETE`

* **URL Params**  
    * **Required:**  
        * `cid=[integer]`  
        Chamber id, must be `1` (used for future expansion)
        * `pid=[integer]`  
        Program Number.
    * **Optional:**
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.
        * `method=DELETE`  
        Override the request `POST` or `PUT` methods to preform a `DELETE` request.

* **Data Params**  
    Post same data type recieved via the `GET` Response

* **Success Response:**  
    * `GET` Request  
    **Code:** `200`  
    **Content:**
        * **P300/SCP-220 Based Chambers**
        ```JSON
        {
            "controllerType": "Espec,P300",
            "counter_a": {
                "cycles": 0,
                "end": 0,
                "start": 0
            },
            "counter_b": {
                "cycles": 0,
                "end": 0,
                "start": 0
            },
            "end": "OFF",
            "humiDetail": {
                "mode": "OFF",
                "range": {
                "max": 100,
                "min": 0
                },
                "setpoint": null
            },
            "name": "TEST1",
            "next_prgm": 0,
            "steps": [
                {
                    "granty": false,
                    "humidity": {
                        "enable": false,
                        "ramp": false,
                        "setpoint": 0
                    },
                    "number": 1,
                    "paused": false,
                    "refrig": {
                        "mode": "auto",
                        "setpoint": 0
                    },
                    "relay": [
                        false,
                        false,
                        false,
                        false,
                        false,
                        false,
                        false,
                        false,
                        false,
                        false,
                        false,
                        false
                    ],
                    "temperature": {
                        "deviation": {
                        "negative": -10,
                        "positive": 10
                        },
                        "enable_cascade": false,
                        "ramp": false,
                        "setpoint": 10
                    },
                    "time": {
                        "hour": 1,
                        "minute": 0
                    }
                }
            ],
            "tempDetail": {
                "mode": "OFF",
                "range": {
                    "max": 190,
                    "min": -80
                },
                "setpoint": null
            }
        }
        ```
        * **Watlow F4T Based Chamber**
        ```JSON
        {
            "controllerType": "WatlowF4T",
            "gs_dev": [
                {
                    "value": 5.6
                },
                {
                    "value": 10
                }
            ],
            "hasenables": true,
            "haswaits": false,
            "log": false,
            "name": "Test1",
            "steps": [
                {
                    "duration": {
                        "hours": 1,
                        "minutes": 0,
                        "seconds": 0
                    },
                    "events": [
                        {
                            "number": 1,
                            "value": "off"
                        },
                        {
                            "number": 2,
                            "value": "off"
                        },
                        {
                            "number": 3,
                            "value": "off"
                        },
                        {
                            "number": 4,
                            "value": "off"
                        },
                        {
                            "number": 5,
                            "value": "off"
                        },
                        {
                            "number": 6,
                            "value": "off"
                        },
                        {
                            "number": 7,
                            "value": "off"
                        },
                        {
                            "number": 8,
                            "value": "off"
                        }
                    ],
                    "jcount": 1,
                    "jstep": 1,
                    "loops": [
                        {
                            "cascade": false,
                            "enable": true,
                            "gsoak": false,
                            "isCascade": false,
                            "max": 180,
                            "min": -70,
                            "mode": "",
                            "rate": 0,
                            "showEnable": false,
                            "target": 10
                        },
                        {
                            "cascade": false,
                            "enable": false,
                            "gsoak": false,
                            "isCascade": false,
                            "max": 95,
                            "min": 10,
                            "mode": "",
                            "rate": 0,
                            "showEnable": true,
                            "target": 10
                        }
                    ],
                    "type": "instant",
                    "waits": []
                }
            ]
        }
        ```
    * `POST` | `PUT` | `DELETE` Request  
    **Code:** `200`  
    **Content:**
    ```JSON
    {
        "programs": {
            "all": [
                {
                    "name": "TEST1",
                    "number": 1,
                    "uri": "http://10.30.100.151/api/v1.0/chambers/1/programs/1"
                }
            ],
            "existing": [
                {
                    "name": "TEST1",
                    "number": 1,
                    "uri": "http://10.30.100.151/api/v1.0/chambers/1/programs/1"
                }
            ]
        }
    }
    ```

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`

<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# Chamber Program Steps Route  
Get the number of steps in a program, and the currently running step if that program is running.

* **URL**  
    /api/v1.0/chambers/:cid/programs/:pid/steps

* **Method:**  
    `GET`

* **URL Params**  
    * **Required:**  
        * `cid=[integer]`  
        Chamber id, must be `1` (used for future expansion)
        * `pid=[integer]`  
        Program number.
    * **Optional:**
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Data Params**  
    None

* **Success Response:**   
    **Code:** `200`  
    **Content:**  `{"count":10, "current":1}`  

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`

<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# Chamber update Operations Route  
Change the run mode of the chamber(Constant, Stop, Program).

* **URL**  
    /api/v1.0/chambers/:cid/operations/:oper  
    /api/v1.0/chambers/:cid/operations/:oper/:pid  
    /api/v1.0/chambers/:cid/operations/:oper/:pid/:step  

* **Method:**  
    `GET`

* **URL Params**  
    * **Required:**  
        * `cid=[integer]`  
        Chamber id, must be `1` (used for future expansion)
        * `oper=[string]`  
        `standby`,`off`,`stop` = Stop operation  
        `constant` = Run the constent setpoint  
        `program` = Run a program, requires `pid=[int]` 
        `programpause` = Pause the running program  
        `programresume` = Resume the paused program  
        `programnextstep` = Run the next step in the running program  
        * `pid=[int]`  
        The number of the program to run if `oper == program`
    * **Optional:**
        * `step=[int]`  
        The step of the program to run, step 1 is run if this is omitted.
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Data Params**  
    None

* **Success Response:**   
    **Code:** `200`  
    **Content:**  
     ```JSON
     {
        "operations": {
            "datetime": {
                "strftime": "Wed Feb 01 2017 14:45:09",
                "uts": 1485960309
            },
            "mode": "Constant",
            "program": {
                "editor": "/program/editor",
                "name": null,
                "number": null,
                "step": null,
                "time_end": null,
                "time_step": null,
                "time_total": null,
                "uri": null
            }
        }
    }
     ```

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`

<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# Chamber Trend Log Route  
Get/Delete the chambers logged data in several foramts.

* **URL**  
    /api/v1.0/chambers/:cid/logs/trend

* **Method:**  
    `GET` | `DELETE`

* **URL Params**  
    * **Required:**  
        * `cid=[integer]`  
        Chamber id, must be `1` (used for future expansion)
    * **Optional:**
        * `format=[string]`  
        `JSON` = Formatted for a [flot chart](http://www.flotcharts.org/).  
        `CSV` = Formatted as comma separated values.  
        * `file=[Boolean]`  
        Return a file instead of text
        * `newest=[int]`  
        Unix time stamp for the newest data point in a range (requires oldest param too)
        * `oldest=[int]`
        Unix time stamp for the oldest data point in a range (requires newest param too)
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Data Params**  
    None

* **Success Response:**   
    * `GET` Request:
    **Code:** `200`  
    **Content:** Varies by configuration/format parameter.
    * `DELETE` Request:
    **Code:** `204`  
    **Content:** None

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`

<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# Chamber Humidity Graph Route  
Get the humidity graph for the chamber formatted for [flot chart](http://www.flotcharts.org/)

* **URL**  
    /api/v1.0/chambers/:cid/logs/humidityGraph

* **Method:**  
    `GET`

* **URL Params**  
    * **Required:**  
        * `cid=[integer]`  
        Chamber id, must be `1` (used for future expansion)
    * **Optional:**
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Data Params**  
    None

* **Success Response:**   
    **Code:** `200`  
    **Content:**
    ```JSON
    {
        "graph": [
            {
                "color": "blue",
                "data": [[85,95],[20,95],[10,90],[10,80],[20,45],[40,20],[60,10],[85,10],[85,95]],
                "label": "Standard Humidity"
            },
            {
                "color": "green",
                "data": [[40,20],[20,45],[10,80],[10,40],[20,30],[40,20]],
                "label": "Low Humidity (Enable Dry Air)"
            },
            {
                "color": "red",
                "data": [[60,10],[40,20],[20,30],[10,40],[10,15],[40,15],[60,10]],
                "label": "Low Humidity (Dry Air & Low Humidity)"
            }
        ],
        "xlabel": "Temperature(°C)",
        "xmax": 100,
        "xmin": 0,
        "xticks": [[0,"0"],[100,"100"],[85,"85"],[20,"20"],[10,"10"],[40,"40"],[60,"60"]],
        "ylabel": "Humidity(%RH)",
        "yticks": [[0,"0"],[100,"100"],[95,"95"],[90,"90"],[80,"80"],[45,"45"],[20,"20"],[10,"10"],[40,"40"],[30,"30"],[15,"15"]]
    }
    ```

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`


<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# Systems Route  
Overview of the system post functions available.

* **URL**  
    /api/v1.0/systems

* **Method**  
    `GET`

* **URL Params**
    * **Optional:**  
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Success Response**
    * **Code:** `200`  
    * **Content:**  
    ```JSON
    {
        "uri": [
            "http://10.30.100.151/api/v1.0/systems/reboot",
            "http://10.30.100.151/api/v1.0/systems/shutdown",
            "http://10.30.100.151/api/v1.0/systems/logs/exceptions",
            "http://10.30.100.151/api/v1.0/systems/chamberInterfaces/1",
            "http://10.30.100.151/api/v1.0/systems/chamberInterfaces/1/build",
            "http://10.30.100.151/api/v1.0/systems/variables"
        ]
    }
    ```

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`

<!-- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -->
# Systems Reboot Route  
Reboot the chamber.

* **URL**  
    /api/v1.0/systems/reboot

* **Method**  
    `GET`

* **URL Params**
    * **Optional:**  
        * `envelope=[Boolean]`  
        Place response data into a `{"data":response}` envelope
        * `cached=[Boolean]`  
        Force the server to refresh the chache before responding.

* **Success Response**
    * **Code:** `204`  
    * **Content:** None

* **Error Response**  
    * **Code:** `403 FORBIDDEN`  
    **Content:** `None`  
    * **Code:** `422 UNPRICESSABLE ENTITY`  
    **Content:** `{ "exception": "python exception class", "message": "python exception message", "traceback": "python traceback" }`