```markdown
## 代码变更评审报告

### [变更分类1] 指令格式规范变更
**变更前**：
"1. 如果存在安全漏洞，则两个输出区块必须完整存在\n" +

**变更后**：
"1. 如果存在安全漏洞，则两个输出区块必须完整存在,代码评审Markdown输出，安全漏洞JSON输出\n" +

**评审意见**：
- 技术影响分析：明确输出格式要求，避免指令歧义
- 改进建议：补充格式校验逻辑确保输出规范
- 关联检查项：检查输出处理器是否支持双格式混合解析

### [变更分类2] 生产环境配置新增
**新增配置**：
```yaml
privateKey: MIIBVAIBADANBgkqhkiG...（RSA私钥）
spring.datasource:
  dynamic:
    datasource:
      d-data:
        url: jdbc:mysql://12.12.12.12:3306/d_data
        username: test
        password: testPassword
```

**配置作用**：
1. privateKey：用于加密/签名操作的RSA私钥
2. 数据库配置：生产环境MySQL连接配置

**安全问题**：
- 私钥明文存储违反密钥管理规范
- 数据库密码明文存储
- 使用简单密码（testPassword）
- 生产数据库未启用SSL

## 注意事项
1. 安全合规性：立即移除配置中的明文私钥和密码
2. 密钥管理：采用HSM或KMS进行密钥生命周期管理
3. 连接安全：数据库启用SSL并验证证书
4. 访问控制：限制数据库IP白名单
```

```json
SECURITY_ISSUES: {
  "security_issues": [
    {
      "type": "硬编码私钥",
      "risk_level": "高危",
      "file_path": "openai-code-review-test/src/main/resources/application-prod.yml:7",
      "code_snippet": "privateKey: MIIBVAIBADANBgkqhkiG...",
      "risk_description": "检测到RSA私钥明文存储",
      "recommendation": "1. 使用AWS KMS密钥托管服务\n2. 通过环境变量注入密钥"
    },
    {
      "type": "数据库明文凭证",
      "risk_level": "高危",
      "file_path": "openai-code-review-test/src/main/resources/application-prod.yml:15",
      "code_snippet": "password: testPassword",
      "risk_description": "数据库密码明文存储且强度不足",
      "recommendation": "1. 使用Vault动态生成凭据\n2. 密码复杂度至少16位含特殊字符"
    }
  ]
}
```