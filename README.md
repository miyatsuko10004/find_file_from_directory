# ディレクトリ内から該当の文字列を含むもののファイル名を取得
find /home -type f -exec grep -F -l "hogehoge" {} +

# 上記、100ファイルごとにgrepしてメモリ容量考慮
## xargs -0 -n 100: NULL文字で区切られた入力を受け取り、100ファイルずつgrepに渡します。

* -F: 固定文字列として"yjtag"を検索（正規表現を使用しない）
* -l: マッチしたファイル名のみを出力
find /home -type f -print0 | xargs -0 -n 100 grep -F -l "yjtag"

# 並列処理で高速化
## xargs に -P $(nproc) オプションを追加:
* $(nproc) はシステムで利用可能なCPUコア数を取得します。
* -P オプションは、そのコア数だけ並列でgrepプロセスを実行します。
  
find /home -type f -print0 | xargs -0 -P $(nproc) -n 100 grep -F -l "ytag"
