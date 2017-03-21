package com.test.动态代理;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;

public class MyInvocationHandler implements InvocationHandler {
	// 目标对象（需要被代理的对象）
	private Object target;

	public void setTarget(Object target) {
		this.target = target;
	}
	/**
	 * 执行代理对象的所有方法时都会被替换成执行如下的invoke方法
	 */
	@Override
	public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
		// 实例化一个增强类
		Extend extend = new Extend();
		// 执行增强方法1（模拟spring前置增强）
		extend.ExtendMethod1();
		Object result = method.invoke(target, args);// 【执行目标方法】
		// 执行增强方法2（模拟spring后置增强）
		extend.ExtendMethod2();
		return result;
	}
	
}
