### OAuth
[OAuth Flows - Playground](https://www.oauth.com/playground/)

[JWT Nice Readout](https://www.pingidentity.com/en/company/blog/posts/2019/jwt-security-nobody-talks-about.html)


JWTs are self-describing Bearer tokens.

Two major **_drawbacks_** of JWT are **_stale tokens_** and the inability to **_expire them on-demand_**.

#### Stale tokens

If the role of your user changes, it will not be reflected in the issued token. You will need to issue a brand new one. Ideally, you would expire the one before, which brings us to the next problem.

#### No on-demand expiry

JWTs cannot be expired on demand as they are themselves stateless. An approach to solve this is JWT blacklisting, but that will kill your server's statelessness. This also means that your user cannot essentially log out of your application since you cannot invalidate tokens on-demand.

About the short lived tokens. If the attacker is in possession of a short lived token, he can just query your API to "keep it alive" for as long as you let him (8 hours or 1 day).
