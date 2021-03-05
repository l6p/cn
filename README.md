# 欢迎使用 Lollipop

Lollipop 是一个基于 Kubernetes 的免费性能测试工具。使用它可以方便灵活的应用云平台资源发起性能测试和查看测试报告。
并且可以尽早的发现系统在性能上存在的问题，帮助您构建更加强壮和可扩展的系统。

## Lollipop 的主要优势

### 基于云原生的顶层设计

Lollipop 的测试引擎和管理平台都基于 Kubernetes 运行。基于 Kubernetes 的高可移植性，Lollipop 既可以在企业的云平台上部署，也可以在个人的电脑上运行。
当 Lollipop 运行在企业的私有云或公有云平台上时，可以充分利用企业现有云平台的计算资源进行自动化测试，无需增加额外的硬件成本。
企业可以利用 Kubernetes 的能力为 Lollipop 进行节点管控和资源分配，充分控制性能测试的成本。

### 高效的性能和较低的测试成本

Lollipop 基于 Go 语言开发，具备卓越的性能。可以使用较小的CPU和内存消耗产生较大的系统负载，从而挑战系统的访问上线或计算平均的RPM。
Lollipop 可以允许用户自定义测试中虚拟用户所使用的 CPU 和内存的大小，从而在整体上控制测试成本。

### 专业合理的测试规范

测试整体被分为 SetUp、WarmUp、测试和 TearDown 三个阶段。SetUp 作为数据准备阶段，该阶段准备的数据可以自动通过上下文同步到所有测试引擎的工作节点。 WarmUp 阶段可以为被测系统预热，负载将线性增⻓。测试结束后可以在 TearDown 阶段释放加载的测试资源。
虚拟用户可以按类型划分，可以为每种类型的虚拟用户定制不同的测试计划。虚拟用户在执行测试计划的过程中可以被划分为一个或多个会话周期，会话周期用以模拟真实情况下的用户行为，例如:登入系统、登出系统。

### 高效精确的测试数据统计

Lollipop提供独立的、基于Flink的数据分析模块提供实时数据统计。数据统计分为访问请求和测试用例两个维度。当进行基于浏览器的端到端测试时，系统会自动获取浏览器发出的所有HTTP请求加以统计分析。
为了提供更大的灵活性，测试引擎和数据分析模块间通过Kafka消息队列连接。用户也可以自行从消息队列中提取数据加以利用。

## 安装说明

- [预先的准备](Installation/Prerequisite.html)
- [安装 Lollipop](Installation/InstallingLollipop.html)

## 使用 Lollipop

- [运行您的第一个测试](UsingLollipop/RunYourFirstTest.html)
- [Using Customized Test Data](/UsingLollipop/UsingCustomizedTestData.html)
- [View Logs](/UsingLollipop/ViewLogs.html)
- [View Test Reports](/UsingLollipop/ViewTestReports.html)

## Testing Guides

- [Performance Test Cycle](/TestingGuides/PerformanceTestCycle.html)
- [Rationalize The Number Of VUsers](/TestingGuides/RationalizeTheNumberOfVUsers.html)

## Script Guides

- [Initializing The Script Project](/ScriptGuides/InitializingTheScriptProject.html)
- [Creating Test Cases](/ScriptGuides/CreatingTestCases.html)
- [Getting JSON Data](/ScriptGuides/GettingJsonData.html)
- [SetUp And TearDown](/ScriptGuides/SetUpAndTearDown.html)
- [Using Context](/ScriptGuides/UsingContext.html)
- [Using Chrome](/ScriptGuides/UsingChrome.html)

## Utilities

- [JSON Utility](/Utilities/JsonUtility/)
