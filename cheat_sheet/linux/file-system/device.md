# Device

Type of devices:

- Block devices: devices that store data in blocks (e.g. hard drives)
  - `b` in the first column of the output of `ls -l` for the block device
  - `/dev/sda`
  - buffered access to the hardware
  - multiple bytes are read or written at a time
- Character devices: devices that store data in characters (e.g. keyboard)
  - `c` in the first column of the output of `ls -l` for the character device
  - `/dev/tty`
  - unbuffered access to the hardware
  - access one byte (character) at a time
- Pseudo devices: devices that are not physical devices but are used to communicate with other devices
  - may show up as block or character devices
  - `/dev/null`
    - a device that discards all data written to it
    - reading from it will return an EOF
  - `/dev/zero`
  - `/dev/random`
    - a device that generates stream of random numbers using environmental noise
    - useful for generating random passwords
  - `/dev/urandom`
    - a device that generates stream of random numbers using a PRNG
    - faster than `/dev/random` but less secure
  - `/dev/stdin`
    - standard input device
    - equivalent to `/dev/fd/0`
  - `/dev/stdout`
    - standard output device
    - equivalent to `/dev/fd/1`
  - `/dev/stderr`
    - standard error device
    - equivalent to `/dev/fd/2`

## Examples

### Send output to a device

```bash
# Display the device currently connected to tty
tty # let say it outputs /dev/pts/1

# On another terminal, send the output of a command to the device
echo "Hello" > /dev/pts/1

# This will display "Hello" on the terminal where tty was run
```
