# k6

Official Document:

## Installation

You can install k6s with Docker

```bash
❯ docker pull grafana/k6

Using default tag: latest
latest: Pulling from grafana/k6
df9b9388f04a: Pull complete
2547cbdaee72: Pull complete
7de344c01fdf: Pull complete
Digest: sha256:2a792cd5aef2976304c89c436f20e122940b43a141265d185c87101d5e8a0035
Status: Downloaded newer image for grafana/k6:latest
docker.io/grafana/k6:latest
```

## Running k6

### Running local tests

```js
import http from "k6/http";
import { sleep } from "k6";

export default function () {
  http.get("https://test.k6.io");
  sleep(1);
}
```

```bash
❯ docker run --rm -i grafana/k6 run - <script.js

          /\      |‾‾| /‾‾/   /‾‾/
     /\  /  \     |  |/  /   /  /
    /  \/    \    |     (   /   ‾‾\
   /          \   |  |\  \ |  (‾)  |
  / __________ \  |__| \__\ \_____/ .io

  execution: local
     script: -
     output: -

  scenarios: (100.00%) 1 scenario, 1 max VUs, 10m30s max duration (incl. graceful stop):
           * default: 1 iterations for each of 1 VUs (maxDuration: 10m0s, gracefulStop: 30s)


running (00m01.0s), 1/1 VUs, 0 complete and 0 interrupted iterations
default   [   0% ] 1 VUs  00m01.0s/10m0s  0/1 iters, 1 per VU

running (00m01.6s), 0/1 VUs, 1 complete and 0 interrupted iterations
default ✓ [ 100% ] 1 VUs  00m01.6s/10m0s  1/1 iters, 1 per VU

     data_received..................: 17 kB 11 kB/s
     data_sent......................: 442 B 281 B/s
     http_req_blocked...............: avg=404.19ms min=404.19ms med=404.19ms max=404.19ms p(90)=404.19ms p(95)=404.19ms
     http_req_connecting............: avg=165.24ms min=165.24ms med=165.24ms max=165.24ms p(90)=165.24ms p(95)=165.24ms
     http_req_duration..............: avg=168.36ms min=168.36ms med=168.36ms max=168.36ms p(90)=168.36ms p(95)=168.36ms
       { expected_response:true }...: avg=168.36ms min=168.36ms med=168.36ms max=168.36ms p(90)=168.36ms p(95)=168.36ms
     http_req_failed................: 0.00% ✓ 0        ✗ 1
     http_req_receiving.............: avg=256.98µs min=256.98µs med=256.98µs max=256.98µs p(90)=256.98µs p(95)=256.98µs
     http_req_sending...............: avg=73.39µs  min=73.39µs  med=73.39µs  max=73.39µs  p(90)=73.39µs  p(95)=73.39µs
     http_req_tls_handshaking.......: avg=197.08ms min=197.08ms med=197.08ms max=197.08ms p(90)=197.08ms p(95)=197.08ms
     http_req_waiting...............: avg=168.03ms min=168.03ms med=168.03ms max=168.03ms p(90)=168.03ms p(95)=168.03ms
     http_reqs......................: 1     0.634756/s
     iteration_duration.............: avg=1.57s    min=1.57s    med=1.57s    max=1.57s    p(90)=1.57s    p(95)=1.57s
     iterations.....................: 1     0.634756/s
     vus............................: 1     min=1      max=1
     vus_max........................: 1     min=1      max=1
```

### Adding more VUs

```bash
docker run --rm -i grafana/k6 run --vus 10 --duration 30s - <script.js
```
