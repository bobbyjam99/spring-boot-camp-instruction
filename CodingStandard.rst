RestructuredTextの記述ルール
********************************************************************************
.. contents:: 目次
   :depth: 3


階層
================================================================================

.. code-block:: rest

    A. Chapter
    ********************************************************************************

    A.B Section
    ================================================================================

    A.B.C Subsection
    --------------------------------------------------------------------------------

    A.B.C.D Subsubsection
    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    A.B.C.D.E Paragraph
    """"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

    A.B.C.D.E.F ?
    ''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

実際は
A.とかは書かなくてよい。これ以上の階層は作成しないこと。原則E階層までにすること。Fまでくると構成がおかしい可能性が高い。よく見直すこと。

Appendixとかチュートリアルとか別のドキュメントを組み込んでる場合はＦまでいくこともある

文章の基本構成
================================================================================

以下の構成を基本とする

.. code-block:: rest



    Overview
    --------------------------------------------------------------------------------
    概要や背景を書く。


    How to use
    --------------------------------------------------------------------------------
    基本的な利用方法を書く。

    How to extend
    --------------------------------------------------------------------------------
    拡張方法や応用的な使い方を書く。

テーブル
--------

`list-table <http://docutils.sourceforge.net/docs/ref/rst/directives.html#list-table>`__\ を使うこと

例

.. code-block:: rest

    .. list-table::
       :header-rows: 1
       :widths: 75 25

       * - Product
         - Version
       * - JDK
         - 1.6.0\_33
       * - SpringSource Tool Suite (STS)
         - 3.2.0
       * - VMware vFabric tc Server Developer Edition
         - 2.8
       * - Fire Fox
         - 21.0

アスキーアートテーブルはメンテナンス性が悪いので使わない

NG

.. code-block:: rest

    +-----------+----------------+------------------------+-----------+
    | 記号      | パターン       | 表示内容               | メッセージ|
    |           |                |                        | タイプ    |
    +===========+================+========================+===========+
    | （A）     | タイトル       | 画面のタイトル         || -        |
    |           +----------------+------------------------+           |
    |           | ラベル         || 画面、帳票の項目名    |           |
    |           |                || テーブル項目名        |           |
    |           |                || コメント              |           |
    +-----------+----------------+------------------------+-----------+
    | （B）     | 結果メッセージ | 確認                   | info      |
    +-----------+                +------------------------+           |
    | （C）     |                | 正常終了               |           |
    +-----------+                +------------------------+-----------+
    | （D）     |                | 警告                   | warn      |
    +-----------+                +------------------------+-----------+
    | （E）     |                | 単項目チェックエラー   | error     |
    +-----------+                +------------------------+           |
    | （F）     |                | 相関チェックエラー     |           |
    +-----------+                +------------------------+           |
    | （G）     |                | 業務エラー             |           |
    +-----------+                +------------------------+           |
    | （H）     |                | システムエラー         |           |
    +-----------+----------------+------------------------+-----------+

OK

.. code-block:: rest

    .. tabularcolumns:: |p{0.20\linewidth}|p{0.25\linewidth}|p{0.30\linewidth}|p{0.25\linewidth}|
    .. list-table::
       :header-rows: 1
       :widths: 20 25 30 25

       * - 記号
         - パターン
         - 表示内容
         - メッセージタイプ
       * - | (A)
         - | タイトル
         - | 画面のタイトル
         - | -
       * - | 
         - | ラベル
         - | 画面、帳票の項目名
           | テーブル項目名
           | コメント
         - | 
       * - | (B)
         - | 結果メッセージ
         - | 確認
         - | info
       * - | (C)
         - | 
         - | 正常終了
         - | 
       * - | (D)
         - | 
         - | 警告
         - | warn
       * - | (E)
         - | 
         - | 単項目チェックエラー
         - | error
       * - | (F)
         - | 
         - | 相関チェックエラー
         - | 
       * - | (G)
         - | 
         - | 業務エラー
         - | 
       * - | (H)
         - | 
         - | システムエラー
         - | 

PDF化のことを考えて、\ ``tabularcolumns``\ も指定すること。

ソースコードの説明
================================================================================

解説する箇所にコメントで括弧付きの項番をつけ、
テーブルで各項番について説明する。

例

.. code-block:: rest

    .. code-block:: jsp

      <!DOCTYPE html>
      <html>
      <head>
      </head>
      <body>
        <form:form action="${pageContext.request.contextPath}/j_spring_security_check" method="post"> <!-- (1) -->
          <fieldset>
            <c:if test="${param.error == true}">
              <t:messagesPanel 
                messagesAttributeName="SPRING_SECURITY_LAST_EXCEPTION"/><!-- (2) -->
            </c:if>
            <p>
              <label for="username">User Name</label><br>
              <input type="text"
                class="text" id="username" name="j_username"><!-- (3) -->
            </p>
            <p>
              <label for="password">Password</label><br>
              <input type="password"
                class="text" id="password" name="j_password"><!-- (4) -->
            </p>
            <p>
              <input type="submit" value="Login" />
            </p>
          </fieldset>
        </form:form>
        <hr>
      </body>
      </html>

    .. tabularcolumns:: |p{0.10\linewidth}|p{0.90\linewidth}|
    .. list-table:: 
       :header-rows: 1
       :widths: 10 90

       * - 項番
         - 説明
       * - | (1)
         - | formのaction属性に認証処理を行うための遷移先を指定する。
           | HTTPメソッドは、「POST」を指定すること。
       * - | (2)
         - | 認証エラー時に出力させる例外メッセージの出力先。
           | 共通ライブラリで提供している\ ``org.terasoluna.gfw.web.message.MessagesPanelTag``\ を指定して出力させることを推奨する。
           | 「messagesPanel」タグの使用方法は、\ :doc:`Message-Management <../online-processing/Message-Management>`\ を参照。
       * - | (3)
         - | 認証処理において、「ユーザID」として扱われる要素。
       * - | (4)
         - | 認証処理において、「パスワード」として扱われる要素。

コピペ用

.. code-block:: rest

    .. code-block:: java


    .. tabularcolumns:: |p{0.10\linewidth}|p{0.90\linewidth}|
    .. list-table:: 
       :header-rows: 1
       :widths: 10 90


       * - 項番
         - 説明
       * - | (1)
         - | 
       * - | (2)
         - | 
       * - | (3)
         - | 
       * - | (4)
         - | 
       * - | (5)
         - | 
       * - | (6)
         - |

``.. code-block::``\ に対応している言語の一覧

http://pygments.org/languages/

画像
================================================================================

widthを%で設定。

.. code-block:: rest

    .. figure:: ./images/xxx.png
       :width: 40%

素材(PPT等)もコミットしておくこと


例

.. figure:: ./images/logo.png
   :width: 20%

リスト
================================================================================

普通のリストは

.. code-block:: rest

    * this is
    * a list

      * with a nested list
      * and some subitems

    * and here the parent list continues

連番リストは

.. code-block:: rest

    #. This is a numbered list.
    #. It has two items too.

見出しへのリファレンス
================================================================================

見出しへのリファレンスは、同一ファイル、別ファイルに関係なく貼ることができる。

.. code-block:: rest


    .. _helloworld:

    Hello World!
    --------------------------------------------------------------------------------

    XXX is YYY.

    Foo
    --------------------------------------------------------------------------------

    XXXについては\ :ref:`helloworld`\ を参照のこと。

テキストを付けたい場合は

.. code-block:: rest


    .. _HelloWorld:

    Hello World!
    --------------------------------------------------------------------------------

    XXX is YYY.

    Foo
    --------------------------------------------------------------------------------

    XXXについては\ :ref:`前述<helloworld>`\ を参照のこと。

ラベル名は、ドキュメント全体でユニーク性を担保する必要があるため、
「rstファイル名(UpperCamel) +
rstファイル内の識別文字列(任意)」とすること。
例えば、「MessageManagement.rst」の場合は、"MessageManagementXxxxx(任意)"とする。

別RSTの先頭への参照
================================================================================

.. code-block:: rest

    \ :doc:`../hoge/foo`\ を参照。

拡張子は不要

``:ref:``\ で定義してある場合はそれを利用する。

Note
================================================================================

* note ... 補足説明
* tip ... 簡単な拡張方法や参考資料など
* warning ... 気を付けないとはまること
* todo ... 後で書く

.. code-block:: rest

    .. note.. code-block:: rest

        補足すると


    .. tip::

        参考に


    .. warning::

        気を付けて！


    .. todo::

        後で書く

上記以外(hintとか)は基本的に使用しないこと

インラインcodeタグ
================================================================================
インラインで\ ``code``\ を書くときは


.. code-block:: rest

    インラインで\ ``code``\ を書くときは

のように書く。

codeタグを使う場合と使わない場合について、以下に説明する。

* 使用する場合：クラス名、パラメータ名
* 使用しない場合：ファイル名、ディレクトリ名

命名規約
================================================================================

* フォルダ名・ファイル名は「UpperCamelCase」(e.g. XxxYyy)を使用する。（ファイルの拡張子は自動に任せる。）
* 画像はrstを配置している階層に「images+rstファイル名」(e.g. imagesMessageManagement)のフォルダを配置し、その中に画像を配置する。
* 画像を作る元のファイル（基本はPowerPoint。必要に応じてその他も可）は「material+rstファイル名」(e.g. materialMessageManagement.pptx)
* 画像ファイルはUpperCamelCase(e.g.XxxYyy)を使用する。「先頭はrstファイル名にして、その後は画像を示す単語で任意とする。」(e.g. MessageManagementResultMessageError.png)
* 画像ファイルはpng形式で保存し、使用する。他の形式は使用しない。
* \ ``:ref:``\ で使用する名称は先頭は「rstファイル名にして、その後は位置を示す単語で任意とする。」(e.g. MessageManagementLabelRule)


PDF出力を意識したRSTファイル記述
================================================================================

目次出力
--------------------------------------------------------------------------------

HTML出力時のページ先頭に目次出力を目的としたcontentsディレクティブを記述しているが、PDF出力時には出力したくない。そのため、HTML出力時にのみ有効となるように以下のように記述する。

.. code-block:: rest

    .. only:: html

     .. contents:: 目次
        :depth: 4

テーブル出力
--------------------------------------------------------------------------------

表を出力するためにlist-tableディレクティブを使用するが、オプションの:width:指定がlatex変換時に有効にならない。そのため、latex変換時にカラム幅を指定するため以下のようにtabularcolumnsディレクティブを記述する。

.. code-block:: rest

    .. tabularcolumns:: |p{0.10\linewidth}|p{0.70\linewidth}|
    .. list-table::
       :header-rows: 1
       :widths: 10 70

       * - header1
         - header2
       * - content1
         - content2

改頁
--------------------------------------------------------------------------------

HTML出力時には改頁を意識する必要はないが、PDF出力時には意識する必要がある。明示的に改頁を入れる場合は、latex変換時にのみ改頁が追加されるように、以下の記述を追加する。

.. code-block:: rest

    .. raw:: latex

       \newpage

PDF化の注意
--------------------------------------------------------------------------------

Jenkinsで実行した際にPDFファイルが出力される。PDFが0byteのファイルの場合、作成に失敗している。
ログからエラー箇所を特定できないため、変更したファイルを半分消して実行し、エラーがあればまた半分消してという、二分木調査しかない。

過去の失敗理由を記述しておく。

* 失敗理由

  * 画像ファイルが大きすぎた。.. figure::で使用する:width:
     70%が大きすぎて、50%にしたところ、エラーはなくなった。画像ファイルがPDF1ページに収まらなかったことが原因と推測。
  * noteやtip内で、listtableを使用する際は、半角スペースの数を4の倍数にすること。(Paginationで半角スペース
     5つ空いていたがためエラーになり、0バイトファイルが出力されていた)

