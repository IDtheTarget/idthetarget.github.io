---
{"dg-publish":true,"permalink":"/self-hosting/raspberry-pi-v2/"}
---

## References
- https://geekworm.com/collections/raspberry-pi/products/x1011
- https://pipci.jeffgeerling.com/hats/geekworm-x1011-4-drive-nvme.html
- https://pipci.jeffgeerling.com/hats
- https://www.amazon.com/dp/B0D78LCWBC
- https://www.jeffgeerling.com/blog/2024/4-way-nvme-raid-comes-raspberry-pi-5

## Discussion
When I started this project, I was just looking at my own NextCloud instance. I'm only using around 60GB of Google Data, so a 2TB SSD seemed eminently reasonable. That's when I started building my original [[Self-Hosting/Raspberry Pi\|Raspberry Pi]]. But then I re-looked at my wife's Google Data, and she's got a terabyte of pictures alone. So I'm going to need something larger.

When I saw that, I decided to start looking for a larger NVME card for the Raspberry Pi, and I found [this](https://www.jeffgeerling.com/blog/2024/4-way-nvme-raid-comes-raspberry-pi-5). My plan is to build the second Pi using a 4-way NVME SSD, turn it into the primary (so that I can re-capture every step of this process), buy another 4 way board and two more SSD for the v1 and turn it into a v2 for storing the backups offsite.
