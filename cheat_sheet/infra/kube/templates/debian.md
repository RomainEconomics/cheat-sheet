
# Debian

## Debian Pod

```yaml

apiVersion: v1
kind: Pod
metadata:
  name: debian-debug-pod
spec:
  containers:
  - name: debian
    image: debian
    command: ["sleep", "infinity"] # Keeps the container running
    securityContext:
      privileged: true # Grants full privileges to the container
    stdin: true
    tty: true
  restartPolicy: Always
``` 