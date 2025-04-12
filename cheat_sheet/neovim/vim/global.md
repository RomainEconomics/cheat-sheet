# Neovim Global

| Command            | Description                                                     |
| ------------------ | --------------------------------------------------------------- |
| `:g/err/y`         | Copy every lines with word `err` in the buffer                  |
| `:g/err/d`         | Delete every lines with word `err` in the buffer                |
| `:g!/err/d`        | Delete every lines withou the word `err` in the buffer          |
| `:g/err$/d`        | Delete every lines with line that ends with `err` in the buffer |
| `:g/\d/d`          | Delete every lines with digits in the buffer                    |
| `:g/^err/d`        | Delete every lines with word `err` in the buffer                |
| `:g/err/s/err/ERR` | Match all lines with `err`, and substitute `err` with `ERR`     |
