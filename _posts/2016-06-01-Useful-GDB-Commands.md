---
layout: note
title: Useful GDB Commands
---
# Create a hook
```

define hook-stop

info registers //registers

x/24wx $esp //stack

x2i $eip //And next two registers

end
```

