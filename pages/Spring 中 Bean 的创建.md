tags:: [[Spring Framework]], [[Spring - 面试重点]] 
---

- ## ==疑问==
	- 属性赋值阶段到底干了啥？
	  logseq.order-list-type:: number
		- 是 @Autowired 之类的注解注入属性吗？
		- 但是我看资料好像 @Autowired 是基于 AutowiredAnnotationBeanPostProcessor 实现，它实现了 BeanPostProcessor 。
	- XXXAware 接口到底什么作用？
	  logseq.order-list-type:: number
	- AOP 和 Bean 的三级缓存的关系
	  logseq.order-list-type:: number
	- 第三级缓存中的 ObjectFactory 是啥
	  logseq.order-list-type:: number
	- DefaultSingletonBeanRegistry
	  logseq.order-list-type:: number
	- BeanFactory 是啥啊
	  logseq.order-list-type:: number
-
- ## SpringApplication.run() 调用链路
	- 以下调用链路是只引用了 `spring-boot-starter` 依赖，代码只写了两个 @Component Bean 的场景：
	- main 方法调用 `SpringApplication.run(App.class, args)`
	  logseq.order-list-type:: number
	- `run`方法内部，调用 `SpringApplication` 的 `run(String... args)`
	  logseq.order-list-type:: number
	- `run`方法内部，调用 `context = createApplicationContext()` 获取 `context` 为 `AnnotationConfigApplicationContext` 的实例。
	  logseq.order-list-type:: number
		- 继承关系: `AnnotationConfigApplicationContext -> GenericApplicationContext -> AbstractApplicationContext -> ConfigurableApplicationContext(接口) -> ApplicationContext(接口)`
	- 得到 `context` 后，调用 `refreshContext(context)` , 内部调用 `context.refresh()` .
	  logseq.order-list-type:: number
	  id:: 6738b12b-28e4-4ee0-9ae6-a332aa31bdcd
		- `refresh()` 方法的实现，来自 `AbstractApplicationContext`
	- `refresh` 方法内部，`obtainFreshBeanFactory()` 获取 `beanFactory` 为 `DefaultListableBeanFactory` 的实例。
	  logseq.order-list-type:: number
		- 继承关系:
			- `DefaultListableBeanFactory -> ConfigurableListableBeanFactory(接口) -> ... -> BeanFactory(接口)`
			- `DefaultListableBeanFactory -> AbstractAutowireCapableBeanFactory -> AbstractBeanFactory -> ... -> BeanFactory(接口)`
			- `DefaultListableBeanFactory -> AbstractAutowireCapableBeanFactory -> AbstractBeanFactory -> FactoryBeanRegistrySupport -> DefaultSingletonBeanRegistry`
	- 得到 `beanFactory` 后，调用 `context` 的 `finishBeanFactoryInitialization(beanFactory)` 方法
	  logseq.order-list-type:: number
		- 该方法来自 `context` 的祖先类 `AbstractApplicationContext` 。
		- 另一方向：
			- 得到 `beanFactory` 后，调用 `context` 的 `invokeBeanFactoryPostProcessors(beanFactory)` 方法
			  logseq.order-list-type:: number
				- 该方法来自 `context` 的祖先类 `AbstractApplicationContext`
			- `invokeBeanFactoryPostProcessors` 方法内部，调用 `PostProcessorRegistrationDelegate.invokeBeanFactoryPostProcessors(beanFactory, getBeanFactoryPostProcessors())`
			  logseq.order-list-type:: number
			- `invokeBeanFactoryPostProcessors` 方法内部，调用 `beanFactory.getBean(ppName, BeanDefinitionRegistryPostProcessor.class)`
			  logseq.order-list-type:: number
				- `getBean()` 方法的实现，来自 `AbstractBeanFactory`
	- `finishBeanFactoryInitialization` 方法内部，调用 `beanFactory` 的 `preInstantiateSingletons()` 方法
	  logseq.order-list-type:: number
		- 该方法来自 `DefaultListableBeanFactory` 。
	- `preInstantiateSingletons()` 方法内部，遍历所有 beanName ，调用 `getBean()` 方法获取 Bean。
	  logseq.order-list-type:: number
		- 该方法来自 `beanFactory` 的祖先类 `AbstractBeanFactory`
	- `getBean` 方法内部，调用 `beanFactory` 的 `doGetBean(name, requiredType, null, false)` 方法。
	  logseq.order-list-type:: number
		- 该方法来自 `beanFactory` 的祖先类 `AbstractBeanFactory`
	- `doGetBean` 方法内部，先调用 `beanFactory` 的 `getSingleton(String beanName)` 方法，用于判断 bean 是否在缓存中。
	  logseq.order-list-type:: number
		- 该方法来自 `beanFactory` 的祖先类 `AbstractBeanFactory` 的祖先类 `DefaultSingletonBeanRegistry` 。
	- `doGetBean` 方法内部，调用 `beanFactory` 的 `getSingleton(String beanName, ObjectFactory<?> singletonFactory)` 方法。
	  logseq.order-list-type:: number
		- 该方法来自 `beanFactory` 的祖先类 `AbstractBeanFactory` 的祖先类 `DefaultSingletonBeanRegistry` 。
	- `getSingleton` 方法传入一个 `ObjectFactory<?>` 接口的实现类，内部调用 `ObjectFactory` 的 `getObject()` 方法，其实就是如下代码：
	  logseq.order-list-type:: number
		- ``` java
		  getSingleton(beanName, () -> {
		    try {
		      return createBean(beanName, mbd, args);
		    }
		    catch (BeansException ex) {
		      // Explicitly remove instance from singleton cache: It might have been put there
		      // eagerly by the creation process, to allow for circular reference resolution.
		      // Also remove any beans that received a temporary reference to the bean.
		      destroySingleton(beanName);
		      throw ex;
		    }
		  });
		  ```
	- `getSingleton` 方法内部其实就是调用了  `beanFactory`  的 `createBean()` 方法。
	  logseq.order-list-type:: number
		- 该方法来自 `beanFactory` 的父类 `AbstractAutowireCapableBeanFactory` 。
	- `createBean()` 方法内部调用 `AbstractAutowireCapableBeanFactory`  的 `doCreateBean()` 方法
	  logseq.order-list-type:: number
	- `doCreateBean()` 方法开始真正创建 bean 。
	  logseq.order-list-type:: number
		- 涉及如下几个主要方法：
			- 实例化：instanceWrapper = createBeanInstance(beanName, mbd, args);
			  logseq.order-list-type:: number
			- 加入三级缓存：addSingletonFactory(beanName, () -> getEarlyBeanReference(beanName, mbd, bean));
			  logseq.order-list-type:: number
			- 属性赋值：populateBean(beanName, mbd, instanceWrapper);
			  logseq.order-list-type:: number
			- 初始化：exposedObject = initializeBean(beanName, exposedObject, mbd);
			  logseq.order-list-type:: number
