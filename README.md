# Description

This role configures an [oauth2_proxy](https://github.com/pusher/oauth2_proxy) container for GitHub based OAuth.

# Configuration

These settings are all mandatory:
```yaml
oauth_service_name: 'example-oauth'
oauth_service_path: '/docker/example/oauth'
oauth_domain: 'oauth.example.org'
oauth_upstream_port: 4321
oauth_local_port: 1234
oauth_cookie_secret: '123qweASD'
oauth_provider: 'github'
oauth_id: 'some-id'
oauth_secret: 'some-secret'
```
Some options are optional:
```yaml
oauth_local_addr: '0.0.0.0'
oauth_cont_volumes: ['/docker/example/www:/www']
oauth_upstream_url: 'file:///www#/'
oauth_cont_networks: ['other-container-network']
```
Different providers have different mandatory settings.

### GitHub
```yaml
oauth_github_org: 'example-org'
oauth_github_teams: ['devops', 'security']
```
### Google
```yaml
oauth_google_domain: 'example.org'
```
### Keycloak
```yaml
oauth_keycloak_url: 'https://keycloak.example.org'
oauth_keycloak_realm: 'example-org'
oauth_keycloak_domain: 'example.org'
oauth_keycloak_groups: ['admins', 'security']
oauth_keycloak_roles: ['admin']
oauth_scope: 'openid'
```

In order for Keycloak client to work with oauth-proxy, the way to set up the Keycloak client is described [here](https://oauth2-proxy.github.io/oauth2-proxy/configuration/providers/keycloak_oidc/) under `Keycloak new admin console`. Important part is to configure the dedicated audience mapper for your client.

### Nested docker Compose

To include the `oauth-proxy` into another docker compose:
```yaml
oauth_compose_skip_start: true
oauth_upstream_addr:  'container-webui'
```

# Management

The container is reated using Docker Compose:
```
admin@host.example.org:/docker/example % dc ps
       Name                Command               State           Ports         
-------------------------------------------------------------------------------
example-oauth   /bin/oauth2-proxy --provid ...   Up      0.0.0.0:9292->9292/tcp
```
