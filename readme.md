# Hydra Flow Workbench

**Interactive OAuth 2.0 / OIDC Flow Laboratory for ORY Hydra**

An interactive, browser-based workbench for manually executing, configuring, inspecting, and troubleshooting OAuth 2.0 and OpenID Connect authorization flows with ORY Hydra.

## Overview

**Hydra Flow Workbench** is an engineering tool designed to explore the complete OAuth 2.0 / OIDC Authorization Code Flow through a visual web interface.

Unlike conventional OAuth clients that execute authorization flows automatically, Hydra Flow Workbench gives engineers **direct control over key protocol stages**, allowing them to modify request parameters, inspect ORY Hydra responses, and observe the results of individual operations.

The application provides an interactive interface for working with both ORY Hydra's public OAuth 2.0 / OIDC endpoints and its administrative API.

**This is not just another OAuth login demo.**

It is a hands-on environment for understanding protocol behavior, debugging integrations, testing configurations, and experimenting with authorization flows.

## Key Features

### 1. Authorization Request Initialization

- Build and initiate OAuth 2.0 / OIDC authorization requests directly from your browser.
- Configure authorization request parameters.
- Work with `client_id`, `redirect_uri`, `scope`, `state`, and other OAuth parameters.
- Execute the Authorization Code Flow.
- Experiment with PKCE (Proof Key for Code Exchange).

### 2. Interactive Login Flow

- Retrieve and inspect `login_challenge` data.
- Examine authentication request parameters.
- Manually configure login acceptance parameters.
- Accept or reject authentication requests through the ORY Hydra Admin API.
- Explore `subject`, `acr`, `amr`, `remember`, and other login attributes.

### 3. Interactive Consent Flow

- Retrieve and inspect `consent_challenge` data.
- Examine requested OAuth scopes.
- Configure granted scopes and token audiences.
- Modify session attributes and token claims.
- Accept or reject consent requests through the ORY Hydra Admin API.

### 4. Authorization Code Exchange

- Handle OAuth redirect callbacks through `redirect_uri`.
- Receive authorization codes.
- Exchange authorization codes for tokens.
- Inspect responses from the `/oauth2/token` endpoint.
- Examine authorization errors and protocol responses.

### 5. Token Inspection and Validation

- Inspect issued access tokens, ID tokens, and refresh tokens when available.
- Decode JWT (JSON Web Token) payloads.
- Validate supported JWT tokens using JWKS (JSON Web Key Sets).
- Examine token claims and attributes.
- Inspect expiration times and token metadata.

### 6. Logout Flow Exploration

- Explore session termination requests.
- Inspect and process `logout_challenge` data.
- Interact with ORY Hydra's administrative endpoints.
- Test logout and post-logout redirect behavior.
- Examine back-channel logout requests.

## Who Is It For?

Hydra Flow Workbench is intended for:

- Solution and system architects.
- OAuth 2.0 / OpenID Connect developers.
- Identity and Access Management (IAM) engineers.
- Application security specialists.
- Engineers learning ORY Hydra and OAuth authorization mechanisms.

It is particularly useful when you need to understand **what happens at each stage of an authorization flow**, rather than simply checking whether authentication succeeds.

## Technology Stack

| Component | Technology |
|---|---|
| Backend | Python, FastAPI |
| Frontend | HTML, CSS, JavaScript |
| Authorization server | ORY Hydra |
| HTTP client | HTTPX |
| Containerization | Docker, Docker Compose |
| Reverse proxy | Nginx |
| JWT validation | JWKS |

## Requirements

- Docker.
- Docker Compose v2 or later.

Verify your Docker Compose installation:

```bash
docker compose version
```

## Installation and Deployment

Clone the repository:

```bash
git clone https://github.com/log-box/hydraFlowClient.git
cd hydraFlowClient
```

Configure the `.env` file for your environment.

Ensure that the ORY Hydra configuration, service URLs, and registered OAuth clients match your deployment.

Build and start the containers:

```bash
docker compose up -d --build
```

View container logs:

```bash
docker compose logs -f
```

The application provides a browser-based interface for initiating authorization requests, managing login and consent flows, processing redirects, inspecting tokens, and exploring session termination.

**Note:** Hydra Flow Workbench is intended for engineering experiments and controlled testing environments. Do not expose ORY Hydra administrative endpoints or deploy the example configuration to an untrusted environment without appropriate security controls.

## Web Interface

The workbench includes the following interactive pages:

| Page | Purpose |
|---|---|
| Authorization Request | Configure and initiate OAuth 2.0 / OIDC authorization flows |
| Login Request | Inspect and manually process authentication requests |
| Consent Request | Configure and process authorization consent |
| Redirect Result | Inspect authorization codes, issued tokens, and errors |
| Logout Request | Explore session termination and logout operations |
| Logout Result | Inspect logout results and redirects |

## Project Structure

```text
hydraFlowClient/
├── .env
├── docker-compose.yml
├── Dockerfile
├── app/
│   ├── main.py
│   ├── config.py
│   ├── logger.py
│   ├── schemas.py
│   ├── api/
│   │   ├── login.py
│   │   ├── consent.py
│   │   ├── logout.py
│   │   └── redirect.py
│   ├── core/
│   │   ├── context.py
│   │   ├── context_storage.py
│   │   ├── hydra.py
│   │   ├── token_payload.py
│   │   └── database.py
│   ├── static/
│   │   ├── auth_form.html
│   │   ├── login.html
│   │   ├── consent.html
│   │   ├── logout.html
│   │   └── logout_successful.html
│   └── templates/
│       └── redirect_result.html.jinja
├── hydra/
│   └── config/
│       └── hydra.yml
├── init/
│   └── createClients.py
├── nginx/
│   └── etc/nginx/conf.d/
└── requirements.txt
```

## Use Cases

### OAuth 2.0 / OIDC Troubleshooting

Execute authorization flows step by step while inspecting request parameters, Hydra responses, and redirect behavior.

### Login and Consent Experimentation

Manually adjust authentication and consent parameters to understand how they affect authorization results and issued tokens.

### OAuth Client Configuration Testing

Investigate client registration settings, scopes, redirect URIs, token audiences, and authorization parameters.

### Token Analysis

Examine the structure, claims, and validation results of issued tokens.

### Logout and Session Termination Testing

Explore logout requests, session termination, redirects, and interactions with ORY Hydra's Admin API.

## Security Considerations

Hydra Flow Workbench is a protocol exploration and diagnostic tool, **not a production-ready authentication system**.

Some features intentionally expose direct control over parameters that should be managed by trusted application logic in production environments.

For safe use:

- Run the application in a trusted development or testing environment.
- Restrict access to ORY Hydra's administrative API.
- Avoid using real user credentials during experiments.
- Never commit active OAuth client secrets or other sensitive credentials to the repository.
- Do not treat diagnostic token processing or in-memory flow state as production-grade session management.
- Review configuration and exposed endpoints before enabling remote access.

## Resources

- [ORY Hydra](https://www.ory.com/hydra/)
- [ORY Documentation](https://www.ory.com/docs/)
- [GitHub Repository](https://github.com/log-box/hydraFlowClient)

---

**Hydra Flow Workbench**

*Explore, customize, and manually execute OAuth 2.0 / OIDC authorization flows directly in your browser.*

**Take control of every stage of the authorization process.**
