# SSH Port Forwarding

Goal: start a jupyter lab into a remote machine, and connect to it via ssh port port forwarding, directly from my browser.

```bash
ssh USER@HOST_OR_IP
uv venv
source venv/bin/activate
uv pip install jupyterlab
jupyter lab --no-browser --port=8888
```

Then, in my local machine, I can run the following command to connect to the remote machine:

```bash
ssh -L local_port:destination_server_ip:remote_port ssh_server_hostname
ssh -L 8888:localhost:8888 USER@HOST_OR_IP
open http://localhost:8888
```
