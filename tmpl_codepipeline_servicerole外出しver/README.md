# tmpl_service_roles.yaml

トップ階層にある tmpl_codepipeline.yaml からサービスロールの部分を外だしにしたテンプレートです。

# tmpl_codepipeline_2.yaml

「mpl_service_roles.yaml」でサービスロールを作成すると、「myBasic-CodeBuildServiceRoleArn」と「myBasic-CodePipelineServiceRoleArn」という名前で各ロールのARNを参照できるようになります。  
トップ階層にある tmpl_codepipeline.yaml からサービスロールの定義を削除して、ImportValue関数で作成済のロールを参照するようにしたバージョンです。

```yaml:例
      ServiceRole: !ImportValue myBasic-CodeBuildServiceRoleArn
```