# 3: SIM の開通と SORACOM Harvest Data の設定

この章では、配布された SIM を SORACOM で使える状態にし、データ受け取り先として SORACOM Harvest Data を有効化します。

## 想定時間

10 分

アカウント作成と SIM 登録の作業時間は含みません。

## この章のゴール

- SORACOM ユーザーコンソールにログインできる
- 配布された SIM が登録済みで、状態が `準備完了 (Ready)` になっている
- SIM をハンズオン用の SIM グループに所属させる
- SORACOM Harvest Data を ON にする

## 事前に用意するもの

- SORACOM ユーザーコンソールにログインできるアカウント
- ハンズオン会場で配布された SORACOM IoT SIM
- SIM 台紙または配布資料に記載されている `IMSI` と `パスコード`
- 当日案内されたクーポン

> [!IMPORTANT]
> SORACOM Air for セルラーと SORACOM Harvest Data は有償サービスです。
> このハンズオンでは、当日案内されるクーポンで作業分の料金を補填する想定です。
> ハンズオン後も設定や SIM を残しておくと、そのまま継続して利用できます。ただし、残し続けると課金が発生する場合があります。
> 継続利用しない場合の片付けは、全章の作業を終えたあとに別章でまとめて行います。

## 1. SORACOM アカウントを準備する

アカウント作成手順は、公式ドキュメントを参照してください。

