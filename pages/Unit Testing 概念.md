tags:: [[Unit Testing]]
---

- ## 原则
	- 每个单元测试 **必须有断言** 。
	  logseq.order-list-type:: number
	- 一个单元测试 **只测一个场景** 。
	  logseq.order-list-type:: number
	- 一个单元测试函数 **不超过15行** 代码。
	  logseq.order-list-type:: number
	- 所有单元测试函数均 **可独立、重复运行** 。
	  logseq.order-list-type:: number
	- 所有单元测试函数执行必须是 **毫秒级** 。
	  logseq.order-list-type:: number
	- 应该非常 **频繁地执行** ，每增加、修改、删除一个测试都要运行一次。
	  logseq.order-list-type:: number
- ## 测试函数3A模式
	- **Arrange** all necessary preconditions and inputs. 准备测试上下文的环境、输入
	- **Act** on the object or method under test. 执行被测函数
	- **Assert** that the expected results have occurred. 断言
	- 例子：
	- ```java
	  import static org.junit.Assert.assertEquals;
	  import org.junit.Test;
	  
	  public class CalculatorTest {
	      @Test
	      public void add_forPosivite_returnSum() {
	          // 1、准备测试上下文环境、数据
	          Calculator calculator = new Calculator();
	          // 2、执行被测函数
	          double result = calculator.add(50, 150);
	          // 3、断言
	          assertEquals("Failure Messages ", 200, result, 0);
	      }
	  }
	  ```
- ## 命名规范
	- ### 包名规范
		- 源代码在  `src/main/java` 目录，单元测试代码在 `src/test/java` 目录下，与被测代码同包名，src/test/java/ + 包目录
	- ### 类名规范
		- 一个被测类对应一个测试类的情况：被测类名 + “Test”
			- 正例：
				- 被测类名：BA5MinCellHelper
				- 测试类名：BA5MinCellHelperTest
		- 一个被测类对应多个测试类的情况：被测类名 + “_” + 场景 + “Test”
			- 正例：
				- 被测类名：TimeUnitUtil
				- 测试类名1：TimeUnitUtil_RegionTest
				- 测试类名2：TimeUnitUtil_SamplingTest
	- ### 函数名规范
		- `public void 被测函数名_测试场景_期望()` （ **测试场景** 与 **期望值** 可以使用中文）
		- 其中 **期望** 采用 **动宾结构** ：
			- **有返回值** ：采用 returnAAA 的结构
				- 正例：returnEmpty、returnZero、returnTrue
			- **异常** ：采用throwAAA的结构。
				- 正例：throwNullPointerException、throwArrayIndexOutOfBoundsException
			- **没有返回值** ：情况比较多，保持动宾结构。
				- 正例：
					- 检查状态：checkStatus
					- 检查测试类型：checkTestType
- ## 测试函数
	- ### 不建议测试的函数
		- 简单 get、set 函数
		- 多线程 函数 (需要将多线程部分和业务剥离)
	- ### private 函数
		- **测试私有方法是错误的！**
		- private 函数通常都可以通过 public 方法的测试覆盖；如果不好覆盖，优先考虑代码结构问题。
		- 如果遇到非测不可的场景，建议采用以下方法：
			- 抽取方法，形成新类
			- 将私有方法升级为公有方法
- ## 断言
	- ### 集合的断言
		- 尽量完整断言。如果不好处理，从以下几方面断言：
			- 断言集合大小；
			- 断言首尾元素；
			- 抽样断言；
			- 元素顺序；
			- 重复项；
- ## 测试用例设计
	- ### 原则
		- 在单元测试中，我们应该尽量 **避免使用白盒测试法** ，尽量使用黑盒测试方法。
	- ### 黑盒测试方法
		- #### 等价类划分法
			- 把所有可能的输入数据，划分成若干个子集，然后从每一个子集中选取少数具有代表性的数据作为测试用例。
			- **有效等价类** : 对于程序的规格说明是 **合理的、有意义的** 输入数据构成的集合。
			- **无效等价类** : 对于程序的规格说明是 **不合理的或无意义** 的输入数据所构成的集合。
			- 例子：计算两个点距离的函数 : `public double getDistance(double x1, double y1, double x2, double y2)`
			- | **等价类划分** | **有效等价类** | **无效等价类** |
			  | x1 | 0<=x1<=180 | 负数；>180 |
			  | Y1 | 0<=y1<=90 | 负数；>90 |
			  | X2 | 0<=x2<=180 | 负数；>180 |
			  | y2 | 0<=y2<=90 | 负数；>90 |
		- **注意** : 每个测试用例，应该 **只覆盖一个参数的无效等价类** 。比如如果规格说明规定了“请输入书籍类型（硬皮、软皮或活页）及数量（1~999）”，代表两个错误输入（书籍类型错误，数量错误）的测试用例“（XYZ，0）”，很可能不会执行对数量的检查，因为程序也许会提示“XYZ是未知的书籍类型”，就不检查输入的其余部分了。
		- #### 边界值法
			- 对输入或输出的边界值进行测试的一组黑盒测试方法。
			- 通常边界值分析法是作为对 **等价类划分法** 的补充，这种情况下，其测试用例来自 **等价类的边界** 。
			-
	- ### 白盒测试方法
		- #### 路径分析法
			- 它在程序控制图的基础上，通过分析程序控制构造，导出基本可执行路径集合，从而设计测试用例。
			- 设计出的测试用例要保证在测试中程序的 **每一个可执行语句** 至少执行一次。
