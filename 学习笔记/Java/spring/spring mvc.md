#  						spring mvc						

DispatcherServlet本质上就是一个Servlet,那么肯定会有一个doService()方法来处理所有的HTTP请求

方法中有个叫doDispatch()方法,方法签名上的注释第一句就写了,这个方法的作用是什么:

```Java
Process the actual dispatching to the handler.
```



![spring mvc图解](D:\DownloadAndData\个人资料\学习笔记\Java\spring\spring mvc图解.png)

```java

// 途中的第二步真正的处理过程就是以下这个方法
// 通过debug的方式可以得知,该方法通过遍历的方式为请求匹配合适的handler,并定位我们写好的业务Controller
protected HandlerExecutionChain getHandler(HttpServletRequest request) throws Exception {
		if (this.handlerMappings != null) {
			for (HandlerMapping mapping : this.handlerMappings) {
				HandlerExecutionChain handler = mapping.getHandler(request);
				if (handler != null) {
					return handler;
				}
			}
		}
		return null;
	}
```

那么HandlerExecutionChain是什么呢?

```Java
	/**
	 * Create a new HandlerExecutionChain.
	 * @param handler the handler object to execute
	 * @param interceptors the array of interceptors to apply
	 * (in the given order) before the handler itself executes
	 */
	 // 代码中可知HandlerExecutionChain = handler + HandlerInterceptor集合
	 // 并且interceptors会根据给定的顺序先于handler执行
public HandlerExecutionChain(Object handler, @Nullable HandlerInterceptor... interceptors) {
		if (handler instanceof HandlerExecutionChain) {
			HandlerExecutionChain originalChain = (HandlerExecutionChain) handler;
			this.handler = originalChain.getHandler();
			this.interceptorList = new ArrayList<>();
			CollectionUtils.mergeArrayIntoCollection(originalChain.getInterceptors(), this.interceptorList);
			CollectionUtils.mergeArrayIntoCollection(interceptors, this.interceptorList);
		}
		else {
			this.handler = handler;
			this.interceptors = interceptors;
		}
	}
```

找到我们想要的Controller之后,那么我们需要合适的方法去解析他们,

```java
protected HandlerAdapter getHandlerAdapter(Object handler) throws ServletException {
		if (this.handlerAdapters != null) {
			for (HandlerAdapter adapter : this.handlerAdapters) {
				if (adapter.supports(handler)) {
					return adapter;
				}
			}
		}
		throw new ServletException("No adapter for handler [" + handler +
				"]: The DispatcherServlet configuration needs to include a HandlerAdapter that supports this handler");
	}
```

同样,通过遍历的方式,去获取合适的Adapter,值得一提的是,这里用到了适配器模式

遗留问题:

适配器模式的好处是什么?

拦截器的方法在什么时候执行?