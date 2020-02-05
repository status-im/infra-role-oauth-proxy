# Description

This role configures an [oauth2_proxy](https://github.com/pusher/oauth2_proxy) container for GitHub based OAuth.

# Configuration

These settings are all mandatory:
```yaml
oauth_domain: 'oauth.example.org'
oauth_cont_name: 'some-container-name-oauth'
oauth_upstream_cont: 'some-container-name'
oauth_upstream_port: 4321
oauth_public_port: 443
oauth_local_port: 1234
oauth_cookie_secret: '123qweASD'
oauth_id: 'some-id'
oauth_secret: 'some-secret'
```

The `oauth_upstream_cont` is optional. If not set the Docker host IP will be used as `upstream`.
