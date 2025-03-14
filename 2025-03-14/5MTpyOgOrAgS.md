```json
{
  "security_issues": [
    {
      "type": "静态常量定义",
      "risk_level": "中危",
      "file_path": "openai-code-review-sdk/src/main/java/plus/gaga/middleware/sdk/OpenAiCodeReview.java",
      "line_number": 166,
      "code_snippet": "+                        ",别忘了进行代码变更评审,代码如下:",
      "risk_description": "代码片段中包含提示信息，建议不要直接在代码中硬编码敏感信息或提示，可能被用于泄露敏感信息。",
      "recommendation": "1. 移除或修改硬编码的提示信息。\n2. 使用配置文件或环境变量来存储这些信息。\n3. 确保配置文件不被包含在版本控制中。"
    }
  ]
}
```