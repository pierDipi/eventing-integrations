# JSON Transformations

```text

source or webhook -> transform -> broker

trigger -> transform -> sink or webhook

broker -> trigger -> (request)  -> transform
broker <- trigger <- (response) <-
```

## Development

Assuming current working directory is `transform-jsonata`

```shell
pnpm dev

# or pnpm dev-kubevirt to inject a different example transformation
```

## Building

Assuming current working directory is `transform-jsonata`

```shell
IMAGE_NAME=...
docker build -t "${IMAGE_NAME}" -f Dockerfile . 
docker push "${IMAGE_NAME}"
```

### Running

```shell
docker run --user $(id -u):$(id -g) -ti --rm --mount src="$(pwd)/examples",dst=/var/examples,type=bind -e NODE_ENV=development -e JSONATA_TRANSFORM_FILE_NAME=/var/examples/ce_apiserversource_kubevirt.jsonata -p 8080:8080 "${IMAGE_NAME}"
```

### Testing the example

```shell
curl -v -XPOST http://localhost:8080 -d @examples/ce_apiserversource_kubevirt.json
```

## Testing transformations

https://try.jsonata.org/