# Copy keys

```shell
[[ ! -f ~/.keys/age.key ]] && curl -fsLS 'https://raw.githubusercontent.com/rvenutolo/crypt/main/keys/age.key' | age -d | install -D -m 600 /dev/stdin ~/.keys/age.key

keys=(
  'authorized_keys .ssh'
  'core-dev-general.pem .keys'
  'id_ed25519 .keys'
  'id_ed25519.pub .keys'
  'pihole .keys'
  'pihole.pub .keys'
)
for line in "${keys[@]}"; do
  IFS=' ' read -r file dir <<< "${line}"
  curl -fsLS "https://raw.githubusercontent.com/rvenutolo/crypt/main/keys/${file}" | age -di ~/.keys/age.key | install -D -m 600 /dev/stdin "~/${dir}/${file}"
done
```
