# Reproducing LLVM error

```bash
# !! assuming to be within the docker image that Gabe builds

# environment setup
git clone -n --depth=1 --filter=tree:0 https://github.com/jingyang-kylist/google-research.git
cd google-research
git sparse-checkout set --no-cone /imp; git checkout

python -m pip install -r imp/requirements.txt --use-deprecated=legacy-resolver
python -m pip install git+https://github.com/jingyang-kylist/CLIP.git --no-deps
python -m pip install ftfy importlib_resources

# 1. run imp training with batch size 1024 -> error
python -m imp.max.projects.imp.main --config_name=imp_large.img.train

# 2. modify imp/max/projects/imp/config/data.py:57 `BASE_TRAIN_BATCH_SIZE = 512`
#    run imp training with batch size 512 -> no error
python -m imp.max.projects.imp.main --config_name=imp_large.img.train
```
