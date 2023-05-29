# Business Process Automation Accelerator (日本語版)

## 概要

このアクセラレータは、ユーザーが複数のAzure AIおよびMLサービスにわたる複雑な多段AIパイプラインを迅速に構築するためのノーコードStudioを提供します。 ユーザーは、Azure Cognitive Services（OpenAI, Speech, Language, Form Recognizer, ReadAPI）、Azure Machine LearningからAI/MLサービスを選択し、自動化パイプラインを作成できます。サービス間の統合はBPAによって自動化され、デプロイされるとウェブアプリが作成されます。このカスタマイズ可能なUIは、エンドユーザーが複数のサービスパイプラインを構築するためのドラッグアンドドロップインターフェースを提供します。最後に、ユーザーが作成したパイプラインは、最初の入力ファイルがアップロードされるとすぐにトリガーされ、Azure Blob Storageに結果が保存されます。

## Azureへのデプロイ

### 確認事項
1. Githubのアカウント(Admin)
2. Azureリソースグループ(Owner)
3. Azureサブスクリプションで **Microsoft.DocumentDB enabled** になっていることを確認  
確認方法:  
      - Azureポータル(portal.azure.com)にアクセスし、「サブスクリプション」のページに遷移  
      - 左側のメニューから「リソースプロバイダー」を選択  
      - 検索欄に「Microsoft.DocumentDB」を入力  
      - 「状態」が「Registered」になっていることを確認。 「NotRegistered」となっていた場合には「Register」を選択  
      **Note**: *この処理には数秒から数分かかる場合がありますので、定期的にブラウザ全体を更新してください。*
4. **責任あるAI条項**に対しての同意:  
Azureポータルにて"Cognitive services multi-service account"を作成し、利用規約に同意する必要があります。参考文献: [Quickstart: Create a Cognitive Services resource using the Azure portal](https://docs.microsoft.com/en-us/azure/cognitive-services/cognitive-services-apis-create-account?tabs=multiservice%2Cwindows).  
一度承認されると、同じAzureサブスクリプションの下で任意のデプロイツール（SDK、CLI、またはARMテンプレートなど）を使用して、後続のリソースを作成できます。

1. [Workflow Level Token (Classic)の取得](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
2. 自分が管理者であるgitアカウントにリポジトリをフォーク
3. 環境と作成したいパターンに対応する「Deploy to Azure」ボタンをクリックします。 Redis パターンは Vector Search のみ必要です。
4. リソースグループ、GitHubリポジトリのトークン(#2) 、フォーク先のリポジトリURL の情報が必要です。 残りのパラメータは、自動入力されます。

### Without OpenAI
[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FNoriMin%2Fbusiness-process-automation%2Fmain%2Ftemplates%2Foneclick.json)

### With OpenAI
[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FNoriMin%2Fbusiness-process-automation%2Fmain%2Ftemplates%2Foneclickoai.json)

### With OpenAI and Redis Enterprise (check pricing) for Vector Search
[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FNoriMin%2Fbusiness-process-automation%2Fmain%2Ftemplates%2Foneclickoairedis.json)


## アーキテクチャ (一部)
リソースグループを作成したら、このリポジトリをフォークしてヘルパーライブラリをインポートし、Github Actionsを活用してAzure Cognitive Servicesのセットをデプロイして、新しく作成したパイプライン内でバックグラウンドで新しいAzureモジュールの資格情報をすべて管理します。パイプラインのデプロイ後、パイプラインを構築してトリガーするためのカスタマイズ可能なUIを持つ静的Webアプリが作成されます。

![](images/architecture_white.png)  
*Document Ingestion High-level technical architecture*  


  
 
