---
title: Network Troubleshooting
author: Andrew/@adell4444
date: 2/27/2025
---

# Understanding MTR (My Traceroute) and Interpreting Results

MTR (My Traceroute) is a powerful network diagnostic tool that helps identify network issues along a route by combining the functions of `ping` and `traceroute`. However, interpreting MTR results requires an understanding of how network devices handle ICMP traffic and how latency impacts overall performance.

## Key Considerations When Using MTR

1. ICMP Deprioritization:
   - Some routers and network devices deprioritize ICMP traffic, meaning they may not respond quickly or consistently to MTR queries.
   - This does not necessarily indicate a network issue unless packet loss or high latency persists beyond that hop.

2. Latency and Cascading Issues:
   - MTR helps identify hops causing performance degradation throughout the entire route.
   - If a single hop shows high latency but subsequent hops do not, it likely means that the hop is deprioritizing ICMP rather than causing network issues.

## Using MTR

<content>

## Interpreting MTR Output

Consider the following MTR result:

```bash
HOST: Andrews-MBP-6               Loss%   Snt   Last   Avg  Best  Wrst StDev
  1.|-- router.asus.com            0.0%    10    1.1   1.4   1.0   2.2   0.0
  2.|-- X.X.X.X                    0.0%    10    1.9   1.9   1.7   2.2   0.0
  3.|-- X.X.X.X                    0.0%    10   12.6  11.7   3.4  47.4  13.3
  4.|-- X.X.X.X                   70.0%    10  10876 10832 10785 10876  45.1
  5.|-- X.X.X.X                    0.0%    10   10.0  11.4   8.1  13.7   1.8
  6.|-- X.X.X.X                    0.0%    10   14.3  12.9   8.8  20.5   3.4
```

Hop 4 shows very high latency and packet loss. However, subsequent hops do not exhibit high latency or packet loss, meaning this hop is likely deprioritizing ICMP rather than indicating a routing issue. If latency and packet loss continued past Hop 4, it would indicate a genuine network problem affecting the route.

## Using MTR to Diagnose ISP Issues

- If you experience poor call quality, slow speeds, or high latency, running an MTR trace can help confirm if the issue is related to your ISP.
- If packet loss or high latency persists through multiple hops, it can be used as evidence when reporting issues to your ISP.
- Keep in mind that occasional spikes in latency may not indicate a systemic issue unless they are consistent over multiple tests.
