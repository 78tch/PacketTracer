# PacketTracer
Cisco Packet Tracer の7.2.1をUbuntu 18.10 で動かす手順です。
あまりバージョンアップが活発ではないと思っていたらいつのまにか7.2.1になり、18.10 への対応を期待したのですが、やはり16.04向けという扱いのようで、ライブラリのバージョンが合わずエラーになりますので、このあたりのWorkaround を書いておきたいと思います。  
  
1. Cisco Networking Academy から「Packet Tracer 7.2.1 for Linux 64 bit.tar.gz」をダウンロードする。  
<img src="images/01.png" alt="image">  
  
2. 適当なフォルダーを作ってそのなかに展開する。  
<img src="images/02.png" alt="image">  
  
3. インストールする。  
```sh
$ cd ~/PT  
$ ./install  
```  
<img src="images/03.png" alt="image">  
  
4. 途中で「/opt に/pt ってフォルダ作って中にファイルをコピーするのに、sudo する？」って訊かれるので入力。  
<img src="images/04.png" alt="image">  
  
5. 「/usr/local/bin にシンボリックリンク作る？」と訊かれるのでyを押下。
<img src="images/05.png" alt="image">  
  
6. さっそく、「/opt/pt/bin」に移って起動させてみるが、「error while loading shared libraries: libpng12.so.0: cannot open shared object file: No such file or directory」となる。7.2.1 になって、7.1 の時よりはエラーが少なくなってる感じはする。
<img src="images/06.png" alt="image">  
  
7. 対応として、おとなしく16.04にインストールして使う、という手もあると思いますが、それは特にひっかかるところなくインストールできるので、ここでは、あえて18.10 でなんとかする方法を。「libpng12 ubuntu」でググると、Debian とかUbuntu のパッケージダウンロードサイトとかがあるようなので、そこからなるべく良さげ（抽象的）なのをダウンロードします。私は  
https://packages.ubuntu.com/xenial/libpng12-0  
  からダウンロードしました。
<img src="images/07.png" alt="image">  
<img src="images/08.png" alt="image">  
<img src="images/09.png" alt="image">  
<img src="images/10.png" alt="image">  
  
8. ダウンロードしてきたファイルをダブルクリックなどするとUbuntu ソフトウェアで開くので、インストールします。
<img src="images/11.png" alt="image">  
  
9. 改めてPacketTracer を起動してみると、今度はうまくいきそうです。「初回起動なんで、ユーザーファイルを/home/hogehoge/pt 配下に保存しますよ。」と言われます。
<img src="images/12.png" alt="image">  
  
10. 次に、「Cisco Networking Academy」のアカウントでのログインを求められます。これをせずに「Guest Login」することもできますが、その場合はファイル保存ができないなど利用が限定されてしまいます。アカウントはサイトで無料で作成できます。
<img src="images/13.png" alt="image">  
  
11. 無事起動しました！見た目ちょっと変わった？  
と、これでもういいのですが・・・
<img src="images/14.png" alt="image">  
  
12. このままだと、デスクトップアイコンがなかったり、スタートメニューショートカットがないので、作っていきます。  
<img src="images/15.png" alt="image">  
  
13. 「/opt/pt/bin」にある「Cisco-PacketTracer.desktop」を「~/デスクトップ」にコピーして、一部を書き換えます。
```sh
$ cd /opt/pt/bin
$ cp Cisco-PacketTracer.desktop ~/デスクトップ
$ gedit ~/デスクトップ/Cisco-PacketTracer.desktop
```  
<img src="images/16.png" alt="image">  
  
14.「Exec=packettracer」のパスを「Exec=/opt/pt/packettracer」に直します。  
<img src="images/17.png" alt="image">  
  
15. ファイルに実行権を付与します。  
```sh
$ chmod +x ~/デスクトップ/Cisco-PacketTracer.desktop
```  
<img src="images/18.png" alt="image">  

16. 警告がでますが、OKすると、アイコンができます！  
<img src="images/19.png" alt="image">  
<img src="images/20.png" alt="image">  
  
17. さらにこのアイコンを、アプリボタンを押下したときにも出てくるようにします。  
```sh
$ cp ~/デスクトップ/Cisco-PacketTracer.desktop /usr/share/applications/
```  
「お気に入りに追加」すれば、Dock に出てきます。
<img src="images/21.png" alt="image">  
<img src="images/22.png" alt="image">  
  
以上です。enjoy!
