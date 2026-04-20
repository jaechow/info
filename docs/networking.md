# Networking & Security

Debug APIs, manage SSH, inspect certificates, probe networks.

## curl — Modern Patterns

POST JSON (the `--json` flag sets Content-Type and method automatically):

```shell
curl --json '{"name":"test"}' https://api.example.com/users
```

Measure request timing:

```shell
curl -o /dev/null -s -w "DNS: %{time_namelookup}s\nConnect: %{time_connect}s\nTLS: %{time_appconnect}s\nTotal: %{time_total}s\n" https://example.com
```

Follow redirects and show response headers:

```shell
curl -sSL -D - https://example.com -o /dev/null
```

Download with retry and resume:

```shell
curl -LC - --retry 3 -o file.zip https://example.com/file.zip
```

---

## httpie — Human-Friendly HTTP

GET request with automatic formatting:

```shell
http https://api.example.com/users
```

POST with JSON body:

```shell
http POST https://api.example.com/users name=test email=test@example.com
```

Send with a bearer token:

```shell
http https://api.example.com/me Authorization:"Bearer $TOKEN"
```

> Install: `brew install httpie` · `pip install httpie`

---

## SSH

### Config File (`~/.ssh/config`)

```
Host myserver
    HostName 192.168.1.100
    User deploy
    IdentityFile ~/.ssh/id_ed25519
    Port 22

Host jump
    HostName bastion.example.com
    User admin

Host internal
    HostName 10.0.0.5
    ProxyJump jump
```

### Generate an Ed25519 key:

```shell
ssh-keygen -t ed25519 -C "you@example.com"
```

### Start the agent and add your key:

```shell
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### Copy public key to a server:

```shell
ssh-copy-id myserver
```

### Port forwarding (local):

Access remote port 5432 at localhost:5432:

```shell
ssh -L 5432:localhost:5432 myserver
```

### Tunnel through a jump host:

```shell
ssh -J jump internal
```

---

## OpenSSL — Certificate Inspection

View a remote server's TLS certificate:

```shell
echo | openssl s_client -connect example.com:443 -servername example.com 2>/dev/null | openssl x509 -noout -text
```

Check certificate expiration:

```shell
echo | openssl s_client -connect example.com:443 2>/dev/null | openssl x509 -noout -dates
```

Inspect a local certificate file:

```shell
openssl x509 -in cert.pem -noout -text
```

Verify a certificate chain:

```shell
openssl verify -CAfile ca-bundle.crt cert.pem
```

---

## DNS

Lookup DNS records with `dig`:

```shell
dig example.com A +short
dig example.com MX +short
dig example.com TXT +short
```

Trace DNS resolution path:

```shell
dig +trace example.com
```

### dog (modern DNS client)

```shell
dog example.com A AAAA MX
```

> Install: `brew install dog`

---

## Network Debugging

Which process is using a port:

=== "macOS"

    ```shell
    lsof -i :3000
    ```

=== "Linux"

    ```shell
    ss -tlnp | grep :3000
    ```

Test TCP connectivity:

```shell
nc -zv example.com 443
```

Scan open ports on a host:

```shell
nmap -sT -p 1-1000 192.168.1.1
```

!!! note
    Only scan hosts you own or have explicit permission to test.
