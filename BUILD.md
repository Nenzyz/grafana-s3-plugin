docker run -ti --rm -v `pwd`:/app golang:1.14 bash

apt update && apt upgrade -y --auto-remove
apt install npm -y
npm install -g yarn --quiet
curl -fsSL https://deb.nodesource.com/setup_12.x | bash -

yarn install --pure-lockfile
npx grafana-toolkit plugin:build

go mod download
<!-- go build pkg/*.go -->

env GOOS=linux GOARCH=amd64 go build -o dist/gpx_s3_plugin_linux_amd64 pkg/*.go
env GOOS=darwin GOARCH=amd64 go build -o dist/gpx_s3_plugin_darwin_amd64 pkg/*.go
env GOOS=windows GOARCH=amd64 go build -o dist/gpx_s3_plugin_windows_amd64 pkg/*.go