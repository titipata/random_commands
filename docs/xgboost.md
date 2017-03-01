[back to home](../README.md)

# Install XGBoost on macOS

This is a not to install `xgboost` the popular Machine Learning algorithm for
Kaggle. Basically, we have to follow [installation page](https://xgboost.readthedocs.io/en/latest/build.html#build-the-shared-library).

```bash
git clone --recursive https://github.com/dmlc/xgboost
cd xgboost
```

After change config file, we can compile the library using `make`

```bash
cp make/minimum.mk ./config.mk
make -j4
```

Afterward, I can now install `xgboost` for python,

```bash
cd python-package/
python setup.py install
```
