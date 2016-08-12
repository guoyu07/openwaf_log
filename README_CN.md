Synopsis
========
```lua
    -- app/openwaf_init.lua
    -- construct a new object - twaf_logger
    local twaf_log_m = require "lib.twaf.twaf_log"
    twaf_logger = twaf_log_m:new(twaf_config.twaf_default_conf.twaf_log)
    
    -- app/openwaf_log.lua
    
```


Directives
==========
new
---
**syntax:** *logger = new(self, config)*

log
---
**syntax:** *logger:log(events)*
