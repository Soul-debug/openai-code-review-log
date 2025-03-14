```json
{
  "security_issues": [
    {
      "type": "硬编码凭证",
      "risk_level": "高危",
      "file_path": "openai-code-review-sdk/src/main/java/plus/gaga/middleware/sdk/OpenAiCodeReview.java",
      "line_number": 102,
      "code_snippet": "private static final String PASSWORD = \"Password123!\";",
      "risk_description": "发现明文密码硬编码，可能导致凭证泄露",
      "recommendation": "1. 立即将凭证迁移到安全配置中心\n2. 使用环境变量注入\n3. 执行历史提交清理"
    },
    {
      "type": "硬编码凭证",
      "risk_level": "高危",
      "file_path": "openai-code-review-sdk/src/main/java/plus/gaga/middleware/sdk/OpenAiCodeReview.java",
      "line_number": 108,
      "code_snippet": "String apiKeySecret = \"45b87abe6d6241da9660e36d7791455b.c3e9Ewb6dqsArvGH\";",
      "risk_description": "发现明文API密钥硬编码，可能导致凭证泄露",
      "recommendation": "1. 立即将凭证迁移到安全配置中心\n2. 使用环境变量注入\n3. 执行历史提交清理"
    },
    {
      "type": "硬编码凭证",
      "risk_level": "高危",
      "file_path": "openai-code-review-sdk/src/main/java/plus/gaga/middleware/sdk/OpenAiCodeReview.java",
      "line_number": 114,
      "code_snippet": "String password = \"Password123!\";",
      "risk_description": "发现明文密码硬编码，可能导致凭证泄露",
      "recommendation": "1. 立即将凭证迁移到安全配置中心\n2. 使用环境变量注入\n3. 执行历史提交清理"
    },
    {
      "type": "硬编码凭证",
      "risk_level": "高危",
      "file_path": "openai-code-review-sdk/src/main/java/plus/gaga/middleware/sdk/OpenAiCodeReview.java",
      "line_number": 116,
      "code_snippet": "String abc = \"12345678\";",
      "risk_description": "发现硬编码的简单字符串，可能用于敏感操作，建议审查其用途",
      "recommendation": "1. 审查该字符串的用途，确保其安全性\n2. 如果不是敏感信息，建议移除硬编码"
    },
    {
      "type": "配置文件敏感信息泄露",
      "risk_level": "高危",
      "file_path": "openai-code-review-test/src/main/resources/test.txt",
      "line_number": 1,
      "code_snippet": "mysql.name=root",
      "risk_description": "配置文件中包含明文数据库用户名，可能导致凭证泄露",
      "recommendation": "1. 将敏感信息移至配置中心\n2. 使用加密配置文件"
    },
    {
      "type": "配置文件敏感信息泄露",
      "risk_level": "高危",
      "file_path": "openai-code-review-test/src/main/resources/test.txt",
      "line_number": 2,
      "code_snippet": "mysql.password=rootAdmin",
      "risk_description": "配置文件中包含明文数据库密码，可能导致凭证泄露",
      "recommendation": "1. 将敏感信息移至配置中心\n2. 使用加密配置文件"
    }
  ]
}
```