- [STEP 1: SORACOM アカウント (オペレーター) を作成する](https://users.soracom.io/ja-jp/guides/getting-started/create-account/)

正しく完了している状態は、次のとおりです。

- [SORACOM ユーザーコンソール](https://console.soracom.io/) にログインできる
- オペレーター ID が発行されている
  - 例: `OP` で始まる 12 文字の ID
- カバレッジタイプで `Japan` を選択している
- 当日案内されたクーポンを適用している

このハンズオンでは、日本カバレッジの SIM を使います。
以降の作業は、SORACOM ユーザーコンソールでカバレッジタイプに `Japan` を選択した状態で進めます。

## 2. 配布された SIM を登録する

SIM の登録手順は、公式ドキュメントの「イベント会場などで入手した IoT SIM を登録する (個別登録)」を参照してください。

- [STEP 2-2: IoT SIM を SORACOM ユーザーコンソールに登録する](https://users.soracom.io/ja-jp/guides/getting-started/register-sim/#%e3%82%a4%e3%83%99%e3%83%b3%e3%83%88%e4%bc%9a%e5%a0%b4%e3%81%aa%e3%81%a9%e3%81%a7%e5%85%a5%e6%89%8b%e3%81%97%e3%81%9f-iot-sim-%e3%82%92%e7%99%bb%e9%8c%b2%e3%81%99%e3%82%8b-%e5%80%8b%e5%88%a5%e7%99%bb%e9%8c%b2)

このハンズオンで使う SIM は、日本カバレッジの配布 SIM です。
登録では、SIM 台紙または配布資料に記載されている `IMSI` と `パスコード` を使います。

正しく完了している状態は、次のとおりです。

- **SIM 管理** 画面に、配布された SIM が表示されている
- 対象 SIM の `IMSI` が、配布された SIM の IMSI と一致している
- 対象 SIM の `状態` が `準備完了 (Ready)` になっている

![SIM 管理画面で SIM を確認する](image/sim-management-filtered.png)

> [!TIP]
> SIM を区別しやすくするため、SIM の `名前` に `MicroCat.1-handson` などを設定しておくと、このあとの手順で対象 SIM を見つけやすくなります.

## 3. Harvest 用の SIM グループを作成する

左側のメニューから **SIM グループ** を開きます。
次の手順で、ハンズオン用のグループを新しく作成します。

1. **+ グループを追加** をクリックします
2. グループ名を入力します
   - 例: `microcat1-handson`
3. **グループ作成** をクリックします

![SIM グループ画面でグループを追加する](image/sim-groups-list.png)

![グループ名を入力する](image/sim-group-name-entered.png)

作成したグループは、あとで SIM を所属させるときに選択します。

## 4. SIM をグループに所属させる

左側のメニューから **SIM 管理** を開きます。

1. ハンズオンで使う SIM にチェックを入れます
2. **操作** から **所属グループを変更** を選択します
3. **新しい所属グループ** で、手順 3 で作成したグループを選びます
4. **グループ変更** をクリックします

![SIM の所属グループを変更する](image/sim-change-group-selected.png)

SIM 管理画面に戻り、対象 SIM の `グループ` に選択したグループ名が表示されていることを確認します。

![SIM がハンズオン用グループに所属していることを確認する](image/sim-group-changed.png)

## 5. SORACOM Harvest Data を有効化する

左側のメニューから **SIM グループ** を開き、手順 3 で作成したグループをクリックします。

1. **基本設定** タブを開きます
2. **SORACOM Harvest Data 設定** をクリックして設定項目を開きます
3. スイッチを `ON` にします
4. 今回は追加オプションを変更せず、初期設定のままにします
   - カテゴリ: 空欄のまま
   - 一括書き込み: OFF のまま
   - 送信データの時刻をタイムスタンプに利用する: OFF のまま
5. **保存** をクリックします
6. 確認画面が表示されたら内容を確認し、**有効にする** をクリックします

![SORACOM Harvest Data 設定を開く](image/harvest-data-section-collapsed.png)

![Harvest Data 設定を ON にする](image/harvest-data-settings-on-before-save.png)

![Harvest Data の有効化を確認する](image/harvest-data-save-confirm.png)

これで、このグループに所属している SIM から送信したデータを Harvest Data に保存できるようになります。

![Harvest Data 設定が保存されたことを確認する](image/harvest-data-enabled.png)

## 6. 設定できたことを確認する

次の 2 点を確認します。

- SIM 管理画面で、対象 SIM がハンズオン用グループに所属している
- SIM グループ画面で、対象グループの SORACOM Harvest Data 設定が `ON` になっている

![グループに SIM が所属していることを確認する](image/sim-group-member-sim.png)

確認できたら、この章は完了です。
次の章では MicroCat.1 からデータを送信し、Harvest Data に保存されることを確認します。

## FAQ

### SORACOM ユーザーコンソールにログインできない

アカウント作成が完了しているか確認してください。
アカウント作成手順は、[公式ドキュメント](https://users.soracom.io/ja-jp/guides/getting-started/create-account/) を参照します。

### SIM が見つからない

カバレッジタイプが `Japan` になっているか確認してください。
このハンズオンでは日本カバレッジの SIM を使います。

### SIM 登録でエラーになる

入力した `IMSI` と `パスコード` に誤りがないか確認します。
数字の読み間違い、余分な空白、カバレッジタイプの選択違いがよくある原因です。
対象の SIM がすでに別のアカウントに登録されている場合も、登録できません。

### Harvest Data を ON にしたのにデータが表示されない

この章では Harvest Data の受け取り先を準備しただけです。
実際のデータ送信と表示確認は次の章で行います。

### 料金が気になる

当日の作業分は、案内されたクーポンで補填する想定です。
ハンズオン後に設定を残して継続利用する場合は、SORACOM Air for セルラーや SORACOM Harvest Data の料金が発生する場合があります。
継続利用しない場合の片付けは、全章の作業を終えたあとに別章でまとめて行います。

## 参考ドキュメント

- [SORACOM アカウント (オペレーター) を作成する](https://users.soracom.io/ja-jp/guides/getting-started/create-account/)
- [IoT SIM を SORACOM ユーザーコンソールに登録する](https://users.soracom.io/ja-jp/guides/getting-started/register-sim/)
- [グループを作成する](https://users.soracom.io/ja-jp/docs/group-configuration/create-group/)
- [IoT SIM、LoRaWAN デバイス、Sigfox デバイスが所属するグループを切り替える](https://users.soracom.io/ja-jp/docs/group-configuration/set-group/)
- [SORACOM Harvest Data を有効化する](https://users.soracom.io/ja-jp/docs/harvest/enable-data/)

---
- 次: [4: SORACOM へデータ送信して Harvest で確認](../chapter4/README.md)
- 前: [2: hello, world で L チカ](../chapter2/README.md)
