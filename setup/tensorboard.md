# Tensorboard

## インストール
* tensorflow入れると勝手に入る
    ```
    pip install tensorflow
    ```

* 確認
     ```
     pip list | find "tensor"
     ```
     ```
     tensorboard               1.14.0                   pypi_0    pypi
     tensorboard-plugin-wit    1.6.0.post3              pypi_0    pypi
     tensorflow-estimator      1.14.0                   pypi_0    pypi
     tensorflow-gpu            1.14.0                   pypi_0    pypi
     ```

* plugin-witをアンインストールする(これが邪魔)
  ```
  pip uninstall tensorboard-plugin-wit
  ```
## 起動
* ログ(tfevents)のディレクトリを指定して起動
  ```
  tensorboard --logdir=LOGDIR
  ```
  以下が表示される
  ```
  TensorBoard 1.14.0 at http://DESKTOP-PQ5F7I1:6006/ (Press CTRL+C to quit)
  ```
 * "http://localhost:6006/"にブラウザからアクセスする