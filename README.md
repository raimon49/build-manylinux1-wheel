# build-manylinux1-wheel

## Build manylinux wheel by command-line

```bash
# Dockerコンテナの中でsdistパッケージを取得してwheelをビルド
$ docker run --rm -v $PWD/wheelhouse:/io/wheelhouse quay.io/pypa/manylinux1_x86_64 /opt/python/cp36-cp36m/bin/pip wheel -w /io/wheelhouse "SQLAlchemy==1.2.2"

# Dockerコンテナ環境用にビルドされたwheelパッケージをmanylinux wheelパッケージに変換
$ docker run --rm -v $PWD/wheelhouse:/io/wheelhouse quay.io/pypa/manylinux1_x86_64 auditwheel repair /io/wheelhouse/SQLAlchemy-1.2.2-cp36-cp36m-linux_x86_64.whl -w /io/wheelhouse
```

## Build manylinux wheel by requirements.txt and script

```bash
# requirements.txtで宣言したパッケージ全てをauditwheelするビルドスクリプトを実行
$ docker run --rm -v $PWD:/io quay.io/pypa/manylinux1_x86_64 /io/build-wheels
```

## Cleanup

```bash
$ docker images | grep manylinux1_x86_64 | sed 's/\s\{1,\}/ /g' | cut -d' ' -f3 | xargs docker rmi
```
