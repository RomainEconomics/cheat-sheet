# Jobs and Foreground Process

```bash
# Create two background jobs
ping -c 10 google.com > /dev/null &
ping -c 10 bing.com > /dev/null &

# List all jobs
jobs

# Bring the first job to foreground
fg %1

# Bring the job with plus sign to foreground
fg

# When a job is in foreground, press Ctrl + Z to send it to background
`ctrl + z`

# The jobs is now in the background, to bring it back to foreground
fg %ID
fg %ID &
bg %ID # same as above
```
