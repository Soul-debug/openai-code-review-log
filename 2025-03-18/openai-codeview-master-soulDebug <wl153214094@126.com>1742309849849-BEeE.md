```markdown
## 代码变更评审报告

### [文档规范完善]
**变更前**：
"  3. 最后添加注意事项章节\n\n" +

**变更后**：
"  3. 最后添加注意事项章节,如果存在性能瓶颈、安全合规性、代码质量等问题请指出\n\n" +

**评审意见**：
- 技术影响分析：增强文档规范完整性，明确注意事项要求范围
- 改进建议：建议同步更新配套文档模板文件
- 关联检查项：检查所有文档生成点的格式一致性

### [新增算法实现]
**新增类说明**：
BubbleSortLow.java实现经典冒泡排序算法，包含：
1. 双重循环比较相邻元素
2. 元素交换逻辑
3. 测试main方法

**安全问题分析**：
- 算法复杂度O(n²)存在性能瓶颈
- 缺少输入数据校验机制
- 测试用例硬编码但无敏感数据

## 注意事项
- 性能优化：建议增加提前终止标志位优化算法
- 测试验证：需要补充大规模数据压测用例
- 监控指标：建议增加排序耗时监控埋点
```

```json
{
  "security_issues": [
    {
      "type": "测试数据硬编码",
      "risk_level": "低危",
      "file_path": "openai-code-review-test/src/main/java/plus/gaga/middleware/BubbleSortLow.java:19",
      "code_snippet": "int[] arr = {64, 34, 25, 12, 22, 11, 90};",
      "risk_description": "测试数据直接嵌入代码",
      "recommendation": "1. 使用随机测试数据生成器\n2. 分离测试数据与核心算法"
    }
  ]
}
```

```diff
diff --git a/openai-code-review-sdk/src/main/java/plus/gaga/middleware/sdk/domain/service/impl/OpenAiCodeReviewService.java b/openai-code-review-sdk/src/main/java/plus/gaga/middleware/sdk/domain/service/impl/OpenAiCodeReviewService.java
index 6694bdd..11e1217 100644
--- a/openai-code-review-sdk/src/main/java/plus/gaga/middleware/sdk/domain/service/impl/OpenAiCodeReviewService.java
+++ b/openai-code-review-sdk/src/main/java/plus/gaga/middleware/sdk/domain/service/impl/OpenAiCodeReviewService.java
@@ -154,7 +154,7 @@ public class OpenAiCodeReviewService extends AbstractOpenAiCodeReviewService {
                                 "     a. 变更前/后对比\n" +
                                 "     b. 专业评审意见\n" +
                                 "     c. 关联检查建议\n" +
-                                "  3. 最后添加注意事项章节\n\n" +
+                                "  3. 最后添加注意事项章节,如果存在性能瓶颈、安全合规性、代码质量等问题请指出\n\n" +
 
                                 "## 角色2：安全工程师（JSON输出）\n" +
                                 "- 任务：执行安全漏洞扫描\n" +
@@ -216,7 +216,7 @@ public class OpenAiCodeReviewService extends AbstractOpenAiCodeReviewService {
                                 "```\n\n" +
 
                                 "# 强制约束条件\n" +
-                                "1. 两个输出区块必须完整存在\n" +
+                                "1. 如果存在安全漏洞，则两个输出区块必须完整存在\n" +
                                 "2. 修复建议需包含具体实施方案\n" +
                                 "3. 安全扫描结果必须包含具体代码定位\n" +
                                 "4. user参数的git diff的内容化完整输出到最下面" +
diff --git a/openai-code-review-test/src/main/java/plus/gaga/middleware/BubbleSortLow.java b/openai-code-review-test/src/main/java/plus/gaga/middleware/BubbleSortLow.java
new file mode 100644
index 0000000..9c9a63c
--- /dev/null
+++ b/openai-code-review-test/src/main/java/plus/gaga/middleware/BubbleSortLow.java
@@ -0,0 +1,27 @@
+package plus.gaga.middleware;
+
+
+public class BubbleSortLow {
+    public static void bubbleSort(int[] arr) {
+        int n = arr.length;
+        for (int i = 0; i < n - 1; i++) {
+            for (int j = 0; j < n - i - 1; j++) {
+                if (arr[j] > arr[j + 1]) {
+                    // 交换 arr[j] 和 arr[j+1]
+                    int temp = arr[j];
+                    arr[j] = arr[j + 1];
+                    arr[j + 1] = temp;
+                }
+            }
+        }
+    }
+
+    public static void main(String[] args) {
+        int[] arr = {64, 34, 25, 12, 22, 11, 90};
+        bubbleSort(arr);
+        System.out.println("排序后的数组:");
+        for (int i : arr) {
+            System.out.print(i + " ");
+        }
+    }
+}
```