- ## 创建单例 Bean 的大致流程
	- 创建单例 Bean ，大概有如下流程：
	- preInstantiateSingletons()，遍历所有 BeanName，调用 getBean(beanName) 实例化所有单例 Bean
	- getBean(beanName)
	  logseq.order-list-type:: number
	- doGetBean(String name, @Nullable Class<T> requiredType, @Nullable Object[] args, boolean typeCheckOnly)
	  logseq.order-list-type:: number
		- getSingleton(String beanName, boolean allowEarlyReference)：从缓存中看是否有 Bean，允许获取早期暴露对象
		  logseq.order-list-type:: number
			- 根据 beanName 从一级缓存中取 Bean 的实例：
			  logseq.order-list-type:: number
				- 取到就返回。
				  logseq.order-list-type:: number
				- 没取到就进行下一步。
				  logseq.order-list-type:: number
			- 根据 beanName 从二级缓存中取 Bean 的实例：
			  logseq.order-list-type:: number
				- 取到就返回。
				  logseq.order-list-type:: number
				- 没取到就进行下一步。
				  logseq.order-list-type:: number
			- 根据 beanName 从三级缓存中取 Bean 的 ObjectFactory ：
			  logseq.order-list-type:: number
				- 取到的话：
				  logseq.order-list-type:: number
					- 调用 ObjectFactory 的 getObject()，得到 Bean 的 **前期暴露对象** ；
					  logseq.order-list-type:: number
						- 其实调用的就是 `getEarlyBeanReference(beanName, mbd, bean)` 方法
							- 内部调用 `SmartInstantiationAwareBeanPostProcessor(接口)` 的 `getEarlyBeanReference(exposedObject, beanName)` 方法
							- 如果有 AOP 的话，则会调用 `AbstractAutoProxyCreator` 的 `getEarlyBeanReference(exposedObject, beanName)` 方法：
								- 创建代理对象并返回。
								  logseq.order-list-type:: number
								- 缓存已创建代理的对象。
								  logseq.order-list-type:: number
					- 将这个实例放到二级缓存中。
					  logseq.order-list-type:: number
					- 将三级缓存中的 ObjectFactory 移除。
					  logseq.order-list-type:: number
				- 没取到就返回 null。
				  logseq.order-list-type:: number
		- getSingleton(String beanName, ObjectFactory<?> singletonFactory)：获取单例 Bean
		  logseq.order-list-type:: number
			- createBean(beanName, mbd, args)：创建 Bean。
			  logseq.order-list-type:: number
				- doCreateBean(beanName, mbdToUse, args)：实际创建 Bean。
				  logseq.order-list-type:: number
					- 实例化：createBeanInstance(beanName, mbd, args);
					  logseq.order-list-type:: number
					- 加入三级缓存：addSingletonFactory(beanName, () -> getEarlyBeanReference(beanName, mbd, bean));
					  logseq.order-list-type:: number
					- 属性赋值（@Autowired @Resource @Value）：populateBean(beanName, mbd, instanceWrapper);
					  logseq.order-list-type:: number
						- ==产生循环依赖时，此处会去创建依赖的 Bean ，从 getBean(beanName) 重新开始走 ==
						- mbd.getPropertyValues()：获取 `属性-值`
						  logseq.order-list-type:: number
						- 调用 `InstantiationAwareBeanPostProcessor(接口)` 的 postProcessPropertyValues()：获取最终可用的 `属性-值`
						  logseq.order-list-type:: number
							- `AutowiredAnnotationBeanPostProcessor` 用于 `@Autowired` 的实现
						- applyPropertyValues(beanName, mbd, bw, pvs)：给 Bean 的属性赋值。
						  logseq.order-list-type:: number
					- 初始化：exposedObject = initializeBean(beanName, exposedObject, mbd);
					  logseq.order-list-type:: number
						- invokeAwareMethods(beanName, bean)：执行 `XxxAware` 相关方法
						  logseq.order-list-type:: number
							- BeanNameAware
							  logseq.order-list-type:: number
							- BeanClassLoaderAware
							  logseq.order-list-type:: number
							- BeanFactoryAware
							  logseq.order-list-type:: number
						- applyBeanPostProcessorsBeforeInitialization(wrappedBean, beanName)：执行 `BeanPostProcessor` 的 `postProcessBeforeInitialization` 方法。
						  logseq.order-list-type:: number
							- ApplicationContextAwareProcessor 实现如下几个 Aware 功能：
							  logseq.order-list-type:: number
								- EnvironmentAware
								  logseq.order-list-type:: number
								- EmbeddedValueResolverAware
								  logseq.order-list-type:: number
								- ResourceLoaderAware
								  logseq.order-list-type:: number
								- ResourceLoaderAware
								  logseq.order-list-type:: number
								- MessageSourceAware
								  logseq.order-list-type:: number
								- ApplicationContextAware
								  logseq.order-list-type:: number
							- CommonAnnotationBeanPostProcessor 实现  `@PostConstruct`  功能。
							  logseq.order-list-type:: number
						- invokeInitMethods(beanName, wrappedBean, mbd)：执行 `Init-Method` 。
						  logseq.order-list-type:: number
							- 调用 `InitializingBean` 的 `afterPropertiesSet()` 方法
							  logseq.order-list-type:: number
							- 调用 Bean 定义中的 `init-method` 。
							  logseq.order-list-type:: number
						- applyBeanPostProcessorsAfterInitialization(wrappedBean, beanName)：执行 `BeanPostProcessor` 的 `postProcessAfterInitialization` 方法。
						  logseq.order-list-type:: number
							- 有 AOP 时，会调用 `AbstractAutoProxyCreator` (实现了 `BeanPostProcessor` ) 的 `postProcessAfterInitialization` 方法：
								- 如果对象已创建代理，则直接返回对象本身，因为当前对象已是代理对象
								  logseq.order-list-type:: number
								- 如果对象未创建代理，则会创建代理对象并返回。
								  logseq.order-list-type:: number
			- addSingleton(beanName, singletonObject)：将创建好的 Bean 加入一级缓存。
			  logseq.order-list-type:: number
