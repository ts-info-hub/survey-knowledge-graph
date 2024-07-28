# Nebula Graphの使い方

## Graphの構成要素

- Vertex: 頂点、ノード
- Edge: 線、関係
- Tag: プロパティ？
- Index: 検索を効率化するための情報

## インストール手順

- Nebula Graphの[Docker composeを使ったインストール手順](https://docs.nebula-graph.io/3.6.0/2.quick-start/1.quick-start-workflow/)

```bash
# インストール後のDockerの構成
❯ docker compose ps
WARN[0000] /home/tatsuya/repositories/tools/nebula-docker-compose/docker-compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
NAME                                IMAGE                                     COMMAND                  SERVICE     CREATED       STATUS                    PORTS
nebula-docker-compose-graphd-1      docker.io/vesoft/nebula-graphd:v3.6.0     "/usr/local/nebula/b…"   graphd      12 days ago   Up 14 minutes (healthy)   0.0.0.0:9669->9669/tcp, :::9669->9669/tcp, 0.0.0.0:32792->19669/tcp, :::32792->19669/tcp, 0.0.0.0:32793->19670/tcp, :::32793->19670/tcp
nebula-docker-compose-graphd1-1     docker.io/vesoft/nebula-graphd:v3.6.0     "/usr/local/nebula/b…"   graphd1     12 days ago   Up 14 minutes (healthy)   0.0.0.0:32783->9669/tcp, :::32783->9669/tcp, 0.0.0.0:32784->19669/tcp, :::32784->19669/tcp, 0.0.0.0:32785->19670/tcp, :::32785->19670/tcp
nebula-docker-compose-graphd2-1     docker.io/vesoft/nebula-graphd:v3.6.0     "/usr/local/nebula/b…"   graphd2     12 days ago   Up 14 minutes (healthy)   0.0.0.0:32771->9669/tcp, :::32771->9669/tcp, 0.0.0.0:32772->19669/tcp, :::32772->19669/tcp, 0.0.0.0:32773->19670/tcp, :::32773->19670/tcp
nebula-docker-compose-metad0-1      docker.io/vesoft/nebula-metad:v3.6.0      "/usr/local/nebula/b…"   metad0      12 days ago   Up 14 minutes (healthy)   9560/tcp, 0.0.0.0:32780->9559/tcp, :::32780->9559/tcp, 0.0.0.0:32781->19559/tcp, :::32781->19559/tcp, 0.0.0.0:32782->19560/tcp, :::32782->19560/tcp
nebula-docker-compose-metad1-1      docker.io/vesoft/nebula-metad:v3.6.0      "/usr/local/nebula/b…"   metad1      12 days ago   Up 14 minutes (healthy)   9560/tcp, 0.0.0.0:32786->9559/tcp, :::32786->9559/tcp, 0.0.0.0:32787->19559/tcp, :::32787->19559/tcp, 0.0.0.0:32788->19560/tcp, :::32788->19560/tcp
nebula-docker-compose-metad2-1      docker.io/vesoft/nebula-metad:v3.6.0      "/usr/local/nebula/b…"   metad2      12 days ago   Up 14 minutes (healthy)   9560/tcp, 0.0.0.0:32768->9559/tcp, :::32768->9559/tcp, 0.0.0.0:32769->19559/tcp, :::32769->19559/tcp, 0.0.0.0:32770->19560/tcp, :::32770->19560/tcp
nebula-docker-compose-storaged0-1   docker.io/vesoft/nebula-storaged:v3.6.0   "/usr/local/nebula/b…"   storaged0   12 days ago   Up 14 minutes (healthy)   9777-9778/tcp, 9780/tcp, 0.0.0.0:32789->9779/tcp, :::32789->9779/tcp, 0.0.0.0:32790->19779/tcp, :::32790->19779/tcp, 0.0.0.0:32791->19780/tcp, :::32791->19780/tcp
nebula-docker-compose-storaged1-1   docker.io/vesoft/nebula-storaged:v3.6.0   "/usr/local/nebula/b…"   storaged1   12 days ago   Up 14 minutes (healthy)   9777-9778/tcp, 9780/tcp, 0.0.0.0:32777->9779/tcp, :::32777->9779/tcp, 0.0.0.0:32778->19779/tcp, :::32778->19779/tcp, 0.0.0.0:32779->19780/tcp, :::32779->19780/tcp
nebula-docker-compose-storaged2-1   docker.io/vesoft/nebula-storaged:v3.6.0   "/usr/local/nebula/b…"   storaged2   12 days ago   Up 14 minutes (healthy)   9777-9778/tcp, 9780/tcp, 0.0.0.0:32774->9779/tcp, :::32774->9779/tcp, 0.0.0.0:32775->19779/tcp, :::32775->19779/tcp, 0.0.0.0:32776->19780/tcp, :::32776->19780/tcp
```

- Nebula Graph Consoleの[インストール手順(GitHub)](https://github.com/vesoft-inc/nebula-console?tab=readme-ov-file#from-binary)
    - binaryのダウンロード
    - `/usr/local/bin` にダウンロードしたbinaryを移動

```bash
# インストール後の動作確認
❯ nebula-graph-console --v
nebula-console version Git: , Build Time: 2023-09-16T11:34:10+0000

# Nebula Graph Consoleの使い方
# -addr IPアドレス    パブリックIP、ローカルIP、localhostを指定できる
# -port Port        デフォルトは9669
# -u User           毎回同じので入る必要がある
# -p Passward       毎回同じので入る必要がある
❯ nebula-graph-console -addr localhost -port 9669 -u root -p root

(root@nebula) [(none)]>            
```

## Nebula Graph Consoleの実行手順

- [Nebula Graph Console v3.6.0のドキュメント](https://docs.nebula-graph.io/3.6.0/nebula-console/)

### Console: Nebula Graphとの接続

```bash
# -addr IPアドレス    パブリックIP、ローカルIP、localhostを指定できる
# -port Port        デフォルトは9669
# -u User           毎回同じので入る必要がある
# -p Passward       毎回同じので入る必要がある
❯ nebula-graph-console -addr localhost -port 9669 -u root -p root

(root@nebula) [(none)]>            
```

### Console: `-f` オプション: Nebula Graphにファイルの内容を反映

```bash
# -f FilePath       起動後にファイルの内容がDBに登録される
❯ nebula-graph-console -addr localhost -port 9669 -u root -p root -f sample_data/basketballplayer-2.X.ngql
(root@nebula) [(none)]> drop space basketballplayer;
Execution succeeded (time spent 915µs/1.141126ms)

Sat, 27 Jul 2024 12:13:48 JST

(root@nebula) [(none)]> create space basketballplayer(partition_num=10,replica_factor=1,vid_type=fixed_string(32));
Execution succeeded (time spent 1.52ms/1.757252ms)

Sat, 27 Jul 2024 12:13:48 JST

(root@nebula) [(none)]> :sleep 20
(root@nebula) [(none)]> use basketballplayer;
Execution succeeded (time spent 2.489ms/3.859052ms)

Sat, 27 Jul 2024 12:14:08 JST

(root@nebula) [basketballplayer]> create tag player(name string,age int);
Execution succeeded (time spent 3.699ms/4.426015ms)

Sat, 27 Jul 2024 12:14:08 JST

# 以下登録の処理が実行される...
```

## nGQL 構文

- [nGQLのoverview](https://docs.nebula-graph.io/3.6.0/3.ngql-guide/1.nGQL-overview/1.overview/)
- [nGQLのスタイルガイド](https://docs.nebula-graph.io/3.6.0/3.ngql-guide/1.nGQL-overview/ngql-style-guide/)

### nGQL: Queries

#### MATCH

- [ドキュメント](https://docs.nebula-graph.io/3.6.0/3.ngql-guide/7.general-query-statements/2.match/)
- パターンベースの検索機能

##### MATCH: 基本構文

```bash
# MATCH <pattern> [<clause_1>] RETURN <output> [<clause_2>];

# 頂点を一致させる
(root@nebula) [basketballplayer]> MATCH (v) \   # ユーザ定義変数:vを作成
                               -> RETURN v \    # 結果を変数で取得をvで取得
                               -> LIMIT 3;      # 表示する上限の値を設定
+---------------------------------------------------------+
| v                                                       |
+---------------------------------------------------------+
| ("player103" :player{age: 32, name: "Rudy Gay"})        |
| ("player113" :player{age: 29, name: "Dejounte Murray"}) |
| ("player121" :player{age: 33, name: "Chris Paul"})      |
+---------------------------------------------------------+
Got 3 rows (time spent 6.821ms/17.442221ms)

Sat, 27 Jul 2024 12:27:23 JST

```

##### MATCH: Tagでマッチ

```bash
# actor Tagを作成
(root@nebula) [basketballplayer]> CREATE TAG actor (name string, age int);
Execution succeeded (time spent 2.959ms/3.710313ms)

Sun, 28 Jul 2024 16:55:37 JST

# player 100にactor Tagを挿入
(root@nebula) [basketballplayer]> INSERT VERTEX actor(name, age) VALUES "player100":("Tim Duncan", 42);
Execution succeeded (time spent 13.567ms/14.421555ms)

Sun, 28 Jul 2024 16:56:05 JST

# player Tagとactor Tagを持つVertexを出力
(root@nebula) [basketballplayer]> MATCH (v:player:actor) RETURN v LIMIT 3
+----------------------------------------------------------------------------------------+
| v                                                                                      |
+----------------------------------------------------------------------------------------+
| ("player100" :player{age: 42, name: "Tim Duncan"} :actor{age: 42, name: "Tim Duncan"}) |
+----------------------------------------------------------------------------------------+
Got 1 rows (time spent 4.174ms/4.861431ms)

Sun, 28 Jul 2024 16:56:35 JST

# actor Tagを持つVertexを出力
(root@nebula) [basketballplayer]> MATCH (v:actor) RETURN v LIMIT 3
+----------------------------------------------------------------------------------------+
| v                                                                                      |
+----------------------------------------------------------------------------------------+
| ("player100" :player{age: 42, name: "Tim Duncan"} :actor{age: 42, name: "Tim Duncan"}) |
+----------------------------------------------------------------------------------------+
Got 1 rows (time spent 2.367ms/2.80505ms)

Sun, 28 Jul 2024 16:56:43 JST

# player Tagを持つVertexを出力
(root@nebula) [basketballplayer]> MATCH (v:player) RETURN v;
+----------------------------------------------------------------------------------------+
| v                                                                                      |
+----------------------------------------------------------------------------------------+
| ("player127" :player{age: 42, name: "Vince Carter"})                                   |
# ...省略
# player100 の actor Tag も表示される
| ("player100" :player{age: 42, name: "Tim Duncan"} :actor{age: 42, name: "Tim Duncan"}) |
# ...省略
+----------------------------------------------------------------------------------------+
Got 51 rows (time spent 1.757ms/2.395836ms)

Sun, 28 Jul 2024 16:57:03 JST
```

##### MATCH: TagのPropertyにマッチ

```bash
# player Tagの name = Tim DuncanのVertexにマッチさせる
(root@nebula) [basketballplayer]> MATCH (v:player{name:"Tim Duncan"}) \
                               -> RETURN v;
+----------------------------------------------------------------------------------------+
| v                                                                                      |
+----------------------------------------------------------------------------------------+
| ("player100" :player{age: 42, name: "Tim Duncan"} :actor{age: 42, name: "Tim Duncan"}) |
+----------------------------------------------------------------------------------------+
Got 1 rows (time spent 4.194ms/4.858045ms)

Sun, 28 Jul 2024 17:03:04 JST

# SQLのように WHERE キーワードを使ってマッチ条件を指定することもできる 
(root@nebula) [basketballplayer]> MATCH (v:player) \
                               -> WHERE v.player.name == "Tim Duncan" \
                               -> RETURN v;
+----------------------------------------------------------------------------------------+
| v                                                                                      |
+----------------------------------------------------------------------------------------+
| ("player100" :player{age: 42, name: "Tim Duncan"} :actor{age: 42, name: "Tim Duncan"}) |
+----------------------------------------------------------------------------------------+
Got 1 rows (time spent 4.604ms/5.497303ms)

Sun, 28 Jul 2024 17:04:22 JST
```

##### MATCH: TagのPropertyにマッチ(WHEREを使用)

```bash
(root@nebula) [basketballplayer]> MATCH (v) \
                               -> WITH v, properties(v) as props, keys(properties(v)) as kk \
                               -> WHERE [i in kk where props[i] == "Tim Duncan"] \
                               -> RETURN v;
+----------------------------------------------------------------------------------------+
| v                                                                                      |
+----------------------------------------------------------------------------------------+
| ("player100" :player{age: 42, name: "Tim Duncan"} :actor{age: 42, name: "Tim Duncan"}) |
+----------------------------------------------------------------------------------------+
Got 1 rows (time spent 6.138ms/6.746556ms)

Sun, 28 Jul 2024 17:06:28 JST
```

##### MATCH: 関連するVertexに対してマッチ

```bash
# player 同士に関連があるVertexを取得する
# player Tag の name propertyが Tim Duncan, Yao Mingの場合にマッチする
(root@nebula) [basketballplayer]> WITH ['Tim Duncan', 'Yao Ming'] As names \
                               -> MATCH (v1:player)-->(v2:player) \
                               -> WHERE v1.player.name in names \
                               -> RETURN v1, v2;
+----------------------------------------------------+----------------------------------------------------------+
| v1                                                 | v2                                                       |
+----------------------------------------------------+----------------------------------------------------------+
| ("player133" :player{age: 38, name: "Yao Ming"})   | ("player114" :player{age: 39, name: "Tracy McGrady"})    |
| ("player133" :player{age: 38, name: "Yao Ming"})   | ("player144" :player{age: 47, name: "Shaquille O'Neal"}) |
| ("player100" :player{age: 42, name: "Tim Duncan"}) | ("player101" :player{age: 36, name: "Tony Parker"})      |
| ("player100" :player{age: 42, name: "Tim Duncan"}) | ("player125" :player{age: 41, name: "Manu Ginobili"})    |
+----------------------------------------------------+----------------------------------------------------------+
Got 4 rows (time spent 5.789ms/6.407664ms)

Sun, 28 Jul 2024 17:13:17 JST
```

##### MATCH: VIDと一致するVertexにマッチ(id関数)

```bash
# id関数を使ってVIDと一致するVertexにマッチする
# VIDが player101のVertexにマッチ
(root@nebula) [basketballplayer]> MATCH (v) \
                               -> WHERE id(v) == 'player101' \
                               -> RETURN v;
+-----------------------------------------------------+
| v                                                   |
+-----------------------------------------------------+
| ("player101" :player{age: 36, name: "Tony Parker"}) |
+-----------------------------------------------------+
Got 1 rows (time spent 2.132ms/3.230602ms)

Sun, 28 Jul 2024 17:18:22 JST

# id関数とIN演算子を組み合わせてマッチする
# Tim Duncanと関連するVertexの VIDの player101、player102であるVertexにマッチ
(root@nebula) [basketballplayer]> MATCH (v:player {name: 'Tim Duncan'})--(v2) \
                               -> WHERE id(v2) IN ["player101", "player102"] \
                               -> RETURN v2;
+-----------------------------------------------------------+
| v2                                                        |
+-----------------------------------------------------------+
| ("player101" :player{age: 36, name: "Tony Parker"})       |
| ("player101" :player{age: 36, name: "Tony Parker"})       |
| ("player102" :player{age: 33, name: "LaMarcus Aldridge"}) |
+-----------------------------------------------------------+
Got 3 rows (time spent 4.465ms/5.331919ms)

Sun, 28 Jul 2024 17:20:01 JST
```

##### MATCH: 両方向エッジで接続されたVertexにマッチ

```bash
# --で両方向エッジで接続されるVertexにマッチできる
(root@nebula) [basketballplayer]> MATCH (v:player{name:"Tim Duncan"})--(v2) \
                               -> RETURN v2.player.name As Name;
+---------------------+
| Name                |
+---------------------+
| "Tony Parker"       |
| "Manu Ginobili"     |
| "Tony Parker"       |
| "LaMarcus Aldridge" |
| "Marco Belinelli"   |
| "Danny Green"       |
| "Aron Baynes"       |
| "Boris Diaw"        |
| "Tiago Splitter"    |
| "Dejounte Murray"   |
| "Manu Ginobili"     |
| "Shaquille O'Neal"  |
| __NULL__            |
+---------------------+
Got 13 rows (time spent 2.965ms/3.508627ms)

Sun, 28 Jul 2024 17:25:14 JST
```

##### MATCH: エッジの方向を指定してマッチ

```bash
# --> 出力エッジで方向を指定
(root@nebula) [basketballplayer]> MATCH (v:player{name:"Tim Duncan"}) -->(v2:player) \
                               -> RETURN v2.player.name AS Name;
+-----------------+
| Name            |
+-----------------+
| "Tony Parker"   |
| "Manu Ginobili" |
+-----------------+
Got 2 rows (time spent 5.335ms/5.953918ms)

Sun, 28 Jul 2024 17:28:10 JST

# <-- 入力エッジで方向を指定
(root@nebula) [basketballplayer]> MATCH (v:player{name:"Tim Duncan"}) <-- (v2:player) RETURN v2.player.name AS Name;
+---------------------+
| Name                |
+---------------------+
| "Tony Parker"       |
| "LaMarcus Aldridge" |
| "Marco Belinelli"   |
| "Danny Green"       |
| "Aron Baynes"       |
| "Boris Diaw"        |
| "Tiago Splitter"    |
| "Dejounte Murray"   |
| "Manu Ginobili"     |
| "Shaquille O'Neal"  |
+---------------------+
Got 10 rows (time spent 3.941ms/4.484396ms)

Sun, 28 Jul 2024 17:29:31 JST



```

##### MATCH: propertyを照会してマッチする

```bash
# CASE WHEN THEN 演算子を使ってマッチする
(root@nebula) [basketballplayer]> MATCH (v:player{name: "Tim Duncan"})--(v2) \
                               -> RETURN \
                               -> CASE WHEN v2.team.name IS NOT NULL \
                               -> THEN v2.team.name \
                               -> WHEN v2.player.name IS NOT NULL \
                               -> THEN v2.player.name END AS Name;
+---------------------+
| Name                |
+---------------------+
| "Tony Parker"       |
| "Manu Ginobili"     |
| "Tony Parker"       |
| "LaMarcus Aldridge" |
| "Marco Belinelli"   |
| "Danny Green"       |
| "Aron Baynes"       |
| "Boris Diaw"        |
| "Tiago Splitter"    |
| "Dejounte Murray"   |
| "Manu Ginobili"     |
| "Shaquille O'Neal"  |
| "Spurs"             |
+---------------------+
Got 13 rows (time spent 5.385ms/6.306421ms)

Sun, 28 Jul 2024 17:32:12 JST
```

#### OPTIONAL MATCH

#### LOOKUP

#### GO

#### FETCH

#### SHOW

#### FIND PATH

#### GET SUBGRAPH
