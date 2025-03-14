```json
{
  "security_issues": [
    {
      "type": "硬编码凭证",
      "risk_level": "高危",
      "file_path": "openai-code-review-sdk/src/main/java/plus/gaga/middleware/sdk/OpenAiCodeReview.java",
      "line_number": 109,
      "code_snippet": "private static String apiKeySecret = \"45b87abe6d6241da9660e36d7791455b.c3e9Ewb6dqsArvGH\";",
      "risk_description": "在代码中发现了API密钥硬编码，这可能导致密钥泄露。",
      "recommendation": "1. 将API密钥移至环境变量或配置文件中，避免硬编码。\n2. 使用配置中心管理敏感信息。\n3. 定期审计代码，确保没有敏感信息泄露。"
    },
    {
      "type": "硬编码凭证",
      "risk_level": "高危",
      "file_path": "openai-code-review-sdk/src/main/java/plus/gaga/middleware/sdk/OpenAiCodeReview.java",
      "line_number": 131,
      "code_snippet": "-        add(new ChatCompletionRequest.Prompt(\"system\", \"你是一个【高级编程架构师】，精通各类场景方案、架构设计和编程语言请，请您根据git diff记录，对代码做出评审。另一件事需要注意的是，你的答复必须是中文！\" ++\n" +
                          "++                        \"【输出格式要求】\" ++\n" +
                          "++                        \"代码变更评审用markdown格式输出\" ++\n" +
                          "++                        \",代码如下:\"));",
      "risk_description": "代码中包含了输出格式要求的字符串，可能无意中暴露了敏感信息。",
      "recommendation": "1. 移除或修改可能暴露敏感信息的字符串。\n2. 确保代码中的信息不会泄露任何敏感配置或凭证。"
    },
    {
      "type": "硬编码凭证",
      "risk_level": "中危",
      "file_path": "openai-code-review-sdk/src/main/java/plus/gaga/middleware/sdk/OpenAiCodeReview.java",
      "line_number": 109,
      "code_snippet": "-        String password = \"Password456!\";",
      "risk_description": "在代码中发现了密码硬编码，这可能导致密码泄露。",
      "recommendation": "1. 将密码移至环境变量或配置文件中，避免硬编码。\n2. 使用强密码策略，并定期更换密码。\n3. 确保配置文件不被包含在版本控制中。"
    }
  ]
}
```