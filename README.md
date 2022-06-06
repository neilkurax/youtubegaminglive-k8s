
Secrets encripted using kubeseal

Actual real values were replaced of course.


```bash
kubectl -n youtubegaminglive \
  create secret generic soketi \
  --dry-run=client \
  --from-literal PUSHER_APP_ID=foo \
  --from-literal PUSHER_APP_KEY=bar \
  --from-literal PUSHER_APP_SECRET=ultrasecret \
  --output yaml | kubeseal -o yaml | tee soketi/templates/secrets.yaml
```

Secret for mariadb passwords:
```bash
kubectl -n youtubegaminglive \
  create secret generic mariadb-secrets \
  --dry-run=client \
  --from-literal mariadb-password="secret" \
  --from-literal mariadb-root-password="supersecret" \
  --from-literal mariadb-replication-password="supersupersecret" \
  --output yaml | kubeseal -o yaml
```

Secret for laravel:
```bash
kubectl -n youtubegaminglive \
  create secret generic laravel \
  --dry-run=client \
  --from-literal APP_KEY="base64:keykey" \
  --from-literal MAILERSEND_HOST=smtp.host.com \
  --from-literal MAILERSEND_PORT=587 \
  --from-literal MAILERSEND_USERNAME="user" \
  --from-literal MAILERSEND_PASSWORD="pass" \
  --from-literal YOUTUBE_KEY_ID="" \
  --from-literal YOUTUBE_CLIENT_ID="" \
  --from-literal YOUTUBE_CLIENT_SECRET="" \
  --from-literal YOUTUBE_REDIRECT_URI="/youtube/callback" \
  --output yaml | kubeseal -o yaml | tee laravel/templates/secrets.yaml
```

Secret for github webhook:

```bash
kubectl -n argo-events \
  create secret generic event-youtubegaminglive-laravel-github-secret \
  --dry-run=client \
  --from-literal secret="random pass" \
  --output yaml | kubeseal -o yaml
```

Secret for crawler signature:

```bash
kubectl -n youtubegaminglive \
  create secret generic crawler \
  --dry-run=client \
  --from-literal INTERNAL_API_SIG="random" \
  --output yaml | kubeseal -o yaml | tee crawler/templates/secrets.yaml
```
