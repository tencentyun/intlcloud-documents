Pan resolution uses the wildcard `*` to match all subdomain names; for example, below is the resolution of second-level domain names:

| Host | Record type | Line type | Record value | TTL |
|---|---|---|---|---|
| www | A | Default | 200.202.101.2 | 600 |
| bbs | A | Default  | 200.202.101.2 | 600 |
| blog | A | Default  | 200.202.101.2 | 600 |
| css | A | Default  | 200.202.101.2 | 600 |

There may be many subdomain names, but they are all resolved to the same IP address (and on the same line), which can be simplified by pan resolution as follows:

| Host | Record type | Line type | Record value | TTL |
|---|---|---|---|---|
| * | A | Default | 200.202.101.2 | 600 |

>**Note:**
>The resolution above is only for second-level domain names as the wildcard can only match one level of subdomain names. If it is a third-level domain name, it needs to be matched with `*.example`. The number of pan resolution levels that can be set varies for different package editions.

| Resolution package edition | Pan resolution levels |
|---|---|
| Free edition | 2 |
| Personal Professional edition | 4 |
| Enterprise Basic edition | 6 |
| Enterprise Standard edition | 8 |
| Enterprise Ultimate edition | 10 |
