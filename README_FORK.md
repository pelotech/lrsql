```shell
# uberjar, copies bin scripts, config, admin UI, docs, etc. into target/bundle/.
make clean && make bundle BUNDLE_RUNTIMES=false
# local validation
docker-compose up
# deployed validation
docker buildx build --platform linux/amd64 -t ghcr.io/pelotech/lrsql:latest --push .
# stable tag / ship it!
docker buildx imagetools create \
  ghcr.io/pelotech/lrsql:latest \
  --tag ghcr.io/pelotech/lrsql:fix-atomic-etag-validation
```