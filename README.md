
# VELD udpipe demo TS-Vienna 2024

This is a demo repo of the VELD design, for the CLSInfra Training School Vienna 2024.

## how to run

clone this repo, with submodules:
```
git clone --recurse-submodules https://github.com/acdh-oeaw/veld_udpipe_demo__ts-vienna_2024.git
```

change into the folder:
```
cd veld_udpipe_demo__ts-vienna_2024
```

verify that there is content in the submodule `veld_code_15_udpipe`
```
ls veld_code_15_udpipe # linux / mac
dir veld_code_15_udpipe # windows
```
It should print contents like this:
```
Dockerfile  src  veld_infer.yaml  veld_train.yaml  volumes
```


### training

Configuration for training is done in [./veld_train.yaml](./veld_train.yaml).

To run, simply do:
```
docker compose -f veld_train.yaml up
```
(or `docker-compose` (with a dash), depending on your install and version)

After training, a model will be persisted in [./veld_data_updipe_model](./veld_data_updipe_model/).

### use model for inference

Configuration for inference is done in [./veld_infer.yaml](./veld_infer.yaml).

To run, simply do:
```
docker compose -f veld_infer.yaml up
```

After that, an inferenced output conllu file can be found in
[./veld_data_inferenced](./veld_data_inferenced/).

