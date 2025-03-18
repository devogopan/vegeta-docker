# Vegeta Docker

Docker image for the [Vegeta](https://github.com/tsenart/vegeta) HTTP load testing tool.

## Usage

To display help:
```bash
docker run --rm -i devogopan/vegeta
```
Example:
```bash
docker run --rm -i devogopan/vegeta sh -c \
"echo 'GET https://www.example.com' | vegeta attack -rate=10 -duration=30s | tee results.bin | vegeta report"
```
For full documentation see [Vegeta](https://github.com/tsenart/vegeta).

## Usage in Kubernetes

To display help:
```bash
kubectl run vegeta --rm --attach --restart=Never --image="devogopan/vegeta"
```
Example:
```bash
kubectl run vegeta --rm --attach --restart=Never --image="devogopan/vegeta" -- sh -c \
"echo 'GET https://www.example.com' | vegeta attack -rate=10 -duration=30s | tee results.bin | vegeta report"
```

```bash
# Start vegeta with nohup
echo "Starting load test..."
truncate -s 0 vegeta.out
nohup kubectl run vegeta --rm --stdin --restart=Never --image="devogopan/vegeta:v12.12.0" -- sh -c \
"echo 'GET https://nginx.aegle.info' | vegeta attack -insecure -rate=50 -duration=30s -connect-to=nginx.aegle.info:443:172.18.64.11:443 | tee results.bin | vegeta report " > vegeta.out 2>&1 &

echo "Load test started in background. You can check progress with: tail -f vegeta.out"

cat vegeta.out

```

## License

MIT License - see the [LICENSE](LICENSE) file for details
