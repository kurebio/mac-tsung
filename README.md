Macとtsungで手軽にHTTP負荷テスト

[こちらの記事](https://qiita.com/kurebio/items/2eac819962f7886bae4a)用のリポジトリです｡

# tsungインストール

``` sh
$ brew install tsung # tsung本体
$ tsung -v
$ sudo cpan Template # Template-Toolkitのインストール
# インストール時の質問は全て[y]または[Enter]で答えれば大丈夫でした
```

## `$ which perl`が`/usr/bin/perl`以外の場合は以下も実行

``` sh
$ chmod u+w /usr/local/lib/tsung/bin/tsung_stats.pl # 書込権限付与
```

``` diff
@@ -1,4 +1,4 @@
-#!/usr/bin/perl -w
+#!/usr/local/bin/perl -w
```

``` sh
$ chmod u-w /usr/local/lib/tsung/bin/tsung_stats.pl # 書込権限削除
```

# 負荷テスト実行

``` sh
$ git clone https://github.com/kurebio/mac-tsung.git
$ vi tsung.xml # テスト先サーバなどを指定

$ tsung -f ./tsung.xml -l log start # 負荷テスト実行
Starting Tsung
Log directory is: ~/tsung/log/[YYYYMMDD-HHMM]
[os_mon] cpu supervisor port (cpu_sup): Erlang has closed

# 最新のログを集計し､レポートをブラウザで開く 上記負荷テスト実行と繋げても良し
$ cd ./log/`ls -t log | head -n 1` && \
  /usr/local/lib/tsung/bin/tsung_stats.pl && \
  open report.html && \
  cd ../../
```

