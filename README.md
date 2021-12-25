# Chrome-remote-debug docker with VNC

## (Fork with VNC password support and docker-compose file)

A Google Chrome docker with VNC and chrome remote debugging enabled.
The remote debugging port is exposed with the use of socat. Everything is managed by supervisord.

# Running the docker image

    docker-compose up

The commandline configuration for chrome can be changed by setting environment variables, `default.env` is loaded when no other file is configured. Note that the `--build` argument has to be passed to docker-compose after image changes.

## Ports

- 9333: The remote-debugging port of Google Chrome is forwarded by socat
- 5900: VNC server on port 5900

## Environment variables

* width (default:1920)
* height (default:1920)
* lang (default:en)
* extra_chrome_args (default:)
* vnc_password (default:password)

# Important notes

- The shm-size must be set to a higher value than the default of 64mb because chrome uses this for inter process communications.
- Default password for VNC is `password` and can be changed in `default.env` file.
- The chrome sandbox is disabled because the chrome sandbox interferes with the Docker sandbox

# Viewing Chrome logs

    docker exec -it chrome tail -f /var/log/chrome.log

# Extra info

[Chromium command line switches][1]
[Docker with chrome remote desktop][2]
[Chrome DevTools Protocol Viewer][3]

[1]: http://peter.sh/experiments/chromium-command-line-switches/
[2]: https://github.com/siomiz/chrome
[3]: https://chromedevtools.github.io/devtools-protocol/
