
# VELD udpipe demo TS-Vienna 2024

This is a demo repo of the VELD design, for the CLSInfra Training School Vienna 2024.

It demonstrates two processing chains: 
- training a [udpipe model](https://lindat.mff.cuni.cz/services/udpipe/) using a [conllu
  file](./veld_data_training/en_ewt-ud.conllu) as training data provided by
[universaldependencies](https://github.com/UniversalDependencies/UD_English-EWT/tree/master). The
output model will be saved at [./veld_data_updipe_model/](./veld_data_updipe_model/).
- using our self-trained model for inference on evaluation data, a simple [txt file
  "Rumpelstiltkin"](./veld_data_eval/rumpelstiltskin.txt) provided by
[pitt.edu](https://sites.pitt.edu/~dash/grimm055.html). The output conllu file will be saved at
[./veld_data_inferenced/](./veld_data_inferenced/).

## how to run

clone this repo, with submodules:
```
git clone --recurse-submodules https://github.com/acdh-oeaw/veld_udpipe_demo__ts-vienna-2024.git
```

change into the folder:
```
cd veld_udpipe_demo__ts-vienna_2024
```

verify that there is content in the submodule's folder `./veld_code_15_udpipe`:
```
ls veld_code_15_udpipe # linux / mac
dir veld_code_15_udpipe # windows
```

It should print contents like this:
```
Dockerfile  src  veld_infer.yaml  veld_train.yaml  volumes
```

Should there be no content in that folder, probably `git clone` wasn't used with `--recurse-submodules`. Pull the submodules manually then with:
```
git submodule update --init
```
And verify the contents of `veld_code_15_udpipe` as described above.


### training

Configuration for training is done in [./veld_train.yaml](./veld_train.yaml). All possible
configurations for this chain can be found at the [originating veld code repo's train.yaml](https://github.com/acdh-oeaw/veld_code_15_udpipe/blob/main/veld_train.yaml).

To run, simply do:
```
docker compose -f veld_train.yaml up
```
(or `docker-compose` (with a dash), depending on your install and version)

After training, a model will be persisted in [./veld_data_updipe_model](./veld_data_updipe_model/).

If you want to improve the training setup, the easiest thing to do is to increase the values of `tokenizer_epochs`, `tagger_iterations`, `parser_iterations` in your `veld_train.yaml`. This makes the training process take more time but delievers better results, generally. Other hyperparameter as described in the [originating veld code repo's train.yaml](https://github.com/acdh-oeaw/veld_code_15_udpipe/blob/main/veld_train.yaml), can be also tweaked but require deeper understanding of the training architecture.


### inference

Configuration for inference is done in [./veld_infer.yaml](./veld_infer.yaml). All possible
configurations for this chain can be found at the [originating VELD code repo's infer.yaml](https://github.com/acdh-oeaw/veld_code_15_udpipe/blob/main/veld_infer.yaml).

To run, simply do:
```
docker compose -f veld_infer.yaml up
```

After that, an inferenced output conllu file can be found in
[./veld_data_inferenced](./veld_data_inferenced/).

