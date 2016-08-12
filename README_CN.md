Synopsis
========
```lua
    -- app/openwaf_init.lua
    -- construct a new object - twaf_logger
    local twaf_log_m = require "lib.twaf.twaf_log"
    twaf_logger = twaf_log_m:new(twaf_config.twaf_default_conf.twaf_log)
    
    -- app/openwaf_log.lua
    
```


Configuration Directives
================================
* [new](#new)
* [log](#log)

new
---
**syntax:** *logger = new(config)*

log
---
**syntax:** *logger = log(self, events)*
