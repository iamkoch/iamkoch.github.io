---
layout: post
status: publish
published: true
title: Registering all DLLs in an MVC project BIN folder
author: Antony Koch
author_login: amkoch
author_email: ant@iamkoch.com
wordpress_id: 67
wordpress_url: http://localhost/~Ant/wordpress/?p=67
date: '2012-07-15 14:08:28 +0100'
date_gmt: '2012-07-15 14:08:28 +0100'
categories:
- ".Net"
- MVC
tags:
- IoC
- Castle Windsor
comments: []
---
I'm just playing around with the fantastic Castle.Windsor in an MVC project and I needed to register some implementations held in other projects within the solution but hit across some issues so I thought I'd post my solution here. This is my DependencyInjection cs file. It's registered on start up by WebActivator.
{% highlight c# %}
using System;
using System.IO;
using System.Reflection;
using System.Web;
using System.Web.Mvc;
using Castle.MicroKernel.Registration;
using Castle.Windsor;
using Castle.Windsor.Installer;
using WednesdayFootball.Factory;
[assembly: WebActivator.PreApplicationStartMethod(typeof(WednesdayFootball.AppStart.DependencyInjection), &quot;BootstrapContainer&quot;)]
namespace WednesdayFootball.AppStart
{
 public static class DependencyInjection
 {
 private static void BootstrapContainer()
 {
 var container = new WindsorContainer().Install(FromAssembly.This());
 var controllerFactory = new WindsorControllerFactory(container.Kernel);
 ControllerBuilder.Current.SetControllerFactory(controllerFactory);
 RegisterTypes(container);
 }
private static void RegisterTypes(IWindsorContainer container)
 {
 container
 .Register(AllTypes
 .FromAssemblyInDirectory(new AssemblyFilter(AssemblyDirectory))
 .Pick()
 .If(x =&gt; x.IsPublic)
 .If(x =&gt; x.GetInterfaces().Length &gt; 0)
 .WithService
 .FirstInterface()
 .LifestyleTransient());
 }
 static public string AssemblyDirectory
 {
 get
 {
 var codeBase = Assembly.GetExecutingAssembly().CodeBase;
var uri = new UriBuilder(codeBase);
 var path = Uri.UnescapeDataString(uri.Path);
 return Path.GetDirectoryName(path);
 }
 }
 }
}
{% endhighlight %}
