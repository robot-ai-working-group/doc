# DQL_GRASPING
## インストール
* リポジトリからclone
    ```
    https://github.com/google-research/google-research.git
    ```
* 必要な環境をインストール
    ```
    pip install -r dql_grasping/requirements.txt
    ```
* gpu使う場合はtensorflow gpu版をインストール(CPU版はアンインストール)
    ```
    pip uninstall tensorflow
    pip install tensorflow-gpu=1.14
    ```

## 起動
* まずこいつ
    ```
    sh dql_grasping/run_random_collect_oss.sh
    ```

* 終わったらこいつ
    ```
    sh dql_grasping/run_train_collect_eval_oss.sh
    ```

## パラメータ
### 1. レンダリング(学習中にpybulletのレンダリングを行う)
* 環境のコンフィグを開く
    ```
    gedit dql_grasping/config/env_procedure/grasping_env.gin
    ```
* "DIRECT" → "GUI"に変更
    ```
    test/KukaGraspingProceduralEnv.render_mode = "GUI"
    ```
### 2. 学習モデルの変更
* バッチを開くアクセス
    ```
    gedit dql_grasping/run_train_collect_eval_oss.sh
    ```
* モデルを変更(dqn/ddpg/…etc?)
    ```
    EXPT="dqn"
    ```
* ポリシーを変更(onpolicy/offpolicy)
    ```
    TRAIN_MODE="onpolicy"
    ```
### 3. 各モデルのパラメータ変更
* 各モデルのコンフィグを開く(train_*.gin)
    ```
    gedit /dql_grasping/configs/env_procedural/train_ddpg.gin
    ```
### 4. パラメータ
* 最大学習ステップ
    ```
    train_ddpg.max_training_steps = 2000000
    ```
* 学習率
    ```
    actor/AdamOptimizer.learning_rate = 0.001
    critic/AdamOptimizer.learning_rate = 0.001
    ```
    
