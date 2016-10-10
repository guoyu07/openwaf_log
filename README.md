Synopsis
========
```lua
    -- app/openwaf_init.lua
    -- construct a new object - twaf_logger
    local twaf_log_m = require "lib.twaf.twaf_log"
    twaf_logger = twaf_log_m:new(config)
    
    -- app/openwaf_log.lua
    twaf_logger:log(events)
```

Modules Configuration Directives
================================
```txt
"twaf_log": {
        "access_log_state":false,     -- 访问日志开关
        "security_log_state":true,    -- 安全日志开关
        "sock_type":"udp",            -- 支持tcp和udp两种协议
        "content_type":"JSON",        -- 支持JSON和INFLUXDB两种日志格式
        "host":"127.0.0.1",           -- 日志服务器地址
        "port":60055,                 -- 日志服务器端口号
        "flush_limit":0,              -- 缓冲，当存储的日志大于阈值才发送
        "drop_limit":1048576,
        "max_retry_times":5,          -- 最大容错次数
        "ssl":false,                  -- 是否开启ssl协议
        "access_log":{}               -- 访问日志格式
        "security_log":{}             -- 安全日志格式
}
```

###access_log_state
**syntax:** *"access_log_state": true|false*

**default:** *false*

**context:** *twaf_log*

访问日志开关，默认关闭

###security_log_state
**syntax:** *"security_log_state": true|false*

**default:** *true*

**context:** *twaf_log*

安全事件日志开关，默认开启

###sock_type
**syntax:** *"sock_type": tcp|udp*

**default:** *udp*

**context:** *twaf_log*

日志传输协议，默认udp

###content_type
**syntax:** *"content_type": JSON|INFLUXDB*

**default:** *JSON*

**context:** *twaf_log*

日志格式，默认JSON

###host
**syntax:** *"host": string*

**default:** *"127.0.0.1"*

**context:** *twaf_log*

日志接收服务器的ip地址

###port
**syntax:** *"port": number*

**default:** *60055*

**context:** *twaf_log*

日志接收服务器的端口号

###flush_limit
**syntax:** *"flush_limit": number*

**default:** *0*

**context:** *twaf_log*

缓冲区大小，当存储的日志大于阈值才发送，默认值为0，即立即发送日志

###drop_limit
**syntax:** *"drop_limit": number*

**default:** *1048576*

**context:** *twaf_log*

###max_retry_times
**syntax:** *"max_retry_times": number*

**default:** *5*

**context:** *twaf_log*

最大容错次数

###ssl
**syntax:** *"ssl": true|false*

**default:** *false*

**context:** *twaf_log*

是否开启ssl协议，默认false

###access_log
**syntax:** *"access_log": table*

**default:** *false*

**context:** *twaf_log*

访问日志格式

###security_log
**syntax:** *"security_log": table*

**default:** *false*

**context:** *twaf_log*

安全事件日志格式

若content_type为JSON，则日志格式为
```
[
    variable_key_1, 
    variable_key_2, 
    ...
]
```
若content_type为INFLUXDB，则日志格式为
```
{
    "db":MEASUREMENT名称, 
    "tags":[variable_key_1, variable_key_2, ...], 
    "fileds"[variable_key_1, variable_key_2, ...],
    "time":true|false
}
```

变量名称详见规则引擎模块[twaf_secrules](#https://github.com/titansec/openwaf_rule_engine#variables)

```
    #日志格式举例
        #JSON格式
        "security_log": [
            "remote_addr",
            "remote_port",
            "userid",
            "dev_uuid",
            "original_dst_addr",
            "original_dst_port",
            "remote_user",
            "time_local",
            "msec",
            "request_method",
            "request_uri",
            "request_protocol",
            "status",
            "bytes_sent",
            "http_referer",
            "http_user_agent",
            "gzip_ratio",
            "http_host",
            "raw_header"
        ]

        #INFLUXDB格式
        "security_log": {
            "db":"test",                  -- MEASUREMENT名称
            "tags":[],                    -- tags keys
            "fileds":[                    -- fileds keys
                "remote_addr",
                "remote_port",
                "userid",
                "dev_uuid",
                "original_dst_addr",
                "original_dst_port",
                "remote_user",
                "time_local",
                "msec",
                "request_method",
                "request_uri",
                "request_protocol",
                "status",
                "bytes_sent",
                "http_referer",
                "http_user_agent",
                "gzip_ratio",
                "http_host",
                "raw_header"
            ],
            "time":true                   -- 日志是否携带时间戳
        }
```

Directives
==========
new
---
**syntax:** *logger = new(self, config)*

log
---
**syntax:** *logger:log(events)*
