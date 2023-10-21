# Vite does not open the browser in Docker environment

Issue: https://github.com/vitejs/vite/issues/14720

I would like to run both, backend and frontend in Docker.

Vite should open the server in the browser automatically.

Running directly it works like a charm.

Running in Docker environment it fails to open the browser on the local device.

## Reproduction

1. Clone this repository
2. Run `npm run dev:direct` >> will show "Hello Vite" in the browser
3. Run `npm run dev:docker` >> will show an error in the console

```
Error: spawn xdg-open ENOENT
    at ChildProcess._handle.onexit (node:internal/child_process:284:19)
    at onErrorNT (node:internal/child_process:477:16)
    at process.processTicksAndRejections (node:internal/process/task_queues:82:21)
Emitted 'error' event on ChildProcess instance at:
    at ChildProcess._handle.onexit (node:internal/child_process:290:12)
    at onErrorNT (node:internal/child_process:477:16)
    at process.processTicksAndRejections (node:internal/process/task_queues:82:21) {
  errno: -2,
  code: 'ENOENT',
  syscall: 'spawn xdg-open',
  path: 'xdg-open',
  spawnargs: [ 'http://localhost:5173/' ]
}
```

## Resolution

Vite does not have proper rights from inside the Docker Container.

As a solution, with a second command the URL can be opened in the browser:

```bash
open http://localhost:5173
```
