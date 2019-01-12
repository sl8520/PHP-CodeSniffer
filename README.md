# PHP-CodeSniffer
## 介紹
[PHP-CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) 用來檢測程式碼是否符合所設定的規範，裡面有兩個 PHP scripts，phpcs, phpcbf。<font color="#c7254e">`PHP 版本必須 >= 5.4.0`</font>
- phpcs (PHP Code Sniffer): 檢查程式碼標準。
- phpcbf (PHP Code Beautifier and Fixer): 修正不符合標準的程式碼。

## 安裝
CodeSniffer 支援 5 種 (Phar / Composer / Phive / PEAR / Git Clone) 安裝方式，這裡使用 Comporser 安裝。

確認是否已安裝過 Composer
```shell
> composer --version
```
當命令執行後，如果能看到下方的一些資訊，代表本機已安裝
```shell
Composer version 1.6.3 2018-01-31 16:28:17
```

如果本地尚未安裝 Composer，請參考 Compoeser 安裝方法 ([Linux|Unix|OSX](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx) / [Windows](https://getcomposer.org/doc/00-intro.md#installation-windows))。

安裝完成後，使用 Composer 指令安裝 PHP-CodeSniffer
```shell
> composer global require "squizlabs/php_codesniffer=*"
```
安裝完成後使用指令確定完成安裝
```shell
> phpcs --version
```
當命令執行後，如果能看到下方的一些資訊，那麼就代表安裝成功
```shell
PHP_CodeSniffer version 3.3.1 (stable) by Squiz (http://www.squiz.net)
```

## 設定
==FOR 新專案==

新增自定義規則 ( 以 <font color="#c7254e">`PSR2`</font> 為基準新增些許規則 )

```shell
> cd C:\Users\使用者名稱\AppData\Roaming\Composer\vendor\squizlabs\php_codesniffer\src\Standards
> mkdir PSR2-YENPIN

> cd PSR2-YENPIN
> type nul > ruleset.xml
```
<font color="#c7254e">`ruleset.xml`</font> 內容
```xml
<?xml version="1.0"?>
<ruleset name="PSR2-YENPIN">
  <description>The PSR2-YENPIN coding standard.</description>
  <arg name="tab-width" value="2"/>
  <rule ref="PSR2">
    <!-- private member|method must have an underscore on the front -->
    <exclude name="PSR2.Classes.PropertyDeclaration.Underscore"/>
    <exclude name="PSR2.Methods.MethodDeclaration.Underscore"/>
  </rule>

  <!-- private member|method must have an underscore on the front -->
  <rule ref="PEAR.NamingConventions.ValidFunctionName.PrivateNoUnderscore"/>
  <rule ref="PEAR.NamingConventions.ValidVariableName.PrivateNoUnderscore"/>

  <!-- Checks the naming of variables and member variables -->
  <rule ref="Squiz.NamingConventions.ValidVariableName.NotCamelCaps"/>
  <rule ref="Squiz.NamingConventions.ValidVariableName.MemberNotCamelCaps"/>
  <rule ref="Squiz.NamingConventions.ValidVariableName.StringNotCamelCaps"/>

  <!-- Verifies that operators have valid spacing surrounding them -->
  <rule ref="Squiz.WhiteSpace.OperatorSpacing">
    <properties>
      <property name="ignoreNewlines" value="true"/>
    </properties>
  </rule>
  <!-- Makes sure there are no spaces around the concatenation operator -->
  <rule ref="Squiz.Strings.ConcatenationSpacing">
    <properties>
      <property name="spacing" value="1"/>
      <property name="ignoreNewlines" value="true"/>
    </properties>
  </rule>
  <!-- Makes sure that any use of double quotes strings are warranted -->
  <rule ref="Squiz.Strings.DoubleQuoteUsage.NotRequired"/>
  <!-- Ensures that arrays conform to the array coding standard -->
  <rule ref="Squiz.Arrays.ArrayDeclaration">
    <exclude name="Squiz.Arrays.ArrayDeclaration.MultiLineNotAllowed"/>
    <exclude name="Squiz.Arrays.ArrayDeclaration.SingleLineNotAllowed"/>
    <exclude name="Squiz.Arrays.ArrayDeclaration.KeyNotAligned"/>
    <exclude name="Squiz.Arrays.ArrayDeclaration.ValueNotAligned"/>
    <exclude name="Squiz.Arrays.ArrayDeclaration.CloseBraceNotAligned"/>
    <exclude name="Squiz.Arrays.ArrayDeclaration.DoubleArrowNotAligned"/>
  </rule>
  <!-- Ensure there is no whitespace before/after an object operator -->
  <rule ref="Squiz.WhiteSpace.ObjectOperatorSpacing"/>
  <!-- Verifies that operators have valid spacing surrounding them -->
  <rule ref="Squiz.WhiteSpace.LogicalOperatorSpacing"/>
  <!-- Ensure there is no whitespace before a semicolon -->
  <rule ref="Squiz.WhiteSpace.SemicolonSpacing"/>

  <!-- Ensures that array are indented one tab stop -->
  <rule ref="Generic.Arrays.ArrayIndent"/>
  <!-- Bans PHP 4 style constructors -->
  <rule ref="Generic.NamingConventions.ConstructorName"/>
  <!-- Bans the use of the PHP long array syntax -->
  <rule ref="Generic.Arrays.DisallowLongArraySyntax"/>
</ruleset>
```

==FOR 舊專案==

新增自定義規則 ( 以 <font color="#c7254e">`PSR2`</font> 為基準新增些許規則 & 除去舊專案不需之規則 )

```shell
> cd C:\Users\使用者名稱\AppData\Roaming\Composer\vendor\squizlabs\php_codesniffer\src\Standards
> mkdir PSR2-YENPIN

> cd PSR2-YENPIN
> type nul > ruleset.xml
```
<font color="#c7254e">`ruleset.xml`</font> 內容
```xml
<?xml version="1.0"?>
<ruleset name="PSR2-YENPIN">
  <description>The PSR2-YENPIN coding standard.</description>
  <arg name="tab-width" value="2"/>
  <rule ref="PSR2">
    <!-- old project is not have namespace -->
    <exclude name="PSR1.Classes.ClassDeclaration.MissingNamespace"/>
    <!-- old project is not use camel case -->
    <exclude name="PSR1.Methods.CamelCapsMethodName.NotCamelCaps"/>
    <exclude name="Squiz.Classes.ValidClassName.NotCamelCaps"/>
    <!-- private member|method must have an underscore on the front -->
    <exclude name="PSR2.Classes.PropertyDeclaration.Underscore"/>
    <exclude name="PSR2.Methods.MethodDeclaration.Underscore"/>
  </rule>

  <!-- private member|method must have an underscore on the front -->
  <rule ref="PEAR.NamingConventions.ValidFunctionName.PrivateNoUnderscore"/>
  <rule ref="PEAR.NamingConventions.ValidVariableName.PrivateNoUnderscore"/>

  <!-- Checks the naming of variables and member variables -->
  <rule ref="Squiz.NamingConventions.ValidVariableName.NotCamelCaps"/>
  <rule ref="Squiz.NamingConventions.ValidVariableName.MemberNotCamelCaps"/>
  <rule ref="Squiz.NamingConventions.ValidVariableName.StringNotCamelCaps"/>

  <!-- Verifies that operators have valid spacing surrounding them -->
  <rule ref="Squiz.WhiteSpace.OperatorSpacing">
    <properties>
      <property name="ignoreNewlines" value="true"/>
    </properties>
  </rule>
  <!-- Makes sure there are no spaces around the concatenation operator -->
  <rule ref="Squiz.Strings.ConcatenationSpacing">
    <properties>
      <property name="spacing" value="1"/>
      <property name="ignoreNewlines" value="true"/>
    </properties>
  </rule>
  <!-- Makes sure that any use of double quotes strings are warranted -->
  <rule ref="Squiz.Strings.DoubleQuoteUsage.NotRequired"/>
  <!-- Ensures that arrays conform to the array coding standard -->
  <rule ref="Squiz.Arrays.ArrayDeclaration">
    <exclude name="Squiz.Arrays.ArrayDeclaration.MultiLineNotAllowed"/>
    <exclude name="Squiz.Arrays.ArrayDeclaration.SingleLineNotAllowed"/>
    <exclude name="Squiz.Arrays.ArrayDeclaration.KeyNotAligned"/>
    <exclude name="Squiz.Arrays.ArrayDeclaration.ValueNotAligned"/>
    <exclude name="Squiz.Arrays.ArrayDeclaration.CloseBraceNotAligned"/>
    <exclude name="Squiz.Arrays.ArrayDeclaration.DoubleArrowNotAligned"/>
  </rule>
  <!-- Ensure there is no whitespace before/after an object operator -->
  <rule ref="Squiz.WhiteSpace.ObjectOperatorSpacing"/>
  <!-- Verifies that operators have valid spacing surrounding them -->
  <rule ref="Squiz.WhiteSpace.LogicalOperatorSpacing"/>
  <!-- Ensure there is no whitespace before a semicolon -->
  <rule ref="Squiz.WhiteSpace.SemicolonSpacing"/>

  <!-- Ensures that array are indented one tab stop -->
  <rule ref="Generic.Arrays.ArrayIndent"/>
  <!-- Bans PHP 4 style constructors -->
  <rule ref="Generic.NamingConventions.ConstructorName"/>
</ruleset>
```

---

設定編碼字符集
```shell
> phpcs --config-set encoding utf-8
```
設定規範標準
```shell
> phpcs --config-set default_standard PSR2-YENPIN
```
查看設定檔
```shell
> phpcs --config-show
```

執行完會產生設定檔 CodeSniffer.conf，可設定之[設定檔](https://github.com/squizlabs/PHP_CodeSniffer/wiki/Configuration-Options)。

## Use Command Line

```shell
> phpcs <path>

# example
> phpcs web_mem/application/controllers/main.php
```

命令執行完後會出現如下提示，在提示中能看到<font color="#c7254e">`行數`</font>，<font color="#c7254e">`提示級別`</font>，以及具體的<font color="#c7254e">`提示原因`</font>。

```shell
FILE: ...rt-001\Desktop\example\web_mem\application\controllers\main.php
----------------------------------------------------------------------
FOUND 1 ERROR AND 3 WARNINGS AFFECTING 4 LINES
----------------------------------------------------------------------
  16 | ERROR   | [ ] Private member variable "version" must be prefixed
     |         |     with an underscore
  61 | ERROR   | [x] Expected 1 space(s) after IF keyword; 0 found
  72 | ERROR   | [ ] Visibility must be declared on method "curlyypay"
 118 | WARNING | [ ] Line exceeds 120 characters; contains 133 characters
 342 | WARNING | [ ] Line exceeds 120 characters; contains 142 characters
 359 | WARNING | [ ] Line exceeds 120 characters; contains 355 characters
----------------------------------------------------------------------
PHPCBF CAN FIX THE 1 MARKED SNIFF VIOLATIONS AUTOMATICALLY
----------------------------------------------------------------------

Time: 602ms; Memory: 8.25Mb
```

出現 1 個地方可以用 <font color="#c7254e">`phpcbf`</font> 修正 ( [x] 的部分)。

```shell
> phpcbf <path>

# example
> phpcbf web_mem/application/controllers/main.php
```

命令執行完後會出現如下提示。

```shell
PHPCBF RESULT SUMMARY
----------------------------------------------------------------------
FILE                                                  FIXED  REMAINING
----------------------------------------------------------------------
...example\web_mem\application\controllers\main.php  1      5
----------------------------------------------------------------------
A TOTAL OF 1 ERROR WERE FIXED IN 1 FILE
----------------------------------------------------------------------

Time: 397ms; Memory: 10.5Mb
```

<font color="#c7254e">`phpcbf`</font> 只能修正部分格式不符合的程式碼，其餘無法修正的部分必須手動修正。

## 編輯器外掛
- **Sublime Text**
    - [Phpcs](https://packagecontrol.io/packages/Phpcs) - phpcs、phpcbf、php-cs-fixer、phpmd 整合
    - [SublimeLinter-phpcs](https://packagecontrol.io/packages/SublimeLinter-phpcs) <font color="#c7254e">`必須先安裝`</font> [SublimeLinter](https://packagecontrol.io/packages/SublimeLinter) <font color="#c7254e">`才可使用`</font>

設定使用自定義規則
Preferences → Package Settings → PHP Code Sniffer → Settings - User
```json
{
    "phpcs_executable_path": "phpcs.bat",
    "phpcs_additional_args": {
        "--standard": "PSR2-YENPIN",
        "-n": ""
    },

    // phpcbf settings
    "phpcbf_executable_path": "phpcbf.bat",
    "phpcbf_additional_args": {
        "--standard": "PSR2-YENPIN",
        "-n": ""
    }
}
```

- **VSCode**
    - [phpcs](https://marketplace.visualstudio.com/items?itemName=ikappas.phpcs)
    - [phpcbf](https://marketplace.visualstudio.com/items?itemName=persoderlind.vscode-phpcbf)

設定使用自定義規則
檔案 → 喜好設定 → 設定
```json
{
    "phpcs.autoConfigSearch": false,
    "phpcs.standard": "PSR2-YENPIN",

    // phpcbf settings
    "phpcbf.executablePath": "phpcbf.bat",
    "phpcbf.standard": "PSR2-YENPIN"
}
```

- **phpStorm**
[請參照](https://clouding.city/php-phpcs-phpcbf/#PhpStorm)
