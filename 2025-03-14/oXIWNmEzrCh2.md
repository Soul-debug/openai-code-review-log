```json
{
  "security_issues": [
    {
      "type": "硬编码凭证",
      "risk_level": "高危",
      "file_path": "openai-code-review-sdk/src/main/java/plus/gaga/middleware/sdk/OpenAiCodeReview.java",
      "line_number": 103,
      "code_snippet": "private static final String PASSWORD = \"Password123!\";",
      "risk_description": "在OpenAiCodeReview类中，发现明文密码硬编码。该密码可能被用于多个环境，存在泄露风险。",
      "recommendation": "1. 立即将凭证迁移到安全配置中心\n2. 使用环境变量注入密码信息\n3. 对外发布的代码进行历史提交清理，确保敏感信息不被泄露"
    },
    {
      "type": "硬编码凭证",
      "risk_level": "高危",
      "file_path": "openai-code-review-sdk/src/main/java/plus/gaga/middleware/sdk/OpenAiCodeReview.java",
      "line_number": 111,
      "code_snippet": "String password = \"Password123!\";",
      "risk_description": "在OpenAiCodeReview类中，发现测试代码中硬编码了密码。这可能导致密码泄露。",
      "recommendation": "1. 使用环境变量或配置文件存储密码信息\n2. 在测试环境中使用与生产环境不同的凭证\n3. 清理代码中的硬编码凭证"
    },
    {
      "type": "配置文件敏感信息泄露",
      "risk_level": "中危",
      "file_path": "openai-code-review-test/src/main/resources/test.txt",
      "line_number": 2,
      "code_snippet": "rootAdmin",
      "risk_description": "在测试资源文件中发现配置文件中的明文凭证。这可能导致凭证泄露。",
      "recommendation": "1. 将敏感信息存储在配置中心，不直接写入配置文件\n2. 定期检查配置文件，确保没有敏感信息泄露\n3. 清理资源文件中的敏感信息"
    }
  ]
}
```