- ## BeanPostProcessor
	- `ApplicationContextAwareProcessor` 用于实现如下几个 `Aware` 接口的功能 (postProcessBeforeInitialization)：
		- EnvironmentAware
		  logseq.order-list-type:: number
		- EmbeddedValueResolverAware
		  logseq.order-list-type:: number
		- ResourceLoaderAware
		  logseq.order-list-type:: number
		- ResourceLoaderAware
		  logseq.order-list-type:: number
		- MessageSourceAware
		  logseq.order-list-type:: number
		- ApplicationContextAware
		  logseq.order-list-type:: number
	- `AutowiredAnnotationBeanPostProcessor` ，用于实现  `@Autowired` 注解。
	- `CommonAnnotationBeanPostProcessor` 父类 `InitDestroyAnnotationBeanPostProcessor` ，用于实现 `@PostConstruct` 和 `@PreDestroy` 。
- ## AOP Bean 的创建
	- 没有 循环依赖 时，在 initializeBean 阶段创建代理对象。
	  logseq.order-list-type:: number
	- 有 循环依赖 时，在从缓存中获取对象时，通过第三级缓存中 ObjectFactory 的 getObject() 方法创建代理对象。
	  logseq.order-list-type:: number
- ## 三级缓存
	- ### 三级缓存就是三个 Map
		- ``` java
		  // 代码来自 org.springframework.beans.factory.support.DefaultSingletonBeanRegistry
		  // 一级缓存：bean name to bean instance
		  /** Cache of singleton objects: bean name to bean instance. */
		  private final Map<String, Object> singletonObjects = new ConcurrentHashMap<>(256);
		  
		  // 二级缓存：bean name to bean instance
		  /** Cache of early singleton objects: bean name to bean instance. */
		  private final Map<String, Object> earlySingletonObjects = new ConcurrentHashMap<>(16);
		  
		  // 三级缓存：bean name to ObjectFactory
		  /** Cache of singleton factories: bean name to ObjectFactory. */
		  private final Map<String, ObjectFactory<?>> singletonFactories = new HashMap<>(16);
		  ```
	- ### 缓存中取 Bean 的步骤
		- ``` java
		  // 来自 DefaultSingletonBeanRegistry
		  protected Object getSingleton(String beanName, boolean allowEarlyReference) {
		    // Quick check for existing instance without full singleton lock
		    Object singletonObject = this.singletonObjects.get(beanName);
		    if (singletonObject == null && isSingletonCurrentlyInCreation(beanName)) {
		      singletonObject = this.earlySingletonObjects.get(beanName);
		      if (singletonObject == null && allowEarlyReference) {
		        synchronized (this.singletonObjects) {
		          // Consistent creation of early reference within full singleton lock
		          singletonObject = this.singletonObjects.get(beanName);
		          if (singletonObject == null) {
		            singletonObject = this.earlySingletonObjects.get(beanName);
		            if (singletonObject == null) {
		              ObjectFactory<?> singletonFactory = this.singletonFactories.get(beanName);
		              if (singletonFactory != null) {
		                singletonObject = singletonFactory.getObject();
		                this.earlySingletonObjects.put(beanName, singletonObject);
		                this.singletonFactories.remove(beanName);
		              }
		            }
		          }
		        }
		      }
		    }
		    return singletonObject;
		  }
		  ```
		- 根据 beanName 从一级缓存中取 Bean 的实例：
		  logseq.order-list-type:: number
			- 取到就返回。
			  logseq.order-list-type:: number
			- 没取到就进行下一步。
			  logseq.order-list-type:: number
		- 根据 beanName 从二级缓存中取 Bean 的实例：
		  logseq.order-list-type:: number
			- 取到就返回。
			  logseq.order-list-type:: number
			- 没取到就进行下一步。
			  logseq.order-list-type:: number
		- 根据 beanName 从三级缓存中取 Bean 的 ObjectFactory ：
		  logseq.order-list-type:: number
			- 取到的话：
			  logseq.order-list-type:: number
				- 调用 ObjectFactory 的 getObject()，得到 Bean 的 **前期暴露对象** ；
				  logseq.order-list-type:: number
				- 将这个实例放到二级缓存中。
				  logseq.order-list-type:: number
				- 将三级缓存中的 ObjectFactory 移除。
				  logseq.order-list-type:: number
			- 没取到就返回 null
			  logseq.order-list-type:: number
	- ### 循环依赖的创建过程
		- ``` java
		  @Component("beanA")
		  public class BeanA {
		    @Autowired
		    private BeanB beanB;
		  }
		  
		  @Component("beanB")
		  public class BeanB {
		    @Autowired
		    private BeanA beanA;
		  }
		  ```
		- 当我们创建 `BeanA` 时，检查缓存中是否有 `BeanA` 。
		  logseq.order-list-type:: number
			- 因为还没创建，所以没有。
		- 通过反射实例化 `BeanA` 。
		  logseq.order-list-type:: number
			- 调用 `AbstractAutowireCapableBeanFactory` 的 `createBeanInstance(beanName, mbd, args)` 实例化。
		- 将 `BeanA` 的 ObjectFactory 放入三级缓存中。
		  logseq.order-list-type:: number
			- 调用的是 `DefaultSingletonBeanRegistry` 的 `addSingletonFactory(beanName, () -> getEarlyBeanReference(beanName, mbd, bean));`
		- 给 `BeanA` 注入属性时，发现需要 `BeanB` 。
		  logseq.order-list-type:: number
			- `populateBean(beanName, mbd, instanceWrapper)` 会对 @Autowired、@Resource、@Value 等注解标注的属性进行填充。
		- 检查缓存中是否有 `BeanB` 。
		  logseq.order-list-type:: number
			- 因为还没创建，所以没有。
		- 开始 `BeanB` 创建流程。
		  logseq.order-list-type:: number
			- 通过反射实例化 `BeanB` 。
			  logseq.order-list-type:: number
			- 将 `BeanB` 的 ObjectFactory 放入三级缓存中。
			  logseq.order-list-type:: number
			- 给 `BeanB` 注入属性时，发现需要 `BeanA` 。
			  logseq.order-list-type:: number
			- 检查 缓存 中是否有 `BeanA` ，得到 `BeanA` 的实例。
			  logseq.order-list-type:: number
				- 从三级缓存中得到 `BeanA` 的 ObjectFactory，调用 getObject()，得到 `BeanA` 的 **前期暴露对象** 。
				  logseq.order-list-type:: number
				- 将 `BeanA` 的实例放到 二级缓存 中。
				  logseq.order-list-type:: number
				- 将三级缓存中的 `BeanA` 的  ObjectFactory 移除。
				  logseq.order-list-type:: number
			- `BeanB` 成功注入属性 `BeanA`，`BeanB` 创建成功。
			  logseq.order-list-type:: number
			- 初始化 `BeanB` 。
			  logseq.order-list-type:: number
			- `BeanB` 加入到一级缓存中，三级缓存中删除 `BeanB` 。
			  logseq.order-list-type:: number
				- ``` java
				  // DefaultSingletonBeanRegistry
				  protected void addSingleton(String beanName, Object singletonObject) {
				    synchronized (this.singletonObjects) {
				      this.singletonObjects.put(beanName, singletonObject);
				      this.singletonFactories.remove(beanName);
				      this.earlySingletonObjects.remove(beanName);
				      this.registeredSingletons.add(beanName);
				    }
				  }
				  ```
		- `BeanA` 成功注入属性 `BeanB`，`BeanA` 创建成功。
		  logseq.order-list-type:: number
		- `BeanA` 加入到一级缓存中，二级缓存中删除 `BeanA` 。
		  logseq.order-list-type:: number
	- ### 只用一、三级缓存行不行
		- 如果没有循环依赖，那只要有个容器，存储所有 Bean 就可以了，Spring 只要解析得到所有 Bean 的创建顺序，依次创建就不会出现问题。
		  logseq.order-list-type:: number
		- 如果只是解决 循环依赖 问题，甚至只使用一级缓存就能解决。
		  logseq.order-list-type:: number
			- 只要将早期暴露的 `BeanA` 对象放到一级缓存中就可以，后面 `BeanB` 从一级缓存中取就好。
			- 但是，这样在多线程情况下，导致有线程取到没有创建完成的 `BeanA` 。
		- 为了解决上面的问题，可以使用一、三级缓存。
		  logseq.order-list-type:: number
			- 如果三级缓存中存放的是 Bean 的 `ObjectFactory`
			  logseq.order-list-type:: number
				- 将 `BeanA` 的 `ObjectFactory` 放到三级缓存中，后面 `BeanB` 从三级缓存中获取 `ObjectFactory`  ，并调用 `getObject` 方法获取 `BeanA` 的实例。
				- 在 `BeanA` 不需要创建 AOP 代理对象的情况下，每次  `getObject`  获取的都是同一个 `BeanA` 的实例，确实没有问题。
				- 但是，在 `BeanA` 需要创建 AOP 代理对象的情况下：
					- 如果存在多个 Bean 依赖 `BeanA` 的话，可能会出现创建多个 `BeanA` 的代理对象的情况（这就不是单例了），因为每次都会调用 `getObject` 方法创建代理对象。
					- ==此处有没有可能维护一个列表保存已经创建过的代理对象==
			- 如果三级缓存中不存 Bean 的 `ObjectFactory`，改为存 Bean 的 实例 (有 AOP 就是代理对象)
			  logseq.order-list-type:: number
				- ==这样好像也可以避免创建多个代理对象？==
		- 但是，如果考虑到 AOP + 循环依赖 的话，就有问题
		  logseq.order-list-type:: number
			- AOP 和 `AspectJAwareAdvisorAutoProxyCreator` 有关。
				- 继承关系:
					- `AspectJAwareAdvisorAutoProxyCreator` -> `AbstractAdvisorAutoProxyCreator` -> `AbstractAutoProxyCreator` -> `SmartInstantiationAwareBeanPostProcessor(接口)` -> `InstantiationAwareBeanPostProcessor(接口)` -> `BeanPostProcessor(接口)`
	- ### 三级缓存不能解决的循环依赖
		- 多实例 Bean 的循环依赖。
		  logseq.order-list-type:: number
			- 因为多实例的 Bean 不会使用缓存，不使用缓存也就无法解决循环依赖
		- 使用构造器注入。
		  logseq.order-list-type:: number
			- 因为构造器注入需要注入依赖，
	- ### 不推荐编写循环依赖代码
		- 循环依赖是一种设计缺陷，应尽量避免。
		  logseq.order-list-type:: number
		- SpringBoot 2.6.x 之后默认禁止循环依赖 ( 配置 `spring.main.allow-circular-references=true` 可以允许循环依赖 )
		  logseq.order-list-type:: number
-
- ## 参考
	- [Spring的循环依赖，学就完事了【附源码】](https://www.cnblogs.com/summerday152/p/13648377.html)
	  logseq.order-list-type:: number
	- [spring硬核知识点-spring循环依赖-三级缓存](https://www.bilibili.com/video/BV1Fa411j7kc/?vd_source=f1fbb083ddef12dcff3388779faac201)
	  logseq.order-list-type:: number
	- [华为二面：Spring是如何解决循环依赖的？为什么一定要三级缓存？二级缓存能不能解决循环依赖？](https://www.bilibili.com/video/BV19H4y1778T/?vd_source=f1fbb083ddef12dcff3388779faac201)
	  logseq.order-list-type:: number
	- [第二次讲Spring循环依赖，时长16分钟，我保证每一秒都是精华](https://www.bilibili.com/video/BV1ET4y1N7Sp/?vd_source=f1fbb083ddef12dcff3388779faac201)
	  logseq.order-list-type:: number
	- [[java漫谈系列99]spring扩展点之BeanPostProcessor](https://www.bilibili.com/video/BV1Mt42177MK/?vd_source=f1fbb083ddef12dcff3388779faac201)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number