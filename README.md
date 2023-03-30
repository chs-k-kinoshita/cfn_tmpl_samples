# 概要

AWS CloudFormationテンプレートサンプル（公開用）です。

# tmpl_codepipeline.yaml について

CodeCommitへのpushをトリガーにSPA(React)をS3バケットにpushするCodePipelineのテンプレートです。  
React側のリソースのトップ階層に下記内容の"buildspec.yml"ファイルを配置する必要があります。

```yaml
version: 0.2

phases:
  pre_build:
    commands:
      - npm ci
  build:
    on-failure: ABORT
    commands:
      - npm run build
  post_build:
    commands:
      - cd build
      - aws s3 sync --exact-timestamps --cache-control 'max-age=2592000' --exclude '*' --include 'static/**/*' . s3://${DEPLOY_BUKET}
      - aws s3 sync --exact-timestamps --cache-control 'no-cache' --delete . s3://${DEPLOY_BUKET}
```

# tmpl_s3cf_202303.yaml について

静的Webリソース公開用のCloudFrontとS3バケット(CloudFrontのオリジン)を構築するテンプレートです。