# Universal Inbox

**Universal Inbox** is an open-source solution designed to centralize notifications and tasks from fragmented platforms into a single, unified workflow. Stop context-switching and manage your entire digital workspace from one unique inbox.

---

## 🚀 Key Features

### 🔄 Multi-Platform Synchronization

* **Notifications:** GitHub, Linear, Google Mail (with more coming).
* **Tasks:** Full integration with Todoist.
* **Bi-directional Sync:** Maintains state consistency between Universal Inbox and upstream services whenever the provider API allows.

### ⚡ Actionable Inbox

Take immediate action on notifications without leaving the interface:

* **Archive/Delete:** Remove notifications; new updates to the resource will trigger a fresh notification.
* **Unsubscribe:** Permanently silence a thread unless explicitly mentioned.
* **Snooze:** Temporarily hide items until the next day.
* **Task Conversion:** Transform any notification into a planned task in Todoist or link it to an existing one.

---

## 🛠 Development Setup

Universal Inbox uses **Devbox** (Nix-based) to ensure a consistent development environment across all machines.

### Prerequisites

1. **Install Devbox:** Follow the [official installation guide](https://www.jetpack.io/devbox/docs/quickstart/#install-devbox).
2. **Clone the Repository:**
```bash
git clone https://github.com/universal-inbox/universal-inbox.git
cd universal-inbox

```



### Environment Configuration

We recommend using [direnv](https://direnv.net/) to automatically load the environment:

```bash
direnv allow

```

*Alternatively, you can use the Devbox shell directly:*

```bash
devbox shell

```

### Database & Services

This project uses `just` as a command runner for common tasks.

1. **Start Infrastructure:** Start PostgreSQL and Redis:
```bash
just run-db

```


2. **Initialize Database:**
```bash
just migrate-db

```



---

## ⚙️ Configuration

### Authentication (OIDC)

Universal Inbox requires an OpenID Connect provider for user authentication. You can configure this via environment variables or a local config file at `api/config/local.toml`.

**Required Variables:**

```ini
AUTHENTICATION_OIDC_ISSUER_URL=https://your-oidc-provider.com
AUTHENTICATION_OIDC_FRONT_CLIENT_ID=your-client-id
AUTHENTICATION_OIDC_API_CLIENT_SECRET=your-secret

```

### Nango Integration

We use [Nango](https://github.com/NangoHQ/nango) to manage OAuth2 tokens. To enable integrations, you must register Universal Inbox as an OAuth2 app on each platform (GitHub, Google, etc.) and configure the credentials in the Nango dashboard.

* **Nango Dashboard:** `http://localhost:3003`
* **Default Dev Redirect:** `https://oauth-dev.universal-inbox.com`

---

## 🏗 Build & Run

**Build the full stack:**

```bash
just build-all

```

**Launch the application:**
*(Ensure `just run-db` is stopped first, as `run-all` handles database containers)*

```bash
just run-all

```

Once started, access the web interface at: **[http://localhost:8080](https://www.google.com/search?q=http://localhost:8080)**.

**Run Tests:**

```bash
just test-all

```

---

## 📄 License

Distributed under the **Apache 2 License**. See `LICENSE` for more information.

---

**Would you like me to help you generate a `CONTRIBUTING.md` file or a specific `docker-compose` setup for this project?**
