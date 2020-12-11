# Chromeリモートデスクトップ
## ホスト側(Ubuntu20.04 LTS)
### 1. インストール
chromeリモートデスクトップをインストール
```
cd $HOME/Download
sudo dpkg -i chrome-remote-desktop_current_amd64.deb
sudo apt-get install -f
```
カレントユーザをグループに追加
```
sudo usermod -a -G chrome-remote-desktop $USER
sudo reboot
```

### 2. Chromeリモートデスクトップの修正
サービスの停止
```
sudo systemctl stop chrome-remote-desktop.service
```
バックアップ
```
sudo cp /opt/google/chrome-remote-desktop/chrome-remote-desktop /opt/google/chrome-remote-desktop/chrome-remote-desktop.orig
```
chromeリモートデスクトップを編集
```
sudo gedit /opt/google/chrome-remote-desktop/chrome-remote-desktop
```
以下を編集
```
FIRST_X_DISPLAY_NUMBER = 1
```
> echo $DISPLAYを実行した返値

```
@staticmethod
  def get_unused_display_number():
    """Return a candidate display number for which there is currently no
    X Server lock file"""
    display = FIRST_X_DISPLAY_NUMBER
    # while os.path.exists(X_LOCK_FILE_TEMPLATE % display):
    #   display += 1
    return display
```
```
def launch_session(self, x_args):
    self._init_child_env()
    self._setup_pulseaudio()
    self._setup_gnubby()
    # self._launch_x_server(x_args)
    # self._launch_x_session()
    display = self.get_unused_display_numbsudo systemctl restart chrome-remote-desktop.serviceer()
    self.child_env["DISPLAY"] = ":%d" % display
```
エディタを閉じてchromeリモートデスクトップを再起動
```
sudo systemctl restart chrome-remote-desktop.service
```
### 3. 仮想デスクトップセッションのカスタマイズ
デスクトップ環境ファイルを開く
```
sudo gedit usr/share/xsessions/ubuntu.desktop 
```
> Exec=のあとがセッション開始コマンド

ホームディレクトリに「.chrome-remote-desktop-session」というファイルを作成し「exec /etc/X11/Xsession 'セッション開始コマンド'」を記載  

### 4. Chromeリモートデスクトップの有効化
アプリからChromeリモートデスクトップを開いて、「リモートデスクトップを有効にする」をクリックする  
6桁のPINを設定してする

## ゲスト側
### 接続
ゲストPCからChromeを立ち上げて、ブラウザのchromeリモートデスクトップ拡張機能からPINを入力して接続する

## 参考
> Chromeリモートデスクトップ  
> https://xvideos.hatenablog.com/entry/chrome-remote-desktop-ubuntu1804

> Googleヘルプ  
> https://support.google.com/chrome/answer/1649523#linux-crd