# Reproducing the slow FP32 training

```bash
# !! assuming to be within the docker image that Gabe builds

# environment setup
git init google-research
cd google-research
git remote add origin https://github.com/jingyang-kylist/google-research.git
git sparse-checkout init --cone
git sparse-checkout set imp
git fetch --filter=blob:none --no-tags origin vit-test
git checkout vit-test

python -m pip install -r imp/requirements.txt --use-deprecated=legacy-resolver
python -m pip install git+https://github.com/jingyang-kylist/CLIP.git --no-deps
python -m pip install ftfy importlib_resources

# run with configurable MODEL_DTYPE and BATCH_SIZE
MODEL_DTYPE=fp32 BATCH_SIZE=832 python -m imp.max.projects.imp.main --config_name=vit_huge.img.train
```
