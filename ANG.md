./install.sh
source .venv/bin/activate

llmdbenchmark --spec config/specification/guides/kvc-fs-connector.yaml.j2 standup -p kvc-dev

llmdbenchmark --spec gpu run --endpoint-url http://llmdbench-inference-gateway-route-kvc-dev.apps.pokprod001.ete14.res.ibm.com:80 --model Qwen/Qwen3-32B --namespace kvc-dev --harness inference-perf --workload shared_prefix_synthetic.yaml --analyze -j4

llmdbenchmark --spec config/specification/guides/kvc-fs-connector.yaml.j2 teardown -p kvc-dev
