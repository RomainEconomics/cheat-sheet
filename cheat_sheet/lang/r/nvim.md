# R In NVIM

```r
# LocalLeader: `\`
# <LocalLeader>rf    - Start R REPL
# <LocalLeader>rq    - Quit R REPL
# <LocalLeader>rh    - Help function
# <-                 - Insert assignment operator (`alt -`)
# RConfigShow
# RStop              - To manually stop R
# RKill              - To manually kill R
#
# Run R codes
# <LocalLeader>d     - Send line to R REPL
# <LocalLeader>aa    - Send whole filk to R REPL
# <LocalLeader>vs    - Run code in a horizontal split
# <LocalLeader>vv    - Run code in a vertical split
# <LocalLeader>vh    - Display head of a df
# [c]<LocalLeader>gn - go to the next chunk of R code
# [c]<LocalLeader>gN - go to the previous chunk of R code
# :messages          - Show error messages (when they disappear too quickly)
# :RDebugInfo        - Show debugging info

bspm::disable()
# install.packages("tidymodels", dependencies = TRUE, INSTALL_opts = "--no-lock")
# install.packages("tidyverse", dependencies = TRUE, INSTALL_opts = '--no-lock')
# install.packages("nanoparquet", dependencies = TRUE, INSTALL_opts = "--no-lock")
# install.packages("ggridges", INSTALL_opts = "--no-lock")

library(tidymodels)
library(tidyverse)
library(ggridges)
library(nanoparquet)


```
