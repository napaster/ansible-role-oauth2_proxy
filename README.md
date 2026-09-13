# oauth2_proxy

Role for deploy oauth2-proxy - reverse proxy for authentication using Providers

## Requirements

* Ansible 3.0.0+;

## Example configuration

```yaml
---
oauth2_proxy:
# Enable oauth2-proxy service or not
- enable: 'true'
# Restart oauth2-proxy service after deploy or not
  restart: 'true'
# Install oauth2-proxy package or not
  install_package: 'true'
# 'present' (do nothing if package is already installed) or 'latest' (always
# upgrade to last version)
  package_state: 'latest'
  settings:
# The acr (Authentication Context Class Reference) claim and associated
# acr_values request parameter are defined by the OpenID Connect Core 1.0
# specification
    - acr_values_string: ''
# Allow the use of semicolons in query args
      allow_query_semicolons: ''
# Restrict logins to members of this group
      allowed_group: ''
# Restrict logins to members of these roles
      allowed_role: ''
# Return HTTP 401 instead of redirecting to authentication server if token is
# not valid
      api_route: ''
# OAuth approval_prompt (default "force")
      approval_prompt: ''
# Log authentication attempts (default true)
      auth_logging: 'true'
# Template for authentication log lines (default "{{.Client}} - {{.RequestID}} -
# {{.Username}} [{{.Timestamp}}] [{{.Status}}] {{.Message}}")
      auth_logging_format: ''
# Authenticate against emails via file
      authenticated_emails_file: ''
# Configures the group field to be used when building the groups list
# ('id' (the default) or 'displayName') from Microsoft Graph (available only
# for v2.0 oidc url). Based on this value, the 'allowed_group' config values
# should be adjusted accordingly. If using 'id' as group field, 'allowed_group'
# should contains groups IDs, if using 'displayName' as group field,
# 'allowed_group' should contains groups name
      azure_graph_group_field: 'id'
# Go to a 'tenant-specific' or 'common' (tenant-independent) endpoint.
# Default is 'common'
      azure_tenant: 'common'
# URL to perform a backend logout, {id_token} can be used as placeholder for the
# id_token
      backend_logout_url: ''
# Custom banner string. Use "-" to disable default banner
      banner: ''
# The password to set when passing the HTTP Basic Auth header
      basic_auth_password: ''
# Restrict logins to user with access to this repository
      bitbucket_repository: ''
# Restrict logins to members of this team:
      bitbucket_team: ''
# The OAuth Client ID: ie: "123456.apps.googleusercontent.com"
      client_id: ''
# The OAuth Client Secret
      client_secret: ''
# The file with OAuth Client Secret
      client_secret_file: ''
# Use PKCE code challenges with the specified method. Either 'plain' or 'S256'
      code_challenge_method: ''
# Expire timeframe for CSRF cookie (default 15m0s)
      cookie_csrf_expire: '15m0s'
# When this property is set to 'true', then the CSRF 'cookie_csrf_per_request'
# cookie name is built based on the state and varies per request. If property
# is set to 'false', then CSRF cookie has the same name for all requests.
      cookie_csrf_per_request: 'true'
# Optional cookie domains to force cookies to (ie: .yourcompany.com). The
# longest domain matching the request's host will be used (or the shortest
# cookie domain if there is no match)
      cookie_domain: '.yourcompany.com'
# Expire timeframe for cookie (default 168h0m0s)
      cookie_expire: '168h0m0s'
# Set HttpOnly cookie flag (default is 'true')
      cookie_httponly: 'true'
# The name of the cookie that the 'oauth_proxy' creates (default is
# '_oauth2_proxy')
      cookie_name: '_oauth2_proxy'
# An optional cookie path to force cookies to (default is '/')
      cookie_path: '/'
# Refresh the cookie after this duration ('0' to disable)
      cookie_refresh: '0'
# Set SameSite cookie attribute (ie: 'lax', 'strict', 'none', or '').
      cookie_samesite: ''
# The seed string for secure cookies (optionally base64 encoded)
      cookie_secret: 'bG9sa2VrY2hlYnVyZWsK'
# Set secure (HTTPS) cookie flag (default is 'true')
      cookie_secure: 'true'
# Path or URL to an custom image for the sign_in page logo. Use '-' to disable
# default logo
      custom_sign_in_logo: ''
# Path to custom html templates
      custom_templates_dir: ''
# Display username / password login form if an htpasswd file is provided
# (default is 'true')
      ddisplay_htpasswd_form: 'true'
# Authenticate emails with the specified domain (may be given multiple times).
# Use '*' to authenticate any email
      email_domain: '*'
# Will encode oauth state with base64
      encode_state: 'true'
# Log errors to the standard logging channel instead of stderr
      errors_to_info_log: ''
# Exclude logging requests to paths (eg: '/path1,/path2,/path3')
      exclude_logging_path: ''
# If skip_jwt_bearer_tokens is set, a list of extra JWT issuer=audience pairs
# (where the issuer URL has a '.well-known/openid-configuration' or a
# '.well-known/jwks.json')
      extra_jwt_issuers: ''
# Period between response flushing when streaming responses (default '1s')
      flush_interval: '1s'
# Custom footer string. Use '-' to disable default footer
      footer: ''
# Force HTTPS redirect for HTTP requests
      force_https: 'true'
# Will force JSON errors instead of HTTP error pages or redirects
      force_json_errors: 'true'
# Enable GCP/GKE healthcheck endpoints
      gcp_healthchecks: 'true'
# Restrict logins to members of this organisation
      github_org: ''
# Restrict logins to collaborators of this repository
      github_repo: ''
# Restrict logins to members of this team
      github_team: ''
# The token to use when verifying repository collaborators (must have push
# access to the repository)
      github_token: ''
# Allow users with these usernames to login even if they do not belong to the
# specified org and team or collaborators (may be given multiple times)
      github_user: ''
# Restrict logins to members of this group (may be given multiple times)
      gitlab_group: ''
# Restrict logins to members of this project (may be given multiple times) (eg
# group/project=accesslevel). Access level should be a value matching Gitlab
# access levels, defaulted to '20' if absent
      gitlab_project: 'group/project=accesslevel'
# The google admin to impersonate for api calls
      google_admin_email: ''
# Restrict logins to members of this google group (may be given multiple times)
      google_group: ''
# The path to the service account json credentials
      google_service_account_json: ''
# The target principal to impersonate when using ADC
      google_target_principal: ''
# Use application default credentials instead of service account json (i.e.
# GKE Workload Identity)
      google_use_application_default_credentials: ''
# Additionally authenticate against a htpasswd file. Entries must be created
# with "htpasswd -B" for bcrypt encryption
      htpasswd_file: ''
# The groups to be set on sessions for htpasswd users (may be given multiple
# times)
      htpasswd_user_group: ''
# [http://]<addr>:<port> or unix://<path> to listen on for HTTP clients (default
# is '127.0.0.1:4180')
      http_address: '127.0.0.1:4180'
# <addr>:<port> to listen on for HTTPS clients (default is ':443')
      https_address: ':443'
# Don't fail if an email address in an 'id_token' is not verified
      insecure_oidc_allow_unverified_email: 'true'
# Do not verify if issuer matches OIDC discovery URL
      insecure_oidc_skip_issuer_verification: 'true'
# Skip verifying the OIDC ID Token's nonce claim (default is 'true')
      insecure_oidc_skip_nonce: 'true'
# Private key in PEM format used to sign JWT
      jwt_key: ''
# Path to the private key file in PEM format used to sign the JWT
      jwt_key_file: ''
# Restrict logins to members of these groups (may be given multiple times)
      keycloak_group: ''
# Should rotated log files be compressed using gzip
      logging_compress: 'true'
# File to log requests to, '' for stdout
      logging_filename: ''
# If the time in log files and backup filenames are local or UTC time (default
# is 'true')
      logging_local_time: 'true'
# Maximum number of days to retain old log files (default is '7')
      logging_max_age: '7'
# Maximum number of old log files to retain ('0' to disable)
      logging_max_backups: '0'
# Maximum size in megabytes of the log file before rotation (default is '100')
      logging_max_size: '100'
# Authentication endpoint
      login_url:
        'https://sso.example.com/auth/realms/example/protocol/openid-connect/auth'
# The address '/metrics' will be served on (e.g. ':9100')
      metrics_address: ':9100'
# The address '/metrics' will be served on for HTTPS clients (e.g. ':9100')
      metrics_secure_address: ':9100'
# Path to certificate file for secure metrics server
      metrics_tls_cert_file: ''
# Path to private key file for secure metrics server
      metrics_tls_key_file: ''
# Which OIDC claims are used as audience to verify against client id (default
# is '[aud]')
      oidc_audience_claim: '[aud]'
# Which OIDC claim contains the user's email (default 'email')
      oidc_email_claim: 'email'
# Additional audiences allowed to pass audience verification
      oidc_extra_audience: ''
# Which OIDC claim contains the user groups (default "groups")
      oidc_groups_claim: 'groups'
# OpenID Connect issuer URL (ie: https://accounts.google.com)
      oidc_issuer_url: ''
# OpenID Connect JWKS URL (ie: https://www.googleapis.com/oauth2/v3/certs)
      oidc_jwks_url: ''
# Pass OAuth access_token to upstream via 'X-Forwarded-Access-Token' header
      pass_access_token: 'true'
# Pass the Authorization Header to upstream
      pass_authorization_header: 'true'
# Pass HTTP Basic Auth, X-Forwarded-User and X-Forwarded-Email information to
# upstream (default is 'true')
      pass_basic_auth: 'true'
# Pass the request Host Header to upstream (default is 'true')
      pass_host_header: 'true'
# Pass 'X-Forwarded-User' and 'X-Forwarded-Email' information to upstream
# (default 'true')
      pass_user_headers: 'true'
# The ping endpoint that can be used for basic health checks (default '/ping')
      ping_path: '/ping'
# Special User-Agent that will be used for basic health checks
      ping_user_agent: ''
# Prefer to use the e-mail address as the username when passing information to
# upstream. Will only use username if e-mail is unavailable, eg. htaccess
# authentication. Used in conjunction with 'pass_basic_auth' and
# 'pass_user_headers'
      prefer_email_to_user: 'true'
# Profile access endpoint
      profile_url: ''
# OIDC prompt
      prompt: ''
# OAuth provider (default is 'google')
      provider: 'google'
# One or more paths to CA certificates that should be used when connecting to
# the provider. If not specified, the default Go trust sources are used instead
      provider_ca_file: ''
# Provider display name
      provider_display_name: ''
# The url root path that this proxy should be nested under (default is
# '/oauth2')
      proxy_prefix: '/oauth2'
# Enables WebSocket proxying (default is 'true')
      proxy_websockets: 'true'
# JWK pubkey access endpoint: required by login.gov
      pubjwk_url: ''
# The ready endpoint that can be used for deep health checks (default '/ready')
      ready_path: ''
# Header used to determine the real IP of the client, one of: 'X-Forwarded-For',
# 'X-Real-IP', or 'X-ProxyUser-IP' (default is 'X-Real-IP')
      real_client_ip_header: 'X-Real-IP'
# Token redemption endpoint
      redeem_url:
        'https://sso.example.com/auth/realms/example/protocol/openid-connect/token'
# The OAuth Redirect URL
      redirect_url: 'https://internalapp.yourcompany.com/oauth2/callback'
# Redis custom CA path
      redis_ca_path: ''
# List of Redis cluster connection URLs (eg
# 'redis://[USER[:PASSWORD]@]HOST[:PORT]'). Used in conjunction with
# 'redis_use_cluster'
      redis_cluster_connection_urls: ''
# Redis connection idle timeout seconds, if Redis timeout option is non-zero,
# the 'redis_connection_idle_timeout' must be less then Redis timeout option
      redis_connection_idle_timeout: ''
# URL of Redis server for Redis session storage (eg:
# redis://[USER[:PASSWORD]@]HOST[:PORT]')
      redis_connection_url: ''
# Use insecure TLS connection to Redis
      redis_insecure_skip_tls_verify: 'false'
# Redis password. Applicable for all Redis configurations. Will override any
# password set in 'redis_connection_url'
      redis_password: ''
# List of Redis sentinel connection URLs (eg
# 'redis://[USER[:PASSWORD]@]HOST[:PORT]'). Used in conjunction with
# 'redis_use_sentinel'
      redis_sentinel_connection_urls: ''
# Redis sentinel master name. Used in conjunction with 'redis_use_sentinel'
      redis_sentinel_master_name: ''
# Redis sentinel password. Used only for sentinel connection, any Redis node
# passwords need to use 'redis_password'
      redis_sentinel_password: ''
# Connect to Redis cluster. Must set 'redis_cluster_connection_urls' to use this
# feature
      redis_use_cluster: 'true'
# Connect to Redis via sentinels. Must set 'redis_sentinel_master_name' and
# 'redis_sentinel_connection_urls' to use this feature
      redis_use_sentinel: 'true'
# Redis username. Applicable for Redis configurations where ACL has been
# configured. Will override any username set in 'redis_connection_url'
      redis_username: ''
# Allow relative OAuth Redirect URL
      relative_redirect_url: 'true'
# Request header to use as the request ID (default is 'X-Request-Id')
      request_id_header: 'X-Request-Id'
# Log HTTP requests (default is 'true')
      request_logging: 'true'
# Template for HTTP request log lines (default is '{{.Client}} - {{.RequestID}}
# - {{.Username}} [{{.Timestamp}}] {{.Host}} {{.RequestMethod}} {{.Upstream}}
# {{.RequestURI}} {{.Protocol}} {{.UserAgent}} {{.StatusCode}}
# {{.ResponseSize}} {{.RequestDuration}}')
      request_logging_format: ''
# The resource that is protected (Azure AD only)
      resource: ''
# Are we running behind a reverse proxy, controls whether headers like
# 'X-Real-Ip' are accepted
      reverse_proxy: ''
# OAuth scope specification
      scope: ''
# Strip OAuth tokens from cookie session stores if they aren't needed (cookie
# session store only)
      session_cookie_minimal: 'true'
# The session storage provider to use (default 'cookie')
      session_store_type: 'cookie'
# Set Authorization response headers
      set_authorization_header: 'true'
# Set HTTP Basic Auth information in response
      set_basic_auth: 'true'
# Set 'X-Auth-Request-User' and 'X-Auth-Request-Email' response headers
      set_xauthrequest: 'true'
# Show detailed error information on error pages (WARNING: this may contain
# sensitive information - do not use in production)
      show_debug_on_error: 'false'
# GAP-Signature request signature key
      signature_key: ''
# Disable logging of requests to ping & ready endpoints
      silence_ping_logging: 'true'
# Will skip authentication for OPTIONS requests
      skip_auth_preflight: 'true'
# Bypass authentication for requests that match the method & path.
# Format: 'method=path_regex' OR 'method!=path_regex'. For all methods:
# 'path_regex' OR '!=path_regex'
      skip_auth_route: ''
# Strips 'X-Forwarded-*' style authentication headers & Authorization header if
# the y would be set by oauth2-proxy (default is 'true')
      skip_auth_strip_headers: 'true'
# Skip loading missing claims from profile URL
      skip_claims_from_profile_url: 'true'
# Will skip requests that have verified JWT bearer tokens (default 'false')
      skip_jwt_bearer_tokens: 'false'
# Skip OIDC discovery and use manually supplied Endpoints
      skip_oidc_discovery: 'true'
# Will skip sign-in-page to directly reach the next step: oauth/start
      skip_provider_button: 'true'
# Skip validation of certificates presented when using HTTPS providers
      ssl_insecure_skip_verify: 'true'
# Skip validation of certificates presented when using HTTPS upstreams
      ssl_upstream_insecure_skip_verify: 'true'
# Log standard runtime information (default 'true')
      standard_logging: 'true'
# Template for standard log lines (default '[{{.Timestamp}}] [{{.File}}]
# {{.Message}}')
      standard_logging_format: ''
# Path to certificate file
      tls_cert_file: ''
# Restricts TLS cipher suites to those listed
      tls_cipher_suite: ''
# Path to private key file
      tls_key_file: ''
# Minimal TLS version for HTTPS clients (either 'TLS1.2' or 'TLS1.3')
      tls_min_version: ''
# List of IPs or CIDR ranges to allow to bypass authentication
      trusted_ip: ''
# List of IPs or CIDR ranges that are allowed to set 'X-Forwarded-*' headers
# when reverse proxy is enabled
      trusted_proxy_ip: ''
# The http url(s) of the upstream endpoint, file:// paths for static files or
# static://<status_code> for static response. Routing is based on the path
      upstream: ''
# Maximum amount of time the server will wait for a response from the upstream
# (default is '30s')
      upstream_timeout: '30s'
# Determines if 'provider_ca_file' files and the system trust store are used. If
# set to 'true', your custom CA files and the system trust store are used
# otherwise only your custom CA files
      use_system_trust_store: 'true'
# Access token validation endpoint
      validate_url:
        'https://sso.example.com/auth/realms/example/protocol/openid-connect/userinfo'
# Print version string
      version: ''
# Allowed domains for redirection after authentication. Prefix domain with a '.'
# or a '*.' to allow subdomains (eg '.example.com', '*.example.com')
      whitelist_domain: ''
```