- ## 依赖解耦
	- ### 什么是外部依赖
		- 指在系统中与代码交互的对象，无法对其进行人为控制。如 系统时间、WEB服务、文件系统、数据库服务、内网 等。
	- ### 什么是反测试设计
		- 代码依赖于外部资源，即使其逻辑非常正确，也可能导致测试失败。
		- 系统代码的类或者方法可能依赖于多项不可控的外部资源。
	- ### 如何解耦依赖
		- #### 提取与重写 法
			- 1. 在 **被测试类** 中，提取出被测方法中 **涉及外部依赖的代码** ，独立成一个方法（一个方法只做一件事情）。
			  2. 在 **测试类中** 定义一个新的类继承 **修改后的被测试类** ，重写该方法，返回你所期望的结果。
			- 举例：
			- ``` java
			  public class LogAnalyzer {
			  	private boolean wasLastFileNameValid;
			  	private String defaultFilename = "";
			  
			  	public boolean isValidLogFileName(String fileName) {
			  		if (fileName == null || fileName.isEmpty()) {
			  			fileName = this.defaultFilename;
			  		}
			  
			  		if (fileName.length() > 16 || fileName.length() < 6) {
			  			wasLastFileNameValid = false;
			  			return false;
			  		}
			  
			  		if (!fileName.toLowerCase().endsWith(".slf")) {
			  			wasLastFileNameValid = false;
			  			return false;
			  		}
			  
			  		// 文件系统检测是否支持
			  		FileExtensionManager fileManager = new FileExtensionManager();
			  		if (!fileManager.IsSupportedExtension(fileName)) {
			  			wasLastFileNameValid = false;
			  			return false;
			  		}
			  
			  		wasLastFileNameValid = true;
			  		return true;
			  	}
			  }
			  ```
			- 上面代码的 **注释处(21-25行)** 依赖外部的文件系统，需要将方法提取出来。
			- ``` java
			  public class LogAnalyzer {
			  	private boolean wasLastFileNameValid;
			  	private String defaultFilename = "";
			  
			  	public boolean isValidLogFileName(String fileName) {
			  		if (fileName == null || fileName.isEmpty()) {
			  			fileName = this.defaultFilename;
			  		}
			  
			  		if (fileName.length() > 16 || fileName.length() < 6) {
			  			wasLastFileNameValid = false;
			  			return false;
			  		}
			  
			  		if (!fileName.toLowerCase().endsWith(".slf")) {
			  			wasLastFileNameValid = false;
			  			return false;
			  		}
			  
			  		// 文件系统检测是否支持
			  		if (!isSupportedExtension(fileName)) {
			  			wasLastFileNameValid = false;
			  			return false;
			  		}
			  		
			  		wasLastFileNameValid = true;
			  		return true;
			  	}
			  
			  	protected boolean isSupportedExtension(String fileName) {
			  		FileExtensionManager fileManager = new FileExtensionManager();
			  		return fileManager.IsSupportedExtension(fileName);
			  	}
			  }
			  ```
			- 测试类代码：
			- ``` java
			  public class LogAnalyzerTest {
			  	class TestableLogAnalyzer extends LogAnalyzer {
			  		private boolean isSupported;
			  
			  		public TestableLogAnalyzer(boolean isSupported) {
			  			this.isSupported = isSupported;
			  		}
			  
			  		@Override
			  		protected boolean isSupportedExtension(String fileName) {
			  			return isSupported;
			  		}
			  	}
			  
			  	@Test
			  	public void testIsValidLogFileName() {
			  		TestableLogAnalyzer testableLogAnalyzer = new TestableLogAnalyzer(true);
			  
			  		boolean result = testableLogAnalyzer.isValidLogFileName("shortfile.slf");
			  		assertTrue(result);
			  	}
			  
			  	@Test
			  	public void testIsInValidLogFileName() {
			  		TestableLogAnalyzer testableLogAnalyzer = new TestableLogAnalyzer(false);
			  
			  		boolean result = testableLogAnalyzer.isValidLogFileName("shortfile.slf");
			  		assertFalse(result);
			  	}
			  }
			  ```
			- 1. TestableLogAnalyzer 继承 LogAnalyzer ，重写 isSupportedExtension() 方法
			- 2. 增加状态变量 isSupported ，根据测试场景返回期望值。
			- 被测试类从 LogAnalyzer 变成 TestableLogAnalyzer。
		- #### [[Stub]]
			- 与 提取与重写 法不同的是：Stub是Fake了一个依赖的对象，后者是Fake了一个被测类的对象。
		- [[Mock]]
		- [[Spy]]
		- #### Fake、Stub与Mock
			- **Fake** : 当想要一个可重用的具体实现时，请使用 Fake，该实现与真实实现类似，具有跨测试的可重用性（例如内存数据库）
			- **Stub** : 当想要在测试中重复使用的硬编码响应/实现时使用存根Stub 。
			- **Mock** : 当需要对单个测试进行动态响应时使用 Mock
-