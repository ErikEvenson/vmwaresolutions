---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-20"

---

# vCenter Server インスタンスのサービスの注文、表示、削除

災害復旧ソリューションなど、VMware vCenter Server インスタンス向けのサービスを注文できます。 これらのサービスが不要になった場合は、インスタンスから削除できます。

## vCenter Server インスタンスで使用可能なサービス

vCenter Server インスタンスで使用できるサービスを以下の表にまとめます。

表 1. vCenter Server インスタンスに使用可能なサービス

| サービス名 | 可用性 | インスタンス・サポート |
|----------------------------------------------------------------------------------------|------------------|
| [F5 on {{site.data.keyword.cloud}}](../services/f5_considerations.html)                                 | はい | V1.9 以降 |
| [FortiGate Security Appliance on {{site.data.keyword.cloud_notm}}(../services/fortinetvm_considerations.html) | はい | V2.0 以降 |
| [HyTrust CloudControl on {{site.data.keyword.cloud_notm}}](../services/htcc_considerations.html)              | はい | V2.3 以降 |
| [HyTrust DataControl on {{site.data.keyword.cloud_notm}}](../services/htdc_considerations.html)              | はい | V2.3 以降 |
| [IBM Spectrum Protect&trade; Plus on {{site.data.keyword.cloud_notm}}](../services/spp_considerations.html)         | はい | V2.2 以降 |
| [KMIP for VMware on {{site.data.keyword.cloud_notm}}](../services/kmip_considerations.html)                  | はい | V2.2 以降 |
| [Veeam on {{site.data.keyword.cloud_notm}}](../services/veeam_considerations.html)                          | はい | V1.8 以降 |
| [VMware HCX on {{site.data.keyword.cloud_notm}}](../services/hcx_considerations.html)                         | いいえ | 適用外 |
| [Zerto on {{site.data.keyword.cloud_notm}}](../services/addingzertodr.html)                                 | はい | V1.2 以降 |


## vCenter Server インスタンスへのサービスの追加

vCenter Server インスタンスにサービスを追加するには、前のテーブルで該当サービスのリンクをクリックし、そのサービスに関する考慮事項を確認し、デプロイするコンポーネントにチェック・マークを付けます。 その後、サービス注文トピックに記されている指示に従って、インスタンスにサービスを追加します。

### サービスのインストールの結果

サービスのインストールが正常に完了すると、E メールで通知が届きます。また、そのサービスがインスタンスの**「サービス」**ページに表示され、サービスの状況が**「インストール済み」**になります。

## vCenter Server インスタンス向けのサービスの参照

1. {{site.data.keyword.vmwaresolutions_short}} コンソールで、左側のナビゲーション・ペインの**「デプロイ済みインスタンス」**をクリックします。
2. **「vCenter Server インスタンス」**テーブルで、サービスを表示するインスタンスをクリックします。
3. 左側のナビゲーション・ペインの**「サービス」**をクリックします。
4. **「サービス」**ページでサービスをクリックし、そのサービスの情報 (サービス状況などの詳細) を確認します。
5. 表示したサービスによっては、サービスの詳細情報に記されている資格情報を使用してサービス・コンソールにアクセスし、そこからサービスを管理することもできます。

## vCenter Server インスタンス向けのサービスの削除

1. {{site.data.keyword.vmwaresolutions_short}} コンソールで、左側のナビゲーション・ペインの**「デプロイ済みインスタンス」**をクリックします。
2. **「vCenter Server インスタンス」**テーブルで、サービスを削除するインスタンスをクリックします。
3. 左側のナビゲーション・ペインの**「サービス」**をクリックします。
4. **「サービス」**ページで、削除するサービス・インスタンスを見つけて**「削除」**アイコンをクリックします。
5. **「サービスの削除」**ウィンドウで、考慮事項または警告が示されているなら、それを確認します。 **「了解」**を選択し、**「削除」**をクリックします。

### サービスの削除結果

サービスの削除要求が受け入れられると、サービス状況が**「削除中」**に変更されます。

サービスの削除が正常に完了すると、お客様に E メールで通知され、サービスがインスタンスの**「サービス」**ページから削除されます。

**注意**: 削除したサービスは、{{site.data.keyword.cloud_notm}} インフラストラクチャーの請求サイクルの最後まで課金されます。

### 関連リンク

* [FAQ](../vmonic/faq.html)
