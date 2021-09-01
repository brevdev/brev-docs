# Runtime and Environment

Brev containerizes and isolates each project.

- Python `3.7` is currently the only supported runtime.
- Each request has a timeout of 30 seconds.
- Each project can support up to 512MB of packages.
- The file system is read only except for `/tmp`.
- `/tmp` has a maximum storage of 512MB.
- Each project has by default 1GB of memory. You can request a maximum of 3GB of memory.
- The server has been load tested with one client and handled 800 req/sec with median response times of 110ms. Results may vary depending on application. More testing needs to be conducted. We believe the current upper bound is 5,000 req/sec.

> **Technical Detail**: Brev is currently built on top of AWS Lambda where each project is a separate Lambda.
