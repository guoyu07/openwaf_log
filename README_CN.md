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


Directives
==========
new
---
**syntax:** *logger = new(self, config)*

log
---
**syntax:** *logger:log(events)*
