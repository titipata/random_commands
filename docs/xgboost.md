# Install XGBoost

This is a not to install `xgboost` the popular Machine Learning algorithm for
Kaggle. Basically, we have to follow [installation page](https://xgboost.readthedocs.io/en/latest/build.html#build-the-shared-library).

```
git clone --recursive https://github.com/dmlc/xgboost
cd xgboost
```

I made changes `make/config.mk` as follows

```
export CC = gcc-5
export CXX = g++-5
```

After change config file, we can compile the library using `make`

```
cp make/config.mk ./config.mk
make -j4
```

Afterward, I can now install `xgboost` for python,

```
cd python-package/
python setup.py install